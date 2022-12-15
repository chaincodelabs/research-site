---
layout: page
title: Introduction to Bitcoin Research
order: 4
---

Hello, Researcher!

Thank you for your interest in Bitcoin.
This page provides an overview of Bitcoin-related research.
We hope it helps you choose your research direction.

The Bitcoin community looks forward to your contributions!

1. [From Research to Development](#from-research-to-development)
2. [Introductory Materials](#introductory-materials)
3. [Research Areas in Bitcoin](#research-areas-in-bitcoin)
4. [Research Areas in Second-Layer Protocols](#research-areas-in-second-layer-protocols)


# From Research to Development

Bitcoin is a fascinating and multi-faceted topic that offers challenging questions across a variety of fields of study.
To make sure research results are applicable, it is important to keep in mind how the Bitcoin development process is structured.

Bitcoin must operate in an adversarial environment while remaining permissionless.
Its [design philosophy](https://github.com/bitcoin-dev-philosophy/btcphilosophy) emphasizes security and decentralization.
Therefore, Bitcoin development is conservative, and the protocol is difficult to change.
This is especially true for consensus-critical code in [Bitcoin Core](https://github.com/bitcoin/bitcoin).
Other aspects of the Bitcoin Core codebase, such as P2P networking, are more open to change.
The same applies to complementary protocols of the Bitcoin stack, such as the Lightning Network.

Bringing a research result to implementation is a challenging task.
It is recommended to share research ideas with developers,
as well as to become familiar with ongoing discussions in the community.
The following resources might be helpful:

* [Bitcoin Optech](https://bitcoinops.org/) issues a newsletter explaining recent changes in Bitcoin-related open-source software and offers a glossary of Bitcoin technical topics.
* [Bitcoin-dev](https://lists.linuxfoundation.org/mailman/listinfo/bitcoin-dev) and [Lightning-dev](https://lists.linuxfoundation.org/mailman/listinfo/lightning-dev) mailing lists host discussions about the development of Bitcoin and the Lightning Network, respectively.
* [Bitcoin Transcripts](https://btctranscripts.com/) is an archive of transcripts from Bitcoin-related talks.
* [Bitcoin StackExchange](https://bitcoin.stackexchange.com/) is a Bitcoin-focused Q&A website.
* [Bitcoin Problems](https://bitcoinproblems.org/) provides context for some of the Bitcoin- and Lightning-related research problems.
* [Bitcoin Core PR Review Club](https://bitcoincore.reviews/) is a weekly meeting to discuss a proposed change (a _pull request_, or PR) into Bitcoin Core.

Many Bitcoin-related technical conferences publish videos of talks online. Examples include:

* [Scaling Bitcoin](https://scalingbitcoin.org/)
* [Breaking Bitcoin](https://breaking-bitcoin.com/)
* [Advancing Bitcoin](https://www.advancingbitcoin.com/)
* [The Atlanta Bitcoin Conference (TABConf)](https://tabconf.com/)

Examples of research projects (also cited below under their respective subsections) have lead to changes in Bitcoin include the [Erebus attack](https://erebus-attack.comp.nus.edu.sg/), other P2P-related issues that have informed [various improvements](https://github.com/bitcoin-core/bitcoin-devwiki/wiki/Addrman-and-eclipse-attacks), and [Erlay](https://arxiv.org/abs/1905.10518) ([implementation in progress](https://github.com/bitcoin/bitcoin/pull/21515) as of late 2022).


# Introductory Materials

The Bitcoin whitepaper (2008) defines its mission and core design principles:

* Nakamoto. [Bitcoin: A Peer-to-Peer Electronic Cash System](https://bitcoin.org/bitcoin.pdf)

Multiple systematization-of-knowledge papers provide an overview of Bitcoin:

* Narayanan and Clark. [Bitcoin's Academic Pedigree](https://queue.acm.org/detail.cfm?id=3136559)
* Bonneau et al. [SoK: Research Perspectives and Challenges for Bitcoin and Cryptocurrencies](https://www.ieee-security.org/TC/SP2015/papers-archived/6949a104.pdf)
* Tschorsch and Scheuermann. [Bitcoin and Beyond: A Technical Survey on Decentralized Digital Currencies](https://eprint.iacr.org/2015/464)
* Gudgeon et al. [SoK: Layer-Two Blockchain Protocols](https://eprint.iacr.org/2019/360)

Books on the subject include:

* Narayanan et al. [Bitcoin and Cryptocurrency Technologies](https://bitcoinbook.cs.princeton.edu/)
* Antonopoulos. [Mastering Bitcoin](https://aantonop.com/books/mastering-bitcoin/)
* Antonopoulos et al. [Mastering the Lightning Network](https://github.com/lnbook/lnbook)
* Rosenbaum. [Grokking Bitcoin](https://www.manning.com/books/grokking-bitcoin)

While it's not strictly required to fully read those books before starting Bitcoin research, they can be helpful as points of reference.



# Research Areas in Bitcoin

This section lists prior work related to Bitcoin in general.
The next section focuses more specifically on Bitcoin-based second-layer protocols, such as the Lightning Network.[^1]

[^1]: There are multiple ways to classify research questions and prior work in this multi-dimensional space. One may consider the desirable properties of Bitcoin (reliability, privacy, censorship resistance), the scientific discipline under which to study it (cryptography, networking, economics), or a particular aspect or layer of the technological stack (key management, P2P networking, second-layer protocols).


## Cryptography

Bitcoin uses multiple cryptographic primitives.
Most relevant for the current research efforts are signatures and encryption.
Ongoing research efforts are as follows.

* **Schnorr-based multi-signatures and threshold signatures.**
Signatures are used to authorize transactions.
Two signature algorithms are available: ECDSA and Schnorr signatures.
ECDSA has been used throughout Bitcoin's history.
Support for Schnorr signatures, which offer privacy and scalability benefits (see [BIP340](https://github.com/bitcoin/bips/blob/master/bip-0340.mediawiki)), has been added in 2021.
In Bitcoin, funds may be controlled by multiple keys.
Spending such coins requires collaborative signature construction, which is a non-trivial task.
Schemes for multi-signatures (n-of-n) as well as threshold signatures (t-of-n) have been designed.
The question of how to **design secure Schnorr-based signature protocols** remains an active area of research.
* **Encryption in the P2P network.**
Currently, connections in the Bitcoin P2P network are unencrypted.
This allows a network adversary to analyze metadata, tamper with connections, and easily detect the fact that Bitcoin protocol is being used.
[BIP-324](https://bip324.com/) addresses these concerns by adding encryption support.

Prior work includes:

* Nick et al. [MuSig2: Simple Two-Round Schnorr Multi-Signatures](https://eprint.iacr.org/2020/1261) proposes a practical multi-signature scheme for Schnorr signatures (related prior work includes [MuSig](https://eprint.iacr.org/2018/068) and [MuSig-DN](https://eprint.iacr.org/2020/1057)).
* Komlo and Goldberg. [FROST: Flexible Round-Optimized Schnorr Threshold Signatures](https://eprint.iacr.org/2020/852) proposes a threshold signature scheme for Schnorr signatures.
* Ruffing et al. [ROAST: Robust Asynchronous Schnorr Threshold Signatures](https://eprint.iacr.org/2022/550) adapts signature schemes like FROST to an asynchronous setting. Potential future improvements listed in the paper include preprocessing the first round of presignature shares, signing a continuous stream of messages, scoring signers, and trading off for latency. 


## P2P Network

Bitcoin uses a P2P network to broadcast transactions, blocks, and related data.
Inspired by earlier data sharing P2P protocols, Bitcoin operates under unique design constraints.
To allow public verifiability and establish a level playing field for miners, the network should ensure efficient information propagation even in low-bandwidth settings.
At the same time, it should defend against denial-of-service and privacy attacks.
The paper [Survey on Cryptocurrency Networking: Context, State-of-the-Art, Challenges](https://arxiv.org/abs/2008.08412) by Dotan et al. presents the state of the art and open problems in cryptocurrency networking.

Bitcoin's P2P protocol should have the following properties:

* **Efficiency.** Data should propagate quickly to facilitate consensus and avoid providing an unfair advantage to better-connected nodes. The requirements differ for different message types. Blocks should propagate as quickly as possible; transaction should reach _miners_ quickly, while there isn't that much urgency in propagating IP addresses of peers.
* **Security.** Bitcoin peers should minimize trust towards their peers and independently verify the data they receive. At the same time, the protocol should discourage denial-of-service attacks. This is challenging in an open network with no fixed identities. **Preventing eclipse attacks**, where an adversary sets up multiple nodes to fully control the flow of data between a victim node and the rest of the network, is especially important. For a review of eclipse attacks and countermeasures against them, see [this document](https://github.com/bitcoin-core/bitcoin-devwiki/wiki/Addrman-and-eclipse-attacks) by Adam Jonas et al.
* **Privacy.** Bitcoin nodes should avoid leaking private information in their P2P communication patterns. In particular, an adversary shouldn't be able to determine which node a given transaction originates from. Similarly, network topology should also remain hidden: it must be difficult to figure out whether two nodes are connected. Ideally, even the fact that someone is communicating via the Bitcoin P2P protocol should remain hidden from a network observer.

Bitcoin miners normally work in _pools_ to receive a consistent income stream.
Communication between miners and pool operators is performed using the [Stratum protocol](https://braiins.com/stratum-v1/docs).
An improved protocol called [Stratum V2](https://stratumprotocol.org/) is under development.
Its advantages include encryption (to prevent man-in-the-middle attacks), lower bandwidth consumption, and the ability for miners to construct their own block templates (to foster decentralization).

Open questions for Bitcoin P2P include:

* What should be the desired properties of the P2P protocol? How to formalize them?
* What node policies ensure quality and diversity of peers? How often should nodes rotate peers?
* What principles should underpin the gossip protocol? How often and to whom should nodes advertise their IP addresses?

Prior work includes:

* Apostolaki et al. [Hijacking Bitcoin: Routing Attacks on Cryptocurrencies](https://ieeexplore.ieee.org/document/7958588) describes attacks that abuse Internet routing protocols (BGP hijack) and allow for isolating a large portion of the Bitcoin network. Suggested countermeasures are AS-aware peer selection (implemented) and traffic encryption (implementation in progress, see [BIP-324](https://bip324.com/)).
* Decker and Wattenhofer. [Information propagation in the Bitcoin network](https://ieeexplore.ieee.org/abstract/document/6688704) measures the speed and efficiency of propagating Bitcoin data among nodes (more recent data is [here](https://www.dsn.kastel.kit.edu/bitcoin/)).
* Fanti et al. [Dandelion++: Lightweight Cryptocurrency Networking with Formal Anonymity Guarantees](https://arxiv.org/abs/1805.11060) proposes a two-stage transaction propagation method for stronger privacy. The protocol hasn't yet been implemented in Bitcoin due to concerns over denial-of-service attacks.
* Heilman et al. [Eclipse Attacks on Bitcoin's Peer-to-Peer Network](https://www.usenix.org/conference/usenixsecurity15/technical-sessions/presentation/heilman) describes a method for an attacker controlling a sufficient number of IP addresses to control the victim's node view of the network. These concerns have motivated changes in the P2P protocol to ensure peer diversity.
* Naumenko et al. [Erlay: Efficient Transaction Relay for Bitcoin](https://dl.acm.org/doi/10.1145/3319535.3354237) proposes a substantial efficiency improvement for transaction dissemination based on set reconciliation (under active development).
* Neudecker and Hartenstein. [Network Layer Aspects of Permissionless Blockchains](https://ieeexplore.ieee.org/document/8456488) classifies the requirements for cryptocurrency network protocols and reviews related attacks.
* Tran et al. [A Stealthier Partitioning Attack against Bitcoin Peer-to-Peer Network](https://erebus-attack.comp.nus.edu.sg/) presents the Erebus attack, which allows malicious Internet service providers to isolate public Bitcoin nodes. The concern has been partly addressed by establishing more outgoing connections and incorporating autonomous systems (AS) topology in peer selection.


## Privacy

Privacy is a critical aspect of Bitcoin.
First, privacy is required to protect users from discrimination based on their behavior.
Second, privacy is necessary to ensure fungibility (making any two currency units indistinguishable).
Ensuring privacy in Bitcoin, while preserving its permissionless nature, is a challenging and important research task.
The fundamental challenge is to ensure privacy while preserving public verifiability of all transactions.
The [Bitcoin Wiki Privacy page](https://en.bitcoin.it/wiki/Privacy) provides an overview of privacy issues.

Privacy-related attacks may be divided into P2P network analysis and transaction graph analysis.

Prior work related to analyzing P2P network traffic:

* Biryukov and Pustogarov. [Bitcoin over Tor isn't a good idea](https://arxiv.org/abs/1410.6079) describes an attack that abuses anti-DoS protection in Bitcoin, allowing for compromising privacy of Bitcoin users behind Tor.
* Biryukov et al. [Deanonymisation of clients in Bitcoin P2P network](https://arxiv.org/abs/1405.7418) proposes a method to cluster Bitcoin transactions based on their senders' sets of peers.
* Delgado-Segura et al. [TxProbe: Discovering Bitcoin's Network Topology Using Orphan Transactions](https://arxiv.org/abs/1812.00942) reconstructs the network topology of Bitcoin through peculiarities of transaction propagation.
* Fanti and Viswanath. [Anonymity Properties of the Bitcoin P2P Network](https://arxiv.org/abs/1703.08761) analyzes an upgrade to Bitcoin's transaction propagation mechanics (_trickling_ and _diffusion_) and concludes that neither method provides good anonymity.
* Fleder et al. [Bitcoin Transaction Graph Analysis](https://arxiv.org/abs/1502.01657) deanonymizes Bitcoin transactions by combining blockchain data with publicly available sources like web forums.
* Koshy et al. [An Analysis of Anonymity in Bitcoin Using P2P Network Traffic](https://www.ifca.ai/fc14/papers/fc14_submission_71.pdf) shows a heuristic-based method of linking transactions to the IP addresses they originated from.
* Miller et al. [Discovering Bitcoin's Public Topology and Influential Nodes](https://www.cs.umd.edu/projects/coinscope/coinscope.pdf) discovers the network topology by using the way Bitcoin nodes store IP addresses.

See also: [Bitcoin Monitoring](https://www.dsn.kastel.kit.edu/bitcoin/) page (KASTEL Institute / Karlsruhe Institute of Technology) that provides longitudinal data on Bitcoin P2P network behavior and links to related research papers.

Analyzing the transaction graph is another approach to privacy attacks.
One possible countermeasure is _mixing_, that is, creating collaborative transactions that make it difficult to track coin history.
Implementing secure and user-friendly mixing protocol without a trusted third party remains a challenge (see e.g. Ghesmati et al. [Usability of Cryptocurrency Wallets Providing
CoinJoin Transactions](https://eprint.iacr.org/2022/285)).
Apart from sender-receiver topology, transactions may be fingerprinted based on wallet-specific properties, such as the order of inputs and amount patterns.
Graph-based deanonymization methods and countermeasures have been described in:

* Androulaki et al. [Evaluating User Privacy in Bitcoin](https://fc13.ifca.ai/proc/1-3.pdf) introduces basic heuristics for transaction graph analysis.
* Bonneau et al. [Mixcoin: Anonymity for Bitcoin with Accountable Mixes](https://eprint.iacr.org/2014/077) proposes a mixing service that provably exposes the mixer's misbehavior.
* Meiklejohn et al. [A Fistful of Bitcoins: Characterizing Payments Among Men with No Names](https://cseweb.ucsd.edu/~smeiklejohn/files/imc13.pdf) describes a heuristic-based deanonymization method and validates it by transacting with actual Bitcoin-based online marketplaces.
* Ruffing et al. [CoinShuffle: Practical Decentralized Coin Mixing for Bitcoin](https://petsymposium.org/2014/papers/Ruffing.pdf) improves upon prior mixer designs by eliminating third parties from the mixing protocol at the cost of a (small) communication overhead.

Open research questions include:

* How to develop secure privacy tools for Bitcoin? How to make them appealing to regular users?
* How to coordinate coin mixing without a designated coordinator? If the coordinator is present, how to limit its influence? How to make the coordinator accountable for misbehavior?
* How can we use Taproot and Schnorr signatures to improve Bitcoin base-layer privacy?


## Game Theory

No central authority coordinates the behavior of Bitcoin nodes.
This makes game theory an important aspect of protocol design.
In particular, miners must be incentivized to produce blocks and, ideally, should be rewarded proportionally to their contribution to Bitcoin's total hashpower.
Moreover, miners usually form pools to share the block rewards and ensure a predictable revenue stream.
The relationships between miners and pools can also be thought of as a game.
Research challenges in this area include formalizing the actions of the network participants, identifying undesired deviation strategies, and coming up with ways to mitigate them.

Research questions might include:

* **Bitcoin's long-term sustainability.** Will Bitcoin be economically sustainable in light of the reduction of block subsidies (that is, if miners are primarily incentivized by transaction fees)?
* **Deviant miner strategies.** Can miners gain more than their fair share of block rewards by deviating from the protocol in some way?
* **Mining pools.** What is the power dynamics between miners and pools? How to ensure that rewards are fairly shared among miners? Is it possible to design a decentralized mining pool?

Notable papers that consider the game-theoretic properties of Bitcoin include:

* Babaioff et al. [On Bitcoin and Red Balloons](https://arxiv.org/abs/1111.2626) suggests a method to incentivize information propagation among nodes.
* Carlsten et al. [On the Instability of Bitcoin Without the Block Reward](https://dl.acm.org/doi/10.1145/2976749.2978408) analyzes the future of Bitcoin in the context of the programmatically diminishing block subsidy and its game-theoretic consequences.
* Courtois and Bahack. [On Subversive Miner Strategies and Block Withholding Attack in Bitcoin Digital Currency](https://arxiv.org/abs/1402.1718) analyzes deviant miners' strategies and the related attacks.
* Eyal and Sirer. [Majority is not Enough: Bitcoin Mining is Vulnerable](https://arxiv.org/abs/1311.0243) introduces selfish mining -- a strategy that allows a malicious miner to get more than its fair share of the block reward by strategically delaying block announcements.
* Garay et al. [The Bitcoin Backbone Protocol: Analysis and Applications](https://eprint.iacr.org/2014/765) formally describes the Bitcoin protocol and analyzes it in the context of Byzantine agreement.
* Pass et al. [Analysis of the Blockchain Protocol in Asynchronous Networks](https://eprint.iacr.org/2016/454) proves that Nakamoto consensus protocol satisfies consistency in an asynchronous setting.
* Guo and Ren. [Bitcoin's Latency--Security Analysis Made Simple](https://arxiv.org/abs/2203.06357) develops the upper and lower bounds on the security of Nakamoto consensus.


## Economics

Bitcoin can also be viewed from the economics perspective.
Clearly, bitcoins are exchanged for fiat currencies and other cryptocurrencies.
The properties of those markets might be analyzed (see e.g. Hale et al. [How Futures Trading Changed Bitcoin Prices](https://www.frbsf.org/economic-research/wp-content/uploads/sites/4/el2018-12.pdf)).
Moreover, actors in the Bitcoin protocol itself are part of a market for _block space_.

Bitcoin transactions must be included in a block to be confirmed.
A block can only include a limited number of transactions, hence, block space is a scarce resource.
Transaction senders bid for block space by attaching fees to transactions they broadcast.
This mechanism establishes the block space market, which presents an active area of research.

Open questions include:

* **Fee strategies.** When constructing transactions, wallets face a trade-off between getting a transaction promptly confirmed vs overpaying in fees. An unconfirmed transaction may be _replaced_ ([replace-by-fee, or RBF](https://bitcoinops.org/en/topics/replace-by-fee/)). Miners are interested in including the highest-paying transaction in their blocks. What is the optimal replacement strategy for a wallet, and how does it affect the overall dynamics of the block space market? 
* **Coin selection and UTXO management**. A Bitcoin transaction spends one or multiple _unspent transaction outputs_ (UTXOs) and creates new UTXOs. How should wallets select UTXOs for a new transaction? (This problem is known as [Coin selection](https://bitcoinops.org/en/topics/coin-selection/); see also [An Evaluation of Coin Selection Strategies](https://murch.one/erhardt2016coinselection.pdf) by Mark Erhardt.) Under what conditions is it worth it to consolidate small UTXOs? (This is especially relevant for high-volume wallets.) What are the privacy implications of coin selection and consolidation strategies?
* **Block building.** On the other side of the block space market are the miners who collect unconfirmed transaction into blocks in exchange for block subsidy and fees. Generally speaking, block building is an instance of the knapsack problem with dependencies (a transaction may spend an output of another unconfirmed transaction, therefore, it will only be included in a block if its parent is included). For Bitcoin miners, time is of essence: every second spent on block template construction leads to lost revenue. There are many Bitcoin-specific considerations to this process (see e.g. [Improvement on the current block building algorithm](https://gist.github.com/Xekyo/5cb413fe9f26dbce57abfd344ebbfaf2#file-candidate-set-based-block-building-md) by Mark Erhardt and Clara Shikhelman). The question is therefore: how to construct an block building algorithm that reliably produces good enough solutions quickly?
* **Mining economics.** Mining is a complex economic phenomenon. What factors influence miners' behavior? Under what conditions is mining profitable? (See [The Economics of Bitcoin Mining, or Bitcoin in the Presence of Adversaries](https://asset-pdf.scinapse.io/prod/2188530018/2188530018.pdf) by Kroll et al.)
* **Bitcoin's wider economic impact.** How does Bitcoin adoption influence the global economy? What role does it play in the remittance market? What are the effects of adopting Bitcoin as legal tender (as done in El Salvador)? How does Bitcoin mining impact the energy markets? (See e.g. Badea and Mungiu-Pupӑzan. [The Economic and Environmental Impact of Bitcoin](https://ieeexplore.ieee.org/abstract/document/9385063).)

Papers on economic analysis of Bitcoin include:

* Budish. [The Economic Limits of Bitcoin and Anonymous, Decentralized Trust on the Blockchain](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4148014) analyzes the cost of maintaining the security in relation to its resilience against attacks.
* Böhme et al. [Bitcoin: Economics, Technology, and Governance](https://www.aeaweb.org/articles?id=10.1257/jep.29.2.213) offers an overview of Bitcoin's design principles for a nontechnical audience.
* Huberman et al. [Monopoly without a Monopolist: An Economic Analysis of the Bitcoin Payment System](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3025604) compares Bitcoin's decentralized design to traditional payment systems in the context of monopolistic prices and suggests automatically adjusting capacity based on transaction volume.
* Kayal and Rohilla. [Bitcoin in the economics and finance literature: a survey](https://link.springer.com/article/10.1007/s43546-021-00090-5) provides a review of Bitcoin-related studies.
* Moroz et al. [Double-spend counterattacks: Threat of retaliation in proof-of-work systems](https://arxiv.org/abs/2002.10736) formalizes a defense to double-spend attacks and shows that the threat of a counterattack leads to an equilibrium in which no attack happens.


## User Experience (UX)

Bitcoin aims to become universally accepted money, yet it introduces a number of novel concepts that may be hard for the general public to grasp.
An important task for developers is to make Bitcoin approachable.
Which aspects of the protocol should be hidden from the user, and how to present those that are not?

Prior work includes:

* Albayati et al. [A study on the use of cryptocurrency wallets from a user experience perspective](https://onlinelibrary.wiley.com/doi/abs/10.1002/hbe2.313) examines the factors impacting the utilization of cryptocurrency wallets.
* Krombholz et al. [The Other Side of the Coin: User Experiences with Bitcoin Security and Privacy](https://link.springer.com/chapter/10.1007/978-3-662-54970-4_33) presents a large-scale survey on user experience in the Bitcoin ecosystem.
* Voskobojnikov. [Towards understanding and improving the crypto-asset user experience](https://open.library.ubc.ca/soa/cIRcle/collections/ubctheses/24/items/1.0401956) (PhD thesis) analyzes the profiles of cryptocurrency users and the UX challenges they face.

See also: [Wallet Scrutiny](https://walletscrutiny.com/), a project to check Bitcoin wallets for code reproducibility.


# Research Areas in Second-Layer Protocols

This section focuses on protocols build on top of Bitcoin.
Such protocols are often referred to as off-chain or second-layer (L2) protocols.
They provide additional functionality and use the base layer (Bitcoin) for dispute resolution.
The most prominent Bitcoin-based L2 protocol is the Lightning Network (LN).
It is a _payment channel network_ (PCN) that achieves low payment latency and high transactional throughput while accepting additional security assumptions.
Other second-layer (L2) protocols are also being developed.

For a general introduction, see:

* Poon and Dryja. [The Bitcoin Lightning Network: Scalable Off-Chain Instant Payments](https://lightning.network/lightning-network-paper.pdf) introduces the LN.[^2]
* Aaron van Wirdum. [Understanding the Lightning Network](https://bitcoinmagazine.com/technical/understanding-the-lightning-network-part-building-a-bidirectional-payment-channel-1464710791) (a series of articles for Bitcoin Magazine).
* Papadis and Tassiulas. [Blockchain-Based Payment Channel Networks: Challenges and Recent Advances](https://ieeexplore.ieee.org/document/9300150).

See also [LN Research Community](https://github.com/lnresearch) for LN datasets and inspection tools.

[^2]: Also see [the LN specifications (BOLTs)](https://github.com/lightning/bolts) for a formal protocol description.


## L2 Protocol Design

Developing and analyzing L2 protocols remains a research challenge.
The general question is: how to design a high-throughput Bitcoin-based second-layer protocol that requires minimal or no modification to the base layer, imposes low resource requirements, preserves user privacy, and does not rely on a trusted third party?

L2 protocol design involves addressing trade-offs.
The protocol should provide additional functionality besides what is available on the base layer without giving up too much security.
Game theory plays an important role here too, as L2 networks are generally maintained by independent actors whose behavior should be properly incentivized.
Another key consideration is decentralization.
Even though L2 nodes may rationally prefer connecting to already well-connecting nodes ("hubs"), causing topological[^4] centralization, the network must remain permissionless, censorship-resistant, and privacy-preserving.

Current research and development efforts include:

* **eltoo** is a new payment channel construction with a more efficient state replacement mechanism. In eltoo, nodes only store the latest channel state (whereas LN nodes store all prior states to ensure a fair dispute resolution). Eltoo relies on a yet-to-be-implemented upgrade to Bitcoin ([SIGHASH_ANYPREVOUT](https://bitcoinops.org/en/topics/sighash_anyprevout/)). See: Decker et al. [eltoo: A Simple Layer2 Protocol for Bitcoin](https://diyhpl.us/~bryan/papers2/bitcoin/eltoo.pdf).
* **Generic oracle-powered contracts** allow parties to sign a contract whose resolution depends on the outcome of a real-world event as reported by a trusted _oracle_. See: Le Guilly et al. [Bitcoin Oracle Contracts: Discreet Log Contracts in Practice](https://ieeexplore.ieee.org/abstract/document/9805512).
* **Chaumian e-cash in the Bitcoin context.** Another approach to scaling Bitcoin is to implement [Chaumian e-cash](http://www.hit.bme.hu/~buttyan/courses/BMEVIHIM219/2009/Chaum.BlindSigForPayment.1982.PDF) within federations, which are communicating via the LN (see [Fedimint](https://fedimint.org/)).
* **Rollups.** A rollup is a family of L2 protocols for blockchain scaling that execute transactions off-chain and verify their correctness on-chain. Research has been published on the feasibility of both major categories of rollups in Bitcoin: [validity rollups](https://bitcoinrollups.org/) and [zk-rollups](https://tr3y.io/articles/crypto/bitcoin-zk-rollups.html).

Prior work on L2 designs also includes:

* Aumayr et al. [Bitcoin-Compatible Virtual Channels](https://publik.tuwien.ac.at/files/publik_292507.pdf) adapts a payment channel construction called _virtual_ channels to Bitcoin. A virtual channel allows two PCN nodes, under certain security assumptions, to exchange payments as if they had a direct channel, without the involvement of intermediary nodes.
* Aumayr et al. [Blitz: Secure Multi-Hop Payments Without Two-Phase Commits](https://www.usenix.org/conference/usenixsecurity21/presentation/aumayr) proposes an improved payment channel protocol that only requires one round of communication between the sender and the receiver, which is an improvement over the LN that requires two.
* Kiayias and Thyfronitis Litos. [Elmo: Recursive Virtual Payment Channels for Bitcoin](https://eprint.iacr.org/2021/747) introduces a Bitcoin-suitable _virtual_ channel constructor that is recursive and supports channels with an indefinite lifetime.

[^3]: More precisely, [_weight_](https://en.bitcoin.it/wiki/Weight_units).
[^4]: There are multiple metrics of centralization; evaluating their applicability in the context of the LN and similar networks is a separate research question.


## Security

Second-layer protocols rely on base layer availability.
In the LN, for instance, a fraudulent channel closure can be disputed within a given a time window.
Dispute resolution depends on whether the justice transaction is timely broadcast and confirmed.

Modern research directions include:

* **Interaction with the base layer.** L2 protocols rely on the base layer for rule enforcement. How can we make such enforcement reliable? The fundamental challenge is that congestion levels cannot be reliably predicted, which enables attack vectors like [transaction pinning](https://bitcoinops.org/en/topics/transaction-pinning/) and flood-and-loot (see below).
* **Trustless watchtowers.** An LN user must monitor the Bitcoin blockchain to dispute fraud attempts. This task can be delegated to a third-party service called a watchtower. How to develop an incentive-compatible and privacy-preserving watchtower protocol? A watchtower should be accountable (get paid only if it does its job, and get punished if it doesn't), while knowing as little as possible about its client. A related challenge is to enforce fair completion of in-flight payments after channel closure. See a watchtower implementation: [The Eye of Satoshi (rust-teos)](https://github.com/talaia-labs/rust-teos).
* **Addressing DoS vectors, such as jamming.** Jamming is a denial-of-service attack that involves initiating payments and delaying their finalization. Multiple approaches to jamming countermeasures [have been discussed](https://blog.bitmex.com/preventing-channel-jamming/), including new [fee and reputation schemes](https://research.chaincode.com/2022/11/15/unjamming-lightning/). How to protect the LN and other L2 protocols from DoS attacks?

Prior work includes:

* Harris and Zohar. [Flood & Loot: A Systemic Attack On The Lightning Network](https://arxiv.org/abs/2006.08513) describes an attack on the LN whereby an adversary floods the base layer with fraudulent channel closure transaction, causing congestion and preventing justice transactions from getting confirmed. The issue might be exacerbated by manipulating the pre-agreed on-chain fees in advance.
* Mizrahi et al. [Congestion Attacks in Payment Channel Networks](https://arxiv.org/abs/2002.06564) evaluates the cost of channel jamming.
* Riard and Naumenko. [Time-Dilation Attacks on the Lightning Network](https://arxiv.org/abs/2006.01418) explores the implications of eclipse attacks on the LN and shows how a adversary who controls the victim's view of the Bitcoin network can steal LN funds.
* Rohrer et al. [Discharged Payment Channels: Quantifying the Lightning Network's Resilience to Topology-Based Attacks](https://arxiv.org/abs/1904.10253) derives the optimal attacker's strategies for channel exhaustion and node isolation in the view of the LN network topology.
* Tohner et al. [Hijacking Routes in Payment Channel Networks: A Predictability Tradeoff](https://arxiv.org/abs/1909.06890) describes an attack that involves attracting LN payments by advertising low fees and then denying service.
* Tsabary et al. [MAD-HTLC: Because HTLC is Crazy-Cheap to Attack](https://arxiv.org/abs/2006.12031) indicates a potential for miner bribery attacks in the current LN protocol and proposes a more game-theoretically robust construction for channel updates.

Proposed watchtower schemes include:

* Avarikioti et al. [Cerberus Channels: Incentivizing Watchtowers for Bitcoin](https://eprint.iacr.org/2019/1092) proposes a Bitcoin-compatible payment channel construction with incentivized watchtowers.
* Khabbazian et al. [Outpost: A Responsive Lightweight Watchtower](https://eprint.iacr.org/2019/986) suggests encoding justice transaction in the opening and commitment transactions in the LN to reduce storage requirements for watchtowers.
* Mirzaei et al. [FPPW: A Fair and Privacy Preserving Watchtower For Bitcoin](https://eprint.iacr.org/2021/117) proposes a watchtower scheme for Bitcoin with fairness and balance privacy.


## Privacy

L2 protocols present a novel set of privacy challenges.
The LN, in particular, should not reveal a user's balance, their position in the payment path, or even the existence of their channels (if they don't announce it).

Privacy-related research areas include:

* **Cross-layer privacy.** Currently, LN channels are linked to their respective opening on-chain transactions. This allows for enriching existing on-chain address clustering data with LN information. With Schnorr signatures, it is possible to make LN-related transactions indistinguishable from other transactions on the base layer through signature aggregation. However, channel announcements must still commit to some scarce resource to avoid denial-of-service attacks. How can we ensure that L2 activity remains opaque from the base-layer viewpoint?
* **Multi-hop payment de-correlation with PTLCs.** Point Time Locked Contracts (PTLCs) are a new type of multi-hop Schnorr-based channel locks. Currently, the LN relies on hashed time-locked contracts (HTLCs) to ensure atomicity in multi-hop payments. HTLCs along a path have the same hash. PTLC is an alternative for HTLC that avoids hop correlation. See: Malavolta et al. [Anonymous Multi-Hop Locks for Blockchain Scalability and Interoperability](https://eprint.iacr.org/2018/472). For a recent write-up, see: [Multi-Hop Locks from Scriptless Scripts](https://github.com/ElementsProject/scriptless-scripts/blob/master/md/multi-hop-locks.md).
* **Privacy-preserving routing.** Receivers in the LN currently reveal their node identity to the sender. Techniques like [blinded paths](https://github.com/lightning/bolts/pull/765) aim to lift this requirement to ensure sender privacy. See also: [trampoline payments](https://bitcoinops.org/en/topics/trampoline-payments/). An adversary can also make educated guesses about routes by running the path-finding algorithm locally on a graph snapshot. Privacy leaks also occur through response timings (see: Rohrer and Tschorsch. [Counting Down Thunder: Timing Attacks on Privacy in Payment Channel Networks](https://arxiv.org/abs/2006.12143)). Privacy-preserving routing remains an open problem.
* **Preventing balance probing.** Channel balances are not announced, but they can be easily _probed_, that is, estimated based on error messages. Nodes perform probing to increase success rates of their own payments, as the uncertainty of channel balances is the leading cause of payment failures. Constant probing (sending payments that immediately fail) burdens the network. How do we reconcile payment reliability with privacy? See e.g.: Herrera-Joancomartí et al. [On the Difficulty of Hiding the Balance of Lightning Network Channels](https://eprint.iacr.org/2019/328).

The following papers analyze privacy challenges for the LN:

* Kappos et al. [An Empirical Analysis of Privacy in the Lightning Network](https://arxiv.org/abs/2003.12470) describes multiple privacy attacks on the LN, including identifying unannounced channels and path discovery by an honest-but-curious routing node.
* Nisslmueller et al. [Toward Active and Passive Confidentiality Attacks On Cryptocurrency Off-Chain Networks](https://arxiv.org/abs/2003.00003) investigates two attacks on the LN: channel balance probing and timing attacks.
* Romiti et al. [Cross-Layer Deanonymization Methods in the Lightning Protocol](https://arxiv.org/abs/2007.00764) investigates how the LN interacts with the base layer and what heuristics help attackers diminish LN users' privacy.

See [an overview](https://lightningprivacy.com/) of privacy challenges and solutions in the LN by benthecarman et al.


## Economics and Network topology

LN nodes open channels and deploy liquidity into the network to send or receive payments, or to earn routing fees.
An open question is: how to optimally deploy liquidity in the LN to maximize fee revenue and payment reliability (or other chosen metrics)?

* **Increasing payment success rate.** Many LN payment require multiple attempts to succeed, which takes time. Moreover, re-trying a payment may not be possible in certain scenarios. How to make LN payments reliable without introducing central points of failure?
* **Liquidity management.** LN payments often fail because of lack of liquidity somewhere along the path. Routing nodes use _liquidity management_ techniques such as _channel rebalancing_ to increase payment success rates. What is the optimal liquidity management algorithm?
* **Channel partner selection.** What is the optimal way for a node to choose a channel partner? Preferential attachment is a concern from a centralization standpoint: nodes have an incentive to connect to already well-connected nodes. How to find a trade-off between each node's individual motivations and the sustainability of the network as a whole?

Prior work includes:

* Pickhardt and Nowostawski. [Imbalance measure and proactive channel rebalancing algorithm for the Lightning Network](https://ieeexplore.ieee.org/abstract/document/9169456) describes a technique for rebalancing (shifting liquidity between channels to increase success rates).
* Avarikioti et al. [HIDE & SEEK: Privacy-Preserving Rebalancing on Payment Channel Networks](https://eprint.iacr.org/2021/1401) presents an opt-in rebalancing protocol that uses multi-party computation for stronger privacy.
* Papadis and Tassiulas. [State-Dependent Processing in Payment Channel Networks for Throughput Optimization](https://arxiv.org/abs/2103.17207) proposes using a channel buffer wherein payments routed in the opposite directions balance each other out to avoid liquidity depletion.
* Guasoni et al. [Lightning Network Economics: Channels](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3840374) quantifies the cost of LN channels and the optimal conditions for two parties to open a channel.
* Beres et al. [A Cryptoeconomic Traffic Analysis of Bitcoin's Lightning Network](https://arxiv.org/abs/1911.09432) simulates LN traffic based on a public network snapshot, estimates feasible fee revenues, and analyzes the network's economic viability as well as privacy.
* Lin et al. [Lightning network: a second path towards centralisation of the Bitcoin economy](https://iopscience.iop.org/article/10.1088/1367-2630/aba062/meta) analyzes the topological centralization of the LN.


## Routing

Each payment in the LN is forwarded along a route chosen by the sender.
The sender considers multiple factors, such as the network topology, channel capacities, advertised fees, and outcomes of prior payment attempts.
Classical path-finding algorithm, such as the Dijkstra algorithm, are not directly applicable, as the sender can't assign edge weights (remote channels balances are generally unknown).

An open research question is **developing a path selection algorithm** for the LN with the following properties:

* Efficiency. Payments should succeed after a low number of attempts (ideally, after just one attempt), while avoiding overpaying in fees. The key obstacles are the uncertainty of channel balances and the fact that some nodes along the route may be offline.
* Being trustless. The sender should not have to delegate path-finding to a trusted third party.
* Security. A routing mechanism should not facilitate attacks. For instance, an adversarial node should not be able to predict other nodes' routing decisions based on public data. Neither should it be possible to reliably influence route selection through strategically chosen announcements (for instance, attract payments by advertising very low fees).
* Privacy. Route selection must not compromise users' privacy.
* Moderate resource usage. Route selection should be feasible on resource-constrained devices in terms of memory and processing power. Currently, sending nodes store the entire public LN graph. As the network grows, path-finding on a partial or compressed graph snapshot may become necessary. 

Prior work on PCN routing includes:

* Sivaraman et al. [High Throughput Cryptocurrency Routing in Payment Channel Networks](https://arxiv.org/abs/1809.05088) suggests a routing algorithm for PCNs that incentivizes rebalancing with adaptive fees.
* Roos et al. [Settling Payments Fast and Private: Efficient Decentralized Routing for Path-Based Transactions](https://arxiv.org/abs/1709.05748) explores embedding-based path discovery for PCNs.
* Pickhardt and Richter. [Optimally Reliable and Cheap Payment Flows on the Lightning Network](https://arxiv.org/abs/2107.05322) proposes an improved path-finding approach for the LN based on the success probabilities of payment attempts. This proposal has been implemented as [a Python package](https://github.com/renepickhardt/pickhardtpayments) and as [a plugin for LND](https://github.com/C-Otto/lnd-manageJ/blob/main/PickhardtPayments.md), a popular LN implementation.

