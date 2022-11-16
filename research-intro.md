---
layout: page
title: Introduction to Bitcoin Research
order: 4
---

Hello, Researcher!

We appreciate your interest in Bitcoin. 

Bitcoin is a fascinating and multi-faceted research topic.
It offers challenging questions across a variety of fields of study.
This page aims to provide an introduction to Bitcoin-related research directions.
We emphasize computer science (cryptography, privacy, networking) and economics, although Bitcoin can be viewed through the lens of other scientific disciplines too.

Bitcoin offers opportunities for applied as well as fundamental research.
The former typically designs and evaluates proposed protocol upgrades planned for the next few years.
The latter tackles more long-term and fundamental challenges that Bitcoin faces.

Bitcoin development emphasizes security and stability.
Changes to the protocol pass strict review.
Even though moving academic results towards implementation may be a challenging task,
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

Collections of materials compiled at Chaincode Labs with a stronger focus on development:

* [Chaincode's Bitcoin Curriculum](https://github.com/chaincodelabs/bitcoin-curriculum)
* [Chaincode's Lightning Curriculum](https://github.com/chaincodelabs/lightning-curriculum)



# Research Areas in Bitcoin

This section lists some of the prior work and research challenges related to the core Bitcoin protocol.


## Cryptography

The main cryptographic primitives Bitcoin uses are digital signatures and hash functions.
Most recently, research efforts have been put into implementing secure cryptographic schemes based on a new type of signatures (Schnorr signatures) that Bitcoin supports since 2021.

Relevant work on Bitcoin-related cryptography includes:

* Gennaro et al. [Threshold-optimal DSA/ECDSA signatures and an application to Bitcoin wallet security](https://eprint.iacr.org/2016/013)
* Komlo and Goldberg. [FROST: Flexible Round-Optimized Schnorr Threshold Signatures](https://eprint.iacr.org/2020/852)
* Ruffing et al. [ROAST: Robust Asynchronous Schnorr Threshold Signatures](https://eprint.iacr.org/2022/550)


## P2P Network

Bitcoin nodes broadcast transactions in the P2P network.
To allow public verifiability and establishing a level playing field for miners, information propagation should happen efficiently even in low-bandwidth settings, while protecting from network-based privacy attacks.

Prior work on P2P networking in the context of Bitcoin includes:

* Apostolaki et al. [Hijacking Bitcoin: Routing Attacks on Cryptocurrencies](https://ieeexplore.ieee.org/document/7958588)
* Decker and Wattenhofer. [Information propagation in the Bitcoin network](https://ieeexplore.ieee.org/abstract/document/6688704)
* Dotan et al. [Survey on Cryptocurrency Networking: Context, State-of-the-Art, Challenges](https://arxiv.org/abs/2008.08412)
* Fanti et al. [Dandelion++: Lightweight Cryptocurrency Networking with Formal Anonymity Guarantees](https://arxiv.org/abs/1805.11060)
* Heilman and Kendler. [Eclipse Attacks on Bitcoin’s Peer-to-Peer Network](https://www.usenix.org/conference/usenixsecurity15/technical-sessions/presentation/heilman)
* Naumenko et al. [Erlay: Efficient Transaction Relay for Bitcoin](https://dl.acm.org/doi/10.1145/3319535.3354237)
* Neudecker and Hartenstein. [Network Layer Aspects of Permissionless Blockchains](https://ieeexplore.ieee.org/document/8456488)

## Privacy

Privacy is a vital property of Bitcoin.
Still, multiple privacy attacks have been described in the literature.
The general research question is achieving a high level of privacy and fungibility the the P2P setting with the transaction data being public for verifiability.

One class of privacy attacks implies analyzing P2P network traffic.
Prior work in this area includes:

* Biryukov and Pustogarov. [Bitcoin over Tor isn't a good idea](https://arxiv.org/abs/1410.6079)
* Biryukov et al. [Deanonymisation of clients in Bitcoin P2P network](https://arxiv.org/abs/1405.7418)
* Fanti and Viswanath. [Anonymity Properties of the Bitcoin P2P Network](https://arxiv.org/abs/1703.08761)
* Koshy et al. [An Analysis of Anonymity in Bitcoin Using P2P Network Traffic](https://www.ifca.ai/fc14/papers/fc14_submission_71.pdf)

A complementary approach to attacking privacy involves transaction graph analysis.
Such deanonymization methods and countermeasures have been described in:

* Androulaki et al. [Evaluating User Privacy in Bitcoin](https://fc13.ifca.ai/proc/1-3.pdf)
* Bonneau et al. [Mixcoin: Anonymity for Bitcoin with Accountable Mixes](https://eprint.iacr.org/2014/077)
* Meiklejohn et al. [A Fistful of Bitcoins: Characterizing Payments Among Men with No Names](https://cseweb.ucsd.edu/~smeiklejohn/files/imc13.pdf)
* Reid and Harrigan. [An Analysis of Anonymity in the Bitcoin System](https://arxiv.org/abs/1107.4524)
* Ruffing et al. [CoinShuffle: Practical Decentralized Coin Mixing for Bitcoin](https://petsymposium.org/2014/papers/Ruffing.pdf)


## Game Theory

Bitcoin's core properties assume that network participants act in their best interest.
Research challenges in the area include formalizing the actions of the network participants, identifying undesired deviation strategies, and coming up with ways to mitigate those.
Notable papers that consider the game-theoretic properties of Bitcoin include:

* Babaioff et al. [On Bitcoin and Red Balloons](https://arxiv.org/abs/1111.2626)
* Carlsten et al. [On the Instability of Bitcoin Without the Block Reward](https://dl.acm.org/doi/10.1145/2976749.2978408)
* Courtois and Bahack. [On Subversive Miner Strategies and Block Withholding Attack in Bitcoin Digital Currency](https://arxiv.org/abs/1402.1718)
* Eyal and Sirer. [Majority is not Enough: Bitcoin Mining is Vulnerable](https://arxiv.org/abs/1311.0243) - the paper introduces _selfish mining_ attack where a malicious miner gets more than its fair share of block subsidy by strategically withholding or revealing blocks they mine.
* Garay et al. [The Bitcoin Backbone Protocol: Analysis and Applications](https://eprint.iacr.org/2014/765)
* Kroll et al. [The Economics of Bitcoin Mining, or Bitcoin in the Presence of Adversaries](https://asset-pdf.scinapse.io/prod/2188530018/2188530018.pdf)


## Economics

Bitcoin can also be viewed from the economics perspective.
Papers on economic analysis of Bitcoin include:

* Budish. [The Economic Limits of Bitcoin and Anonymous, Decentralized Trust on the Blockchain](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4148014)
* Böhme et al. [Bitcoin: Economics, Technology, and Governance](https://www.aeaweb.org/articles?id=10.1257/jep.29.2.213)
* Huberman et al. [Monopoly without a Monopolist: An Economic Analysis of the Bitcoin Payment System](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3025604)
* Kayal and Rohilla. [Bitcoin in the economics and finance literature: a survey](https://link.springer.com/article/10.1007/s43546-021-00090-5)



# Research Areas in Lightning

This section introduces research directions related to protocols build on top of Bitcoin -- most notably, Lightning.
The Lightning Network (LN) is a payment channel network on top of Bitcoin that achieves low payment latency and high transactional throughput while accepting additional security assumptions.
Other second-layer (L2) protocols are also being developed on top of Bitcoin.
They usually implement additional functionality by moving most of the protocol logic off-chain and using the base layer only for dispute resolution.

## Second-layer Protocol Design

Developing functional second-layer protocols that require minimal or no changes to Bitcoin remains a research challenge.

Relevant prior work includes:

* Aumayr et al. [Bitcoin-Compatible Virtual Channels](https://publik.tuwien.ac.at/files/publik_292507.pdf)
* Aumayr et al. [Blitz: Secure Multi-Hop Payments Without Two-Phase Commits](https://www.usenix.org/conference/usenixsecurity21/presentation/aumayr)
* Decker et al. [eltoo: A Simple Layer2 Protocol for Bitcoin](https://diyhpl.us/~bryan/papers2/bitcoin/eltoo.pdf)
* Jourenko et al. [Payment Trees: Low Collateral Payments for Payment Channel Networks](https://eprint.iacr.org/2020/1313)
* Le Guilly et al. [Bitcoin Oracle Contracts: Discreet Log Contracts in Practice](https://ieeexplore.ieee.org/abstract/document/9805512)
* Malavolta et al. [Anonymous Multi-Hop Locks for Blockchain Scalability and Interoperability](https://eprint.iacr.org/2018/472)
* Malavolta et al. [Concurrency and Privacy with Payment-Channel Networks](https://eprint.iacr.org/2017/820)


## Reliability and Security

Second-layer protocols rely on the availability of the base Bitcoin protocol.
In Lightning, for example, a user must monitor the Bitcoin blockchain and dispute potential fraud attempts within a given time window (or delegate this task to a third-party service).
Multiple papers have described issues with this mechanism and related mitigations:

* Harris and Zohar. [Flood & Loot: A Systemic Attack On The Lightning Network](https://arxiv.org/abs/2006.08513)
* Mizrahi et al. [Congestion Attacks in Payment Channel Networks](https://arxiv.org/abs/2002.06564)
* Riard and Naumenko. [Time-Dilation Attacks on the Lightning Network](https://arxiv.org/abs/2006.01418)
* Rohrer et al. [Discharged Payment Channels: Quantifying the Lightning Network's Resilience to Topology-Based Attacks](https://arxiv.org/abs/1904.10253)
* Tohner et al. [Hijacking Routes in Payment Channel Networks: A Predictability Tradeoff](https://arxiv.org/abs/1909.06890)
* Tsabary et al. [MAD-HTLC: Because HTLC is Crazy-Cheap to Attack](https://arxiv.org/abs/2006.12031)


## Routing

Lightning payments are forwarded along routes from the sender to the receiver.
The sender considers multiple factors when choosing the route, such as network topology, channel capacities, advertised fees, and outcomes of prior payment attempts.
An open research question is to design a routing algorithm for payment channel networks that is efficient, scalable, privacy-preserving, and does not lead to network centralization.

Prior work includes:

* Sivaraman et al. [High Throughput Cryptocurrency Routing in Payment Channel Networks](https://arxiv.org/abs/1809.05088)
* Roos et al. [Settling Payments Fast and Private: Efficient Decentralized Routing for Path-Based Transactions](https://arxiv.org/abs/1709.05748)
* Di Stasi et al. [Routing Payments on the Lightning Network](https://ieeexplore.ieee.org/abstract/document/8726489)
* Pickhardt and Richter. [Optimally Reliable and Cheap Payment Flows on the Lightning Network](https://arxiv.org/abs/2107.05322)


## Economics and Game Theory

Similarly to Bitcoin, second-layer networks like Lightning are maintained by independent actors that are assumed to be rational.
However, the game theory of L2 protocols has its unique characteristics.
For instance, fees in Lightning depend on payment amount and not on the size (more precisely, _weight_) of transactions, as is the case in base-layer Bitcoin.
Formalizing and analyzing such protocols remains an active area of research.

Prior work includes:

* Beres et al. [A Cryptoeconomic Traffic Analysis of Bitcoin's Lightning Network](https://arxiv.org/abs/1911.09432)
* Guasoni et al. [Lightning Network Economics: Channels](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3840374)
* Lin et al. [Lightning network: a second path towards centralisation of the Bitcoin economy](https://iopscience.iop.org/article/10.1088/1367-2630/aba062/meta)


## Privacy

Second-layer protocols, including Lightning, present a novel set of privacy challenges, many of which require further research, as exemplified by the following papers:

* Kappos et al. [An Empirical Analysis of Privacy in the Lightning Network](https://arxiv.org/abs/2003.12470)
* Nisslmueller et al. [Toward Active and Passive Confidentiality Attacks On Cryptocurrency Off-Chain Networks](https://arxiv.org/abs/2003.00003)
* Romiti et al. [Cross-Layer Deanonymization Methods in the Lightning Protocol](https://arxiv.org/abs/2007.00764)
* Herrera-Joancomartí et al. [On the Difficulty of Hiding the Balance of Lightning Network Channels](https://eprint.iacr.org/2019/328)

