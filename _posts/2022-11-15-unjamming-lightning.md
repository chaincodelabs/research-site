---
layout: post
title: Unjamming Lightning
---

This post summarizes a [recent paper](https://eprint.iacr.org/2022/1454) by Clara Shikhelman and Sergei Tikhomirov on countermeasures against jamming in the Lightning Network.

Jamming is a denial-of-service attack in Lightning.
An adversary can cheaply block payment channels by initiating payments and delaying their finalization.
Multiple countermeasures against jamming have been proposed but none have been yet implemented.

After carefully reviewing the available design options, we propose a two-part solution.
We combine unconditional fees (applied to failed as well as successful payments) and local peer reputation.
Unconditional fees impose costs on the adversary, especially for jams that are resolved quickly.
Local reputation, in turn, protect channels from long-held jams by allocating less resources to less trusted peers.

We believe that our proposal strikes a good balance between effectiveness and practicality.
Simulations show that unconditional fees don't have to be high to fully compensate the victims.
The UX burden of unconditional fees shouldn't be a showstopper, given that payments generally succeed after a few attempts.
We also analyze our solution in terms of security, privacy, and incentive compatibility.
We conclude that the proposal is practical and comparatively straightforward to implement.

<!-- insert video presentation later -->


1. [Lightning 101](#lightning-101)
2. [Channel Jamming](#channel-jamming)
3. [Unconditional Fees](#unconditional-fees)
4. [Local Reputation](#local-reputation)
5. [Future Work](#future-work)
6. [Conclusion](#conclusion)


# Lightning 101

The Lightning Network (LN) is a payment channel network on top of Bitcoin.
A channel is an instance of a cryptographic protocol between two nodes.
Channel partners lock-up bitcoins into a jointly owned address and make low-latency payments off-chain.
A penalty mechanism ensures cryptoeconomic security of balance updates.
Lightning supports multi-hop payments, which involve an atomic chain of balance updates along a path from the sender to the receiver.
Routing nodes earn fees from payments they forward.

Lightning's protocol design strongly emphasizes privacy.
Payments are onion-routed: an intermediary node only knows its immediate neighbors on the path, but not the ultimate sender or receiver.[[^1]]
In the security context, enhanced privacy makes difficult to punish remote adversarial nodes: it's simply unclear who the attacker is.

[^1]: [Timing attacks](https://arxiv.org/abs/2006.12143) erode this security property.

# Channel Jamming

Jamming is a denial-of-service attack on Lightning channels.
An attacker sets up two nodes and initiates a payment between them, but doesn't finalize it promptly.
Coins (aka liquidity) remains stuck (_in-flight_) in all channels along the route and cannot be used to forward other payments.
As a result, the victims lose cannot send or receive payments and lose potential fee revenue.

An in-flight payment occupies one _payment slot_ and a portion of _liquidity_ of a channel.
Jamming, therefore, can either target slots (slot-based) or liquidity (liquidity-based).
Jammed channels remain unusable until the attacker fails the jams or the victim closes the channel.

We differentiate between _quick_ and _slow_ jamming.
Quick jams are resolved and sent again every few seconds,
which them hardly distinguishable from failing honest payments.
Slow jams, in contrast, remain in-flight for hours or even days.[[^2]]
Slow jamming is easily detectable, but the victim can't do much to stop an ongoing attack (besides closing the channel).

[^2]: The exact boundary between quick and slow jamming is somewhat subjective.

Multiple countermeasures against jamming [have](https://blog.bitmex.com/preventing-channel-jamming/) [been](https://github.com/t-bast/lightning-docs/blob/master/spam-prevention.md) [discussed](https://bitcoinproblems.org/problems/channel-jamming.html).
The two major directions are _fees_ and _reputation_.
First, we could impose fees on the attacker, making jamming at least a minimally costly.
Currently, jamming is essentially free: fees are only charged when the payment succeeds, while jams always fail.[[^3]]
Second, we could limit the amount of resources available for the attacker.
Such a countermeasure would involve some notion of "good" and "bad" payments, where "good" payments are routed on the best effort basis, whereas "bad" (or "risky") payments only occupy a portion of channel resources.
Under such a scheme, a low-reputation jammer can never jam channels fully.
The key question is how to assign reputation scores while avoiding centralization.

[^3]: The same is true for [channel balance probing](https://s-tikhomirov.github.io/lightning-probing-2/).

We take a systematic approach to constructing an anti-jamming countermeasure.
We start by outlining the desired properties of a potential solution.
Besides being effective, it should meet the following requirements:

- be incentive compatible;
- avoid deteriorating the user experience;
- introduce no new attack vectors (including privacy leaks);
- be easily implementable.

We then list the design decisions to be made when constructing a protocol upgrade.
Ultimately, we converge on a combination of unconditional fees and local reputation.
Please refer to the [paper](https://eprint.iacr.org/2022/1454) for detailed discussion.


# Unconditional Fees

Unconditional fees, which are paid regardless of payment success, aim at discouraging quick jamming.
The existing (success-case) fees remain in place.
Unconditional fees may be implemented in different ways.
One way would be _upfront_ fees (paid when the payment is offered).
An alternative approach implies that if the payment fails, the downstream node keeps part of the in-flight value as a fail-case fee.

Unconditional fees inherit the structure of success-case fees.
Fees of both types consist of a base fee and a proportional part that depends on the payment amount.
The coefficients, however, can be much lower for unconditional fees than for their success-case counterparts, as our simulations indicate.

When deciding how much to charge unconditionally, we may pursue different goals.
Ideally, we would like to make the attack prohibitively expensive.
However, that may impose too much of a burden on honest users.
A more realistic goal is to compensate the routing node under attack for the lost revenue.

We have implemented a [simulator](https://github.com/s-tikhomirov/ln-jamming-simulator) that models LN payments with unconditional fees.
Under certain assumptions about the honest payment flow, we have shown that increasing the total fee by just 2% (paid unconditionally) fully compensates a routing node.
In other words, if the success-case fee is 100 coins, additionally charging 2 coins upfront for all payments is sufficient: the node would receive the same revenue form frequent fail-case fees from jams compared to what honest payments normally pay.

We also consider the UX implications of unconditional fees.
The concern is that users won't be willing to pay for failed payment attempts.
We argue, however, that this should not be a deal-breaker.
The reasoning is that the total unconditional fee stays low even if the failure rate is reasonably high.
For instance, if every attempt has a 20% chance of failure, a payment has a 99% chance of succeeding after just three attempts.


# Local Reputation

Fees are ineffective against slow jamming attacks that only involve a few jams.
Instead, we address slow jamming using local reputation.

We suggest that nodes keep track of their peers' past behavior.
A routing node considers its peer _high-reputation_ if it only forwards honest payments that resolve quickly and bring in sufficient fee revenue.
A peer that forwards jams, in contrast, is labeled _low-reputation_.
Nodes may (but don't have to) _endorse_ payments that they forward.
A payment endorsed by a high-reputation peer are considered _low-risk_.
They are forwarded on the best efforts basis, as per the current protocol.
_High-risk_ payments, in contrast, can only use a predefined quota of liquidity and slots.
A high-risk payment is dropped if the next channel lacks slots or liquidity in its high-risk quota, even if it could technically forward the payment.
Unless the attacker builds up a reputation in advance, it cannot fully jam a channel with at least some resources outside of the high-risk quota.
Nodes parameterize their reputation algorithms according to their risk tolerance.

Our reputation scheme is local.
Nodes only assign reputation scores to their peers, not all nodes on the network.
Additionally, the risk level of a payment is determined by a routing node based on its local opinion of the upstream peer.
The sender's identity is not attached to payments, otherwise privacy could be endangered.

From the incentives standpoint, the scheme can be parameterized to make it in the routing nodes' best interest to endorse payments based on their true perception of their risk levels.
Implementation-wise, local reputation is beneficial as it requires no coordination.
Each node reflects its own risk preferences by tuning its reputation adjustment parameters.


# Future Work

Lightning community has debated jamming countermeasures for years.
Most mitigation ideas may be well worth exploring further, even though we have dismissed them in this work.
We have decided to emphasize practicality and have (hopefully) come up with a simple yet efficient solution that can be implemented in the near future.

One idea that we'd love to be thoroughly studied is time-dependent fee amounts.
Lightning fees (both in the existing protocol and in our proposal) do not depend on the actual payment resolution time.
Routing nodes face uncertainty: they provide access to resources for the same fee regardless of whether these resources are occupied for a second or for a day.
From the economical standpoint, we'd like the fees to reflect the time-value of resources the payment consumes.
However, it's unclear how to implement such fees without a (semi-)trusted time signal.

Privacy-preserving reputation is another promising research direction.
Jamming illustrates the dilemma that anonymity-preserving P2P network face.
Given that identities are ephemeral and obfuscated in such networks, how do we prevent malicious actors from abusing the system?
An ideal reputation system would allow routing nodes to filter out bad actors without revealing their (or anyone else's) identities.
Further research in this direction would be highly appreciated.


# Conclusion

In this work, we propose a mitigation strategy against jamming in the Lightning Network.
Our solution combines unconditional fees and local reputation.
Small unconditional fees discourage quick jamming and compensate routing nodes for the damage.
Local reputation allows for prioritizing reliable peers and limits the amount of slots and liquidity the attacker can easily block.
We argue that our proposal can discourage jamming while scoring well with respect to security and privacy, user experience, incentive compatibility, and ease of implementation (see a [proof-of-concept](https://github.com/sr-gi/rust-lightning/commit/ce606) by Sergi Delgado Segura).
Finally, a solution to jamming may also be helpful in addressing other LN issues, such as balance probing and watchtower incentivization.
For more details, please refer to the [full paper](https://eprint.iacr.org/2022/1454).
