---
layout: page
title: Introduction to Bitcoin Research
order: 4
---

Hello, Researcher!

We appreciate your interest in Bitcoin. 

Bitcoin is a fascinating and multi-faceted topic.
It offers challenging questions across a variety of fields of study.
This page provides an overview of Bitcoin-related research.
It focuses on computer science (cryptography, privacy, networking) and economics, although Bitcoin can be viewed through the lens of other scientific disciplines too.

Bitcoin offers avenues for applied as well as fundamental research.
The former typically designs and evaluates proposed protocol upgrades planned for the next few years.
The latter tackles more long-term and fundamental challenges that Bitcoin faces.

Bitcoin development emphasizes security and stability.
Changes to the protocol pass strict review.
While moving academic results towards implementation may be a challenging task,
high-quality scientific contributions to Bitcoin will have a lasting impact.

We hope this page helps you choose your research direction.

The Bitcoin community looks forward to your contributions!


# Introduction

Let us start with introductory materials to get a general overview of the area.

The original whitepaper that introduced Bitcoin in 2008 defines its mission and the core design principles that still inform the development decisions:

* Nakamoto. [Bitcoin: A Peer-to-Peer Electronic Cash System](https://bitcoin.org/bitcoin.pdf)

Multiple systematization-of-knowledge papers provide an overview of Bitcoin:

* Narayanan and Clark. [Bitcoin's Academic Pedigree](https://queue.acm.org/detail.cfm?id=3136559)
* Bonneau et al. [SoK: Research Perspectives and Challenges for Bitcoin and Cryptocurrencies](https://www.ieee-security.org/TC/SP2015/papers-archived/6949a104.pdf)
* Tschorsch and Scheuermann. [Bitcoin and Beyond: A Technical Survey on Decentralized Digital Currencies](https://eprint.iacr.org/2015/464)
* Gudgeon et al. [SoK: Layer-Two Blockchain Protocols](https://eprint.iacr.org/2019/360)

Multiple books have been written on the subject, such as:

* Narayanan et al. [Bitcoin and Cryptocurrency Technologies](https://bitcoinbook.cs.princeton.edu/)
* Antonopoulos. [Mastering Bitcoin](https://aantonop.com/books/mastering-bitcoin/)
* Antonopoulos et al. [Mastering the Lightning Network](https://github.com/lnbook/lnbook)
* Rosenbaum. [Grokking Bitcoin](https://www.manning.com/books/grokking-bitcoin)

While it's not necessarily required to read those books cover to cover to start with Bitcoin research, they can be helpful as points of reference on Bitcoin's technical details.


# A path from research to development in Bitcoin

Bitcoin is guided by a [design philosophy](https://github.com/bitcoin-dev-philosophy/btcphilosophy) that puts a strong emphasis on decentralization and trustlessness.
As a consequence, Bitcoin is difficult to change.
Proposed modifications that break backwards compatibility (i.e., introduce a _hard fork_) are highly unlikely to be considered.
Changes to the protocol that introduce new functionality without forcing nodes to upgrade (_soft forks_) are possible but may take multiple years to be implemented.
Although second-layer protocols like Lightning are more dynamic, convincing their development communities to modify the protocol is also a non-trivial task.

Examples of research projects (also cited below under their respective subsections) that lead to changes to Bitcoin's codebase may include:

* [Erlay](https://arxiv.org/abs/1905.10518) -- a proposed modification to Bitcoin's P2P protocol that significantly decreases bandwidth usage -- is [being actively implemented](https://github.com/bitcoin/bitcoin/pull/21515) (as of late 2022).
* The [Erebus attack](https://erebus-attack.comp.nus.edu.sg/) that allows malicious Internet service providers to isolate Bitcoin nodes has motivated the development of [multiple countermeasures](https://erebus-attack-countermeasures.github.io/).
* Other eclipse-attack-related papers have lead to [multiple P2P improvements](https://github.com/bitcoin-core/bitcoin-devwiki/wiki/Addrman-and-eclipse-attacks).


# Research Areas in Bitcoin

This section lists some of the prior work related to Bitcoin in general.
The next section focused more specifically on second-layer protocols on top of Bitcoin, such as Lightning.[^1]

[^1]: We note that there is no single way to cluster prior work in this multi-dimensional research space. One may consider the desirable properties of Bitcoin as a whole (reliability, privacy, censorship resistance), the scientific discipline under which to study it (cryptography, networking, economics), or a particular aspect or layer of the technological stack (wallet design, key management, P2P protocol, second-layer protocols). On this page, each subsection contains papers on a topic that has attracted notable interest from researchers in the last years. Other classification methods are possible.


## Signature Schemes

Bitcoin spenders use digital signatures authorize their transactions.
ECDSA signatures have been used throughout Bitcoin's history.
A 2021 protocol upgrade added support for Schnorr signatures.

In Bitcoin, funds may be controlled by multiple keys.
Spending such coins requires multiple signatures (or a joint signature).
The corresponding private keys may be held by different parties (to distribute control) or locations (for increased reliability).
Designing secure protocols for collaborative signature construction is a non-trivial task.
It has attracted attention from researchers in the last years.
Schemes for multi-signatures (n-of-n) as well as threshold signatures (t-of-n) have been studied.

Relevant work includes:

* Nick et al. [MuSig2: Simple Two-Round Schnorr Multi-Signatures](https://eprint.iacr.org/2020/1261) proposes a practical multi-signature scheme for Schnorr signatures (related prior work includes [MuSig](https://eprint.iacr.org/2018/068) and [MuSig-DN](https://eprint.iacr.org/2020/1057)).
* Komlo and Goldberg. [FROST: Flexible Round-Optimized Schnorr Threshold Signatures](https://eprint.iacr.org/2020/852) proposes a threshold signature scheme for Schnorr signatures.
* Ruffing et al. [ROAST: Robust Asynchronous Schnorr Threshold Signatures](https://eprint.iacr.org/2022/550) adapts signature schemes like FROST to an asynchronous setting.


## P2P Network

Bitcoin uses a P2P network to broadcast transactions, blocks, and related data.
Inspired by earlier data sharing P2P protocols, Bitcoin operates under unique design constraints.
To allow public verifiability and establishing a level playing field, the network should ensure efficient information propagation even in low-bandwidth settings.
At the same time, it should defend against denial-of-service and privacy attacks.

Prior work on P2P networking in the context of Bitcoin includes:

* Apostolaki et al. [Hijacking Bitcoin: Routing Attacks on Cryptocurrencies](https://ieeexplore.ieee.org/document/7958588) describes attacks that abuse Internet routing protocols (BGP hijack) and allow for isolating a large portion of the Bitcoin network.
* Decker and Wattenhofer. [Information propagation in the Bitcoin network](https://ieeexplore.ieee.org/abstract/document/6688704) measures the speed and efficiency of propagating Bitcoin data among nodes (more recent data is [here](https://www.dsn.kastel.kit.edu/bitcoin/)).
* Dotan et al. [Survey on Cryptocurrency Networking: Context, State-of-the-Art, Challenges](https://arxiv.org/abs/2008.08412) presents the state of the art and current research challenges for networking for cryptocurrencies.
* Fanti et al. [Dandelion++: Lightweight Cryptocurrency Networking with Formal Anonymity Guarantees](https://arxiv.org/abs/1805.11060) proposes a new two-stage method for transaction propagation in Bitcoin aimed at increasing privacy.
* Heilman et al. [Eclipse Attacks on Bitcoin's Peer-to-Peer Network](https://www.usenix.org/conference/usenixsecurity15/technical-sessions/presentation/heilman) describes a method for an attacker controlling a sufficient number of IP addresses to control the victim's node view of the network, violating important security assumptions.
* Naumenko et al. [Erlay: Efficient Transaction Relay for Bitcoin](https://dl.acm.org/doi/10.1145/3319535.3354237) proposes a substantial efficiency improvement for transaction dissemination that uses set reconciliation.
* Neudecker and Hartenstein. [Network Layer Aspects of Permissionless Blockchains](https://ieeexplore.ieee.org/document/8456488) classify the requirements for cryptocurrency network protocols and review related attacks.
* Tran et al. [A Stealthier Partitioning Attack against Bitcoin Peer-to-Peer Network](https://erebus-attack.comp.nus.edu.sg/) presents the Erebus attack, which allows malicious Internet service providers to isolate public Bitcoin nodes from the network.

For a review of eclipse attacks and countermeasures against them, see [this document](https://github.com/bitcoin-core/bitcoin-devwiki/wiki/Addrman-and-eclipse-attacks) by Martin Zumsande.


## Privacy

Privacy is a vital property of Bitcoin.
Not only is privacy required to protect individual users from discrimination based on their financial behavior, it is also necessary to ensure fungibility (making any two units of a currency indistinguishable), which is a desirable property of money.
Yet, multiple privacy attacks on Bitcoin have been described.
Ensuring that Bitcoin preserves privacy while remaining permissionless and publicly verifiable is a challenging and important research task.

Privacy-related issues in Bitcoin may be broadly divided into two categories: P2P network analysis and transaction graph analysis.
Prior work related to analyzing P2P network traffic:

* Biryukov and Pustogarov. [Bitcoin over Tor isn't a good idea](https://arxiv.org/abs/1410.6079) describes an attack that abuses anti-DoS protection in Bitcoin, which allows for compromising privacy of Bitcoin users behind Tor.
* Biryukov et al. [Deanonymisation of clients in Bitcoin P2P network](https://arxiv.org/abs/1405.7418) proposes a method to cluster Bitcoin transactions based on their senders' sets of peers.
* Delgado-Segura et al. [TxProbe: Discovering Bitcoin's Network Topology Using Orphan Transactions](https://arxiv.org/abs/1812.00942) reconstructs the network topology of Bitcoin through peculiarities of transaction propagation.
* Fanti and Viswanath. [Anonymity Properties of the Bitcoin P2P Network](https://arxiv.org/abs/1703.08761) analyzes Bitcoin's anonymity properties in the context of a 2015 upgrade to its flooding mechanics.
* Koshy et al. [An Analysis of Anonymity in Bitcoin Using P2P Network Traffic](https://www.ifca.ai/fc14/papers/fc14_submission_71.pdf) shows a heuristic-based method of linking transactions to IP addresses they have been initially broadcast.
* Miller et al. [Discovering Bitcoin's Public Topology and Influential Nodes](https://www.cs.umd.edu/projects/coinscope/coinscope.pdf) discovers the network topology by using the way Bitcoin nodes store IP addresses.

A complementary approach to privacy attacks implies analyzing the transaction graph.
Such deanonymization methods and countermeasures have been described in:

* Androulaki et al. [Evaluating User Privacy in Bitcoin](https://fc13.ifca.ai/proc/1-3.pdf) evaluates Bitcoin's privacy and introduces basic heuristics for transaction graph analysis.
* Bonneau et al. [Mixcoin: Anonymity for Bitcoin with Accountable Mixes](https://eprint.iacr.org/2014/077) proposes a service to mix coins (thus entangling their history and improving privacy) while provably exposing the mixer's misbehavior if it occurs.
* Meiklejohn et al. [A Fistful of Bitcoins: Characterizing Payments Among Men with No Names](https://cseweb.ucsd.edu/~smeiklejohn/files/imc13.pdf) describes a heuristic-based deanonymization method and validates it by transacting with actual Bitcoin-based online services and marketplaces.
* Ruffing et al. [CoinShuffle: Practical Decentralized Coin Mixing for Bitcoin](https://petsymposium.org/2014/papers/Ruffing.pdf) improves upon prior mixer designs by eliminating third parties from the mixing protocol at the cost of a (small) communication overhead.


## Game Theory

Bitcoin's architecture has no central authority to coordinate the nodes' behavior, which makes game theory an important aspect of protocol design.
Research challenges in this area include formalizing the actions of the network participants, identifying undesired deviation strategies, and coming up with ways to mitigate them.
Notable papers that consider the game-theoretic properties of Bitcoin include:

* Babaioff et al. [On Bitcoin and Red Balloons](https://arxiv.org/abs/1111.2626) suggest a method to incentivize nodes for information propagation.
* Carlsten et al. [On the Instability of Bitcoin Without the Block Reward](https://dl.acm.org/doi/10.1145/2976749.2978408) analyzed the future of Bitcoin in the context of the programmatically diminishing block subsidy and its game-theoretic consequences.
* Courtois and Bahack. [On Subversive Miner Strategies and Block Withholding Attack in Bitcoin Digital Currency](https://arxiv.org/abs/1402.1718) analyze deviant miners' strategies and the related attacks.
* Eyal and Sirer. [Majority is not Enough: Bitcoin Mining is Vulnerable](https://arxiv.org/abs/1311.0243) introduces selfish mining - a strategy that allows a malicious miner to get more than its fair share of the block reward by strategically delaying block announcements.
* Garay et al. [The Bitcoin Backbone Protocol: Analysis and Applications](https://eprint.iacr.org/2014/765) formally describe the Bitcoin protocol and analyze it in the context of Byzantine agreement.
* Pass et al. [Analysis of the Blockchain Protocol in Asynchronous Networks](https://eprint.iacr.org/2016/454) analyzes Nakamoto consensus protocol in the asynchronous setting.
* Guo and Ren. [Bitcoin's Latency--Security Analysis Made Simple](https://arxiv.org/abs/2203.06357) develop the upper and lower bounds on the security of Nakamoto consensus.
* Kroll et al. [The Economics of Bitcoin Mining, or Bitcoin in the Presence of Adversaries](https://asset-pdf.scinapse.io/prod/2188530018/2188530018.pdf) analyzes the mining mechanics and discusses Bitcoin governance.


## Economics

Bitcoin can also be viewed from the economics perspective.
Papers on economic analysis of Bitcoin include:

* Budish. [The Economic Limits of Bitcoin and Anonymous, Decentralized Trust on the Blockchain](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4148014) analyzes the cost of maintaining the security in relation to its resilience against attacks.
* Böhme et al. [Bitcoin: Economics, Technology, and Governance](https://www.aeaweb.org/articles?id=10.1257/jep.29.2.213) offers an overview of Bitcoin's design principles for a nontechnical audience.
* Huberman et al. [Monopoly without a Monopolist: An Economic Analysis of the Bitcoin Payment System](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3025604) compares Bitcoin's decentralized design to traditional payment systems in the context of monopolistic prices.
* Kayal and Rohilla. [Bitcoin in the economics and finance literature: a survey](https://link.springer.com/article/10.1007/s43546-021-00090-5) provides a review of Bitcoin-related studies.



# Research Areas in Lightning and Second-Layer Protocols

This section introduces research directions related to protocols build on top of Bitcoin.
The most prominent of those is the Lightning Network (LN).
The LN is a payment channel network (PCN) that achieves low payment latency and high transactional throughput while accepting additional security assumptions.
Other second-layer (L2) protocols are also being developed on top of Bitcoin.
They generally implement additional functionality by moving most of the protocol logic off-chain and using the base layer only for dispute resolution.


## L2 Protocol Design

Developing functional L2 / PCN protocols remains a research challenge.
An important design goal is to require minimal or no changes to Bitcoin.

Relevant prior work includes:

* Poon and Dryja. [The Bitcoin Lightning Network: Scalable Off-Chain Instant Payments](https://lightning.network/lightning-network-paper.pdf) introduces Lightning.[^2]
* Aumayr et al. [Bitcoin-Compatible Virtual Channels](https://publik.tuwien.ac.at/files/publik_292507.pdf) adapts an alternative payment channel construction called _virtual_ channels to Bitcoin. Suggested future work
* Aumayr et al. [Blitz: Secure Multi-Hop Payments Without Two-Phase Commits](https://www.usenix.org/conference/usenixsecurity21/presentation/aumayr) proposes an improved payment channel protocol that only requires one round of communication (unlike the LN that requires two).

[^2]: See [modern LN protocol](https://github.com/lightning/bolts) for the up-to-date protocol specification.

**Game theory** of Lightning is a related research direction.
Similarly to Bitcoin, second-layer networks like Lightning are maintained by independent actors that are assumed to be rational.
However, the game theory of L2 protocols has its unique characteristics.
For instance, Lightning fees depend on the payment amount and not on the transaction size,[^3] as is the case in base-layer Bitcoin.
An important consideration for L2 protocol design is to avoid, or at least to minimize the adverse effects of centralization.
For example, Lightning nodes have tendency to prefer connecting to already well-connected nodes ("hubs"), increasing the network's dependence on them.
A research challenge is thereby: how do we ensure the protocol's security guarantees and permissionless access, even under a relatively centralized[^4] network topology?

Prior work on Lightning's economic aspects includes:

* Beres et al. [A Cryptoeconomic Traffic Analysis of Bitcoin's Lightning Network](https://arxiv.org/abs/1911.09432) simulates Lightning traffic based on a public network snapshot, estimates feasible fee revenues, and analyzes the network's economic viability as well as privacy.
* Guasoni et al. [Lightning Network Economics: Channels](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3840374) quantifies the cost of LN channels and the optimal conditions for two parties to open one.
* Lin et al. [Lightning network: a second path towards centralisation of the Bitcoin economy](https://iopscience.iop.org/article/10.1088/1367-2630/aba062/meta) analyzes the topological centralization of the Lightning network.

Formalizing and analyzing second-layer protocols remains an active area of research.

[^3]: More precisely, [_weight_](https://en.bitcoin.it/wiki/Weight_units).
[^4]: There are multiple metrics of topological centralization; evaluating their applicability for Lightning and similar networks is a separate research question.

Currently active development efforts include the following:

* **eltoo** is a new payment channel construction with a more efficient state replacement mechanism (relies on a yet-to-be-implemented [upgrade](https://bitcoinops.org/en/topics/sighash_anyprevout/) to Bitcoin). See: Decker et al. [eltoo: A Simple Layer2 Protocol for Bitcoin](https://diyhpl.us/~bryan/papers2/bitcoin/eltoo.pdf).
* **Point Time Locked Contracts (PTLC)** are a new type of multi-hop Schnorr-based channel locks improving channel privacy and efficiency. See: Malavolta et al. [Anonymous Multi-Hop Locks for Blockchain Scalability and Interoperability](https://eprint.iacr.org/2018/472). For a recent write-up, see: [Multi-Hop Locks from Scriptless Scripts](https://github.com/ElementsProject/scriptless-scripts/blob/master/md/multi-hop-locks.md).
* **Generic oracle-powered contracts** would allow parties to sign a contract whose resolution depends on the outcome of real-world events as reported by a trusted _oracle_. See: Le Guilly et al. [Bitcoin Oracle Contracts: Discreet Log Contracts in Practice](https://ieeexplore.ieee.org/abstract/document/9805512).

See also [LN Research Community](https://github.com/lnresearch) for LN datasets and inspection tools.

## Reliability and Security

Second-layer protocols rely on the availability of the base Bitcoin protocol.
Multiple papers have described attacks on the Lightning's dispute resolution mechanism and suggested mitigations:

* Harris and Zohar. [Flood & Loot: A Systemic Attack On The Lightning Network](https://arxiv.org/abs/2006.08513) describes an attack on LN by manipulating the pre-agreed on-chain fees for channel closure transactions.
* Mizrahi et al. [Congestion Attacks in Payment Channel Networks](https://arxiv.org/abs/2002.06564) evaluates the cost of channel _jamming_, that is, rendering channels useless by occupying all their payment slots with long-held in-flight payments.
* Riard and Naumenko. [Time-Dilation Attacks on the Lightning Network](https://arxiv.org/abs/2006.01418) explores the implications of eclipse attacks on Lightning and shows how a adversary who controls the victim's view of the Bitcoin network can steal LN funds.
* Rohrer et al. [Discharged Payment Channels: Quantifying the Lightning Network's Resilience to Topology-Based Attacks](https://arxiv.org/abs/1904.10253) derives the optimal attacker's strategies for channel exhaustion and node isolation in the view of the LN network topology.
* Tohner et al. [Hijacking Routes in Payment Channel Networks: A Predictability Tradeoff](https://arxiv.org/abs/1909.06890) describes an attack that involves attracting LN payments by advertising low fees and then denying service.
* Tsabary et al. [MAD-HTLC: Because HTLC is Crazy-Cheap to Attack](https://arxiv.org/abs/2006.12031) indicates a potential for miner bribery attacks in the current LN protocol and proposes a more game-theoretically robust construction for channel updates.

A Lightning user must monitor the Bitcoin blockchain and dispute potential fraud attempts.
This task can be delegated to a third-party service called a watchtower.
Multiple watchtower and payment channel schemes have been proposed:

* Avarikioti et al. [Cerberus Channels: Incentivizing Watchtowers for Bitcoin](https://eprint.iacr.org/2019/1092) proposes a Bitcoin-compatible payment channel construction with incentivized watchtowers.
* Avarikioti et al. [HIDE & SEEK: Privacy-Preserving Rebalancing on Payment Channel Networks](https://eprint.iacr.org/2021/1401) presents an opt-in rebalancing protocol that uses multi-party computation for privacy.
* Khabbazian et al. [Outpost: A Responsive Lightweight Watchtower](https://eprint.iacr.org/2019/986) suggests encoding justice transaction in Lightning opening and commitment transactions to reduce storage requirements for watchtowers.
* Mirzaei et al. [FPPW: A Fair and Privacy Preserving Watchtower For Bitcoin](https://eprint.iacr.org/2021/117) proposes a watchtower scheme for Bitcoin with fairness and balance privacy.

Modern research questions include the following:

* **Improving Lightning's UX.** Some of the current UX challenges stem from Lightning's inherent interactivity requirements. Nodes on the path must be online to forward a payment, in contrast to base-layer Bitcoin, which doesn't require the receiver to be online. Another UX hurdle comes from the fact that many payment fail on the first try. The sender has to try multiple routes, which takes time. The overarching US goal is to ensure a smooth payment experience comparable to traditional payment services while avoiding trusted third parties.
* **Liquidity management.** LN payment often fail because of lack of liquidity in some channel along the path. Routing nodes apply _liquidity management_ techniques such as _channel rebalancing_ to increase payment success rates. See: [Imbalance measure and proactive channel rebalancing algorithm for the Lightning Network](https://ieeexplore.ieee.org/abstract/document/9169456) by Pickhardt and Nowostawski.
* **Trustless watchtowers.** The security of LN channels relies on the assumption that both parties monitor the blockchain and dispute fraudulent channel closure if they happen. Users may delegate this task to a third-party service called a watchtower. A watchtower should be accountable (that is, get paid only if it does its job, and get punish if it doesn't), while revealing minimal details about the channel in question. A separate challenge is to enforce payments that were in-flight at the time of channel closure. See: [The Eye of Satoshi (rust-teos)](https://github.com/talaia-labs/rust-teos).
* **Interaction with the base layer.** Fundamentally, second-layer protocols rely on the base-layer blockchain for rule enforcement. However, it is unclear how to make such enforcement reliable. The fundamental challenge that requires further research and development is that congestion levels cannot be predicted in advance, enabling attack vectors like [transaction pinning](https://bitcoinops.org/en/topics/transaction-pinning/) (see also: [anchor outputs](https://bitcoinops.org/en/topics/anchor-outputs/)).
* **Addressing DoS vectors like jamming.** Jamming is a denial-of-service attack that involves initiating payments and delaying their finalization. Multiple approached to jamming countermeasures [have been discussed](https://blog.bitmex.com/preventing-channel-jamming/), including new [fee and reputation schemes](https://research.chaincode.com/2022/11/15/unjamming-lightning/).


## Routing

Lightning payments are forwarded along routes from the sender to the receiver.
The sender considers multiple factors when choosing the route, such as network topology, channel capacities, advertised fees, and outcomes of prior payment attempts.
An open research question is to design a routing algorithm for PCNs that is efficient, scalable, privacy-preserving, and does not lead to centralization.

Historical work on routing in PCNs includes:

* Sivaraman et al. [High Throughput Cryptocurrency Routing in Payment Channel Networks](https://arxiv.org/abs/1809.05088) suggests improved routing for PCNs with adaptive fees incentivizing rebalancing.
* Roos et al. [Settling Payments Fast and Private: Efficient Decentralized Routing for Path-Based Transactions](https://arxiv.org/abs/1709.05748) proposes embedding-based path discovery for PCNs.

A recent research result on the topic is:

* Pickhardt and Richter. [Optimally Reliable and Cheap Payment Flows on the Lightning Network](https://arxiv.org/abs/2107.05322) proposes an improved path-finding approach for the LN based on the success probabilities of payment attempts. This proposal has been implemented as [a Python package](https://github.com/renepickhardt/pickhardtpayments) and as [a plugin for LND](https://github.com/C-Otto/lnd-manageJ/blob/main/PickhardtPayments.md), a popular Lightning implementation.

An open research question is **developing a path selection algorithm** for Lightning with the following properties:

* Efficiency. Payments should have a high probability of success after a small number of attempted routes (ideally, they should succeed on the first try). The key obstacles are that channel balances are, in the general case, unknown to the sender, and that some nodes along the route may be offline.
* Being trustless. A user should not have to delegate path-finding to trusted third parties.
* Privacy. Route selection must not reveal the user's private information.
* Moderate resource usage. Route selection should be feasible on resource-constrained devices in terms of memory and processing power.


## Privacy

Second-layer protocols, including Lightning, present a novel set of privacy challenges.
The protocol should not reveal a user's balance, their position in the path, or even the existence of their channels, if they choose not to announce it.

The following papers analyze privacy challenges for Lightning:

* Kappos et al. [An Empirical Analysis of Privacy in the Lightning Network](https://arxiv.org/abs/2003.12470) describes multiple privacy attacks on the LN, including identifying unannounced channels and path discovery by an honest-but-curious routing node.
* Nisslmueller et al. [Toward Active and Passive Confidentiality Attacks On Cryptocurrency Off-Chain Networks](https://arxiv.org/abs/2003.00003) investigates two attacks on Lightning: channel balance probing and timing attacks.
* Romiti et al. [Cross-Layer Deanonymization Methods in the Lightning Protocol](https://arxiv.org/abs/2007.00764) investigates how the LN interacts with the base layer and what related heuristics may help an attacker to diminish LN users' privacy.

Ongoing development efforts related to privacy in Lightning include:

* **Cross-layer privacy.** It is easy to link LN channels with their on-chain footprint (in particular, the output, of the channel opening transaction). This allows for enriching existing on-chain address clustering data with LN information. At the same time, it is necessary to link channel announcements to some scarce resource to avoid denial-of-service attacks. One approach is requiring proofs of ownership of _some_ on-chain output without revealing which one it is.
* **Privacy-preserving route discovery.** Receivers in Lightning have to reveal their node identity to the sender. Techniques like [blinded paths](https://github.com/lightning/bolts/pull/765) aim to lift this requirement to ensure sender privacy. See also: [trampoline payments](https://bitcoinops.org/en/topics/trampoline-payments/). More generally, an adversary can make educated guesses regarding the route of a given payment by running the algorithm locally on a graph snapshot. Privacy leaks also occur through response timings, see: [Counting Down Thunder: Timing Attacks on Privacy in Payment Channel Networks](https://arxiv.org/abs/2006.12143) by Rohrer and Tschorsch. Designing a privacy-aware routing remains an open problem.
* **Preventing balance probing.** While channel balances are not announced, it is in most cases easy to estimate them based on payment failures. Nodes may perform probing to increase success rates of their own payments (as the uncertainty of channel balances is the leading cause of payment failure). Constant probing (i.e., sending payments that immediately fail) burdens the network. It remains an open problem to reconcile the need for payment reliability and privacy. See e.g.: Herrera-Joancomartí et al. [On the Difficulty of Hiding the Balance of Lightning Network Channels](https://eprint.iacr.org/2019/328) (the first paper to introduce channel balance probing).


# Further resources

Here we list some of the resources that Bitcoin development discussion centers around.

* [Bitcoin Optech](https://bitcoinops.org/) issues a newsletter explaining recent changes in Bitcoin-related open-source software and offers a glossary of Bitcoin technical topics.
* [Bitcoin-dev mailing list](https://lists.linuxfoundation.org/mailman/listinfo/bitcoin-dev) hosts current discussions about the development of Bitcoin. A separate list ([lightning-dev](https://lists.linuxfoundation.org/mailman/listinfo/lightning-dev)) exists for Lightning Network discussions.
* [Bitcoin Transcripts](https://btctranscripts.com/) hosts an archive of transcripts from Bitcoin-related conference talks.
* [Bitcoin StackExchange](https://bitcoin.stackexchange.com/) is a Bitcoin-focused Q&A website.
* [Bitcoin Problems](https://bitcoinproblems.org/) provides context for some of the Bitcoin- and Lightning-related research problems.
* [Bitcoin Core PR Review Club](https://bitcoincore.reviews/) is a weekly meeting to discuss a proposed change (a _pull request_, or PR for short) into Bitcoin Core.

Bitcoin-related technical conferences are another important discussion platform. Many publish videos of talks online. Examples include:

* [Scaling Bitcoin](https://scalingbitcoin.org/)
* [Breaking Bitcoin](https://breaking-bitcoin.com/)
* [Advancing Bitcoin](https://www.advancingbitcoin.com/)
