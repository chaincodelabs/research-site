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

Books:

* Narayanan et al. [Bitcoin and Cryptocurrency Technologies](https://bitcoinbook.cs.princeton.edu/)
* Antonopoulos. [Mastering Bitcoin](https://aantonop.com/books/mastering-bitcoin/)
* Antonopoulos et al. [Mastering the Lightning Network](https://github.com/lnbook/lnbook)
* Rosenbaum. [Grokking Bitcoin](https://www.manning.com/books/grokking-bitcoin)

Introductory and systematization-of-knowledge papers:

* Nakamoto. [Bitcoin: A Peer-to-Peer Electronic Cash System](https://bitcoin.org/bitcoin.pdf)
* Narayanan and Clark. [Bitcoin's Academic Pedigree](https://queue.acm.org/detail.cfm?id=3136559)
* Bonneau et al. [SoK: Research Perspectives and Challenges for Bitcoin and Cryptocurrencies](https://www.ieee-security.org/TC/SP2015/papers-archived/6949a104.pdf)
* Tschorsch and Scheuermann. [Bitcoin and Beyond: A Technical Survey on Decentralized Digital Currencies](https://eprint.iacr.org/2015/464)
* Gudgeon et al. [SoK: Layer-Two Blockchain Protocols](https://eprint.iacr.org/2019/360)



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
* Aumayr et al. [Bitcoin-Compatible Virtual Channels](https://publik.tuwien.ac.at/files/publik_292507.pdf) adapts an alternative payment channel construction called _virtual_ channels to Bitcoin.
* Aumayr et al. [Blitz: Secure Multi-Hop Payments Without Two-Phase Commits](https://www.usenix.org/conference/usenixsecurity21/presentation/aumayr) proposes an improved payment channel protocol that only requires one round of communication (unlike the LN that requires two).
* Decker et al. [eltoo: A Simple Layer2 Protocol for Bitcoin](https://diyhpl.us/~bryan/papers2/bitcoin/eltoo.pdf) proposes a payment channel protocol with a more efficient state replacement mechanism (that relies on a yet-to-be-implemented [upgrade](https://bitcoinops.org/en/topics/sighash_anyprevout/) to Bitcoin).
* Le Guilly et al. [Bitcoin Oracle Contracts: Discreet Log Contracts in Practice](https://ieeexplore.ieee.org/abstract/document/9805512) proposes a way to establish Bitcoin _contracts_ whose resolution depends on the outcome of real-world events as reported by a trusted _oracle_.
* Malavolta et al. [Anonymous Multi-Hop Locks for Blockchain Scalability and Interoperability](https://eprint.iacr.org/2018/472) defines a novel multi-hop lock construction for privacy-preserving payment channel-networks.

[^2]: See [modern LN protocol](https://github.com/lightning/bolts) for the up-to-date protocol specification.


## Reliability and Security

Second-layer protocols rely on the availability of the base Bitcoin protocol.
In Lightning, for example, a user must monitor the Bitcoin blockchain and dispute potential fraud attempts.[^3]

[^3]: A user can delegate this task to a third-party service called a watchtower.

Multiple papers have described attacks on this mechanism and suggested mitigations:

* Harris and Zohar. [Flood & Loot: A Systemic Attack On The Lightning Network](https://arxiv.org/abs/2006.08513) describes an attack on LN by manipulating the pre-agreed on-chain fees for channel closure transactions.
* Mizrahi et al. [Congestion Attacks in Payment Channel Networks](https://arxiv.org/abs/2002.06564) evaluates the cost of channel _jamming_, that is, rendering channels useless by occupying all their payment slots with long-held in-flight payments.
* Riard and Naumenko. [Time-Dilation Attacks on the Lightning Network](https://arxiv.org/abs/2006.01418) explores the implications of eclipse attacks on Lightning and shows how a adversary who controls the victim's view of the Bitcoin network can steal LN funds.
* Rohrer et al. [Discharged Payment Channels: Quantifying the Lightning Network's Resilience to Topology-Based Attacks](https://arxiv.org/abs/1904.10253) derives the optimal attacker's strategies for channel exhaustion and node isolation in the view of the LN network topology.
* Tohner et al. [Hijacking Routes in Payment Channel Networks: A Predictability Tradeoff](https://arxiv.org/abs/1909.06890) describes an attack that involves attracting LN payments by advertising low fees and then denying service.
* Tsabary et al. [MAD-HTLC: Because HTLC is Crazy-Cheap to Attack](https://arxiv.org/abs/2006.12031) indicates a potential for miner bribery attacks in the current LN protocol and proposes a more game-theoretically robust construction for channel updates.


## Routing

Lightning payments are forwarded along routes from the sender to the receiver.
The sender considers multiple factors when choosing the route, such as network topology, channel capacities, advertised fees, and outcomes of prior payment attempts.
An open research question is to design a routing algorithm for PCNs that is efficient, scalable, privacy-preserving, and does not lead to centralization.

Prior work includes:

* Sivaraman et al. [High Throughput Cryptocurrency Routing in Payment Channel Networks](https://arxiv.org/abs/1809.05088) suggests improved routing for PCNs with adaptive fees incentivizing rebalancing.
* Roos et al. [Settling Payments Fast and Private: Efficient Decentralized Routing for Path-Based Transactions](https://arxiv.org/abs/1709.05748) proposes embedding-based path discovery for PCNs.
* Pickhardt and Richter. [Optimally Reliable and Cheap Payment Flows on the Lightning Network](https://arxiv.org/abs/2107.05322) proposes an improved path-finding approach for the LN based on the success probabilities of payment attempts.


## Economics and Game Theory

Similarly to Bitcoin, second-layer networks like Lightning are maintained by independent actors that are assumed to be rational.
However, the game theory of L2 protocols has its unique characteristics.
For instance, Lightning fees depend on the payment amount and not on the transaction size,[^4] as is the case in base-layer Bitcoin.
Formalizing and analyzing such protocols remains an active area of research.

[^4]: More precisely, [_weight_](https://en.bitcoin.it/wiki/Weight_units).

Prior work includes:

* Beres et al. [A Cryptoeconomic Traffic Analysis of Bitcoin's Lightning Network](https://arxiv.org/abs/1911.09432) simulates Lightning traffic based on a public network snapshot, estimates feasible fee revenues, and analyzes the network's economic viability as well as privacy.
* Guasoni et al. [Lightning Network Economics: Channels](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3840374) quantifies the cost of LN channels and the optimal conditions for two parties to open one.
* Lin et al. [Lightning network: a second path towards centralisation of the Bitcoin economy](https://iopscience.iop.org/article/10.1088/1367-2630/aba062/meta) analyzes the topological centralization of the Lightning network.


## Privacy

Second-layer protocols, including Lightning, present a novel set of privacy challenges.
The protocol should not reveal a user's balance, their position in the path, or even the existence of their channels, if they choose not to announce it.
Further research is needed to achieve these goals, as shown by the following papers:

* Kappos et al. [An Empirical Analysis of Privacy in the Lightning Network](https://arxiv.org/abs/2003.12470) describes multiple privacy attacks on the LN, including identifying unannounced channels and path discovery by an honest-but-curious routing node.
* Nisslmueller et al. [Toward Active and Passive Confidentiality Attacks On Cryptocurrency Off-Chain Networks](https://arxiv.org/abs/2003.00003) investigates two attacks on Lightning: channel balance probing and timing attacks.
* Romiti et al. [Cross-Layer Deanonymization Methods in the Lightning Protocol](https://arxiv.org/abs/2007.00764) investigates how the LN interacts with the base layer and what related heuristics may help an attacker to diminish LN users' privacy.
* Herrera-Joancomartí et al. [On the Difficulty of Hiding the Balance of Lightning Network Channels](https://eprint.iacr.org/2019/328) is the first paper to introduce channel balance probing - an attack that allows for estimating the balance in a remote channel by sending fake payments through it.

