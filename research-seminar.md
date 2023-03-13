---
layout: page
title: Chaincode Research Seminar
order: 2
---

<div class="message">
  The Chaincode Research Seminar exists to foster and encourage collaboration between the open-source community, industry, and academia towards research advances that benefit Bitcoin.
 </div>


 Subscribe to our mailing list by clicking [here](https://gmail.us12.list-manage.com/subscribe?u=d60d7dfc73006b95a62450c30&id=7fa7f74340).
 
  <hr style="border:2px solid gray">
 
 
**Date**: Tuesday March 14th, 2023

**Speaker**: Benedikt Bünz (Espresso Systems, NYU (soon))

**Title**: HyperPlonk: Plonk with Linear-Time Prover and High-Degree Custom Gates

**Abstract**: Plonk is a widely used succinct non-interactive proof system that uses univariate polynomial commitments. Plonk is quite flexible: it supports circuits with low-degree ``custom'' gates as well as circuits with lookup gates (a lookup gate ensures that its input is contained in a predefined table). For large circuits, the bottleneck in generating a Plonk proof is the need for computing a large FFT.

We present HyperPlonk, an adaptation of Plonk to the boolean hypercube, using multilinear polynomial commitments. HyperPlonk retains the flexibility of Plonk but provides several additional benefits. First, it avoids the need for an FFT during proof generation. Second, and more importantly, it supports custom gates of much higher degree than Plonk without harming the running time of the prover. Both of these can dramatically speed up the prover's running time. Since HyperPlonk relies on multilinear polynomial commitments, we revisit two elegant constructions: one from Orion and one from Virgo. We show how to reduce the Orion opening proof size to less than 10kb (an almost factor 1000 improvement) and show how to make the Virgo FRI-based opening proof simpler and shorter.

 <hr style="border:2px solid gray">
 
 
 
**Date**: Tuesday March 2nd, 2023

**Speaker**: Ben Fisch (Yale)

**Title**: Multilinear Schwartz-Zippel mod N with Applications to Succinct Arguments

**Abstract**: In this talk I will present a new variant of the Schwartz-Zippel lemma for multilinear integer polynomials modulo a composite integer N and remark on its application to succinct arguments. This lemma is a key ingredient to analyzing the security of the Bulletproofs protocol with commitment schemes that are only binding to vectors of small norm. These include commitments from groups of unknown order (DARK) as well as integer and ideal lattices (Ajtai). This is the first result showing that Bulletproofs (in its original form) is secure in the lattice setting even with exponentially sized challenges. Prior attempts restricted the challenges to exceptional sets, which have polynomial size, and thus required parallel repetition to amplify soundness.

 <hr style="border:2px solid gray">
 
 
 
 
 
**Date**: Tuesday February 21st, 2023 (Moved to April 11th)

**Speaker**: Maryam Bahrani (a16z)

**Title**: Statistically Undetectable Selfish Mining

**Abstract**: Seminal work of Eyal and Sirer (2014) establishes that a strategic Bitcoin miner may strictly profit by deviating from the intended Bitcoin protocol, using a strategy now termed selfish mining. More specifically, any miner with >1/3 of the total hashrate can earn bitcoin at a faster rate by selfish mining than by following the intended protocol (depending on network conditions, a lower fraction of hashrate may also suffice). Nonetheless, no evidence of selfish mining attacks has been reported in practice (even during periods where a single pool controlled >1/3 of the total Bitcoin hashrate, and even on smaller blockchains where it is relatively less expensive for a single miner to control >1/3 of the total hashrate).

While there are several possible explanations for this, the most cited (and perhaps also the most convincing) is that the presence of a selfish miner is statistically detectable: the pattern of orphaned blocks created by the presence of a selfish miner cannot be explained by natural network delays. Therefore, if an attacker chooses to selfish mine, users will likely notice, and the USD value of Bitcoin may tank. So while the attacker may get slightly more bitcoin by selfish mining, these bitcoins may be worth significantly less USD.

We develop a variant of selfish mining that is provably statistically undetectable: the pattern of orphaned blocks is statistically identical to a world with only honest miners but higher network delay. Specifically, we consider a stylized model where honest miners with network delay produce orphaned blocks at each height independently with probability $\beta'$. We propose a selfish mining strategy that instead produces orphaned blocks at each height independently with probability $\beta > \beta'$ instead. We further show that our strategy is still strictly profitable for attackers with << 1/2 of the total hashrate (for example, when $\beta' = 0$, our strategy is strictly profitable with 38.2% of the total hashrate).

We conclude that statistically undetectable and strictly profitable attacks on any longest-chain proof-of-work blockchain are possible. This suggests that sufficiently large attackers can profitably deviate from the intended Bitcoin protocol (or, perhaps more likely, smaller blockchains where it is relatively less expensive to control >38.2\% of the total hashrate) without risk of tanking the value.

 <hr style="border:2px solid gray">
 
 
 
**Date**: Tuesday January 31st, 2023

**Speaker**: Agostino Capponi (Columbia University)

**Title**: Price Discovery on Decentralized Exchanges

**Abstract**: In contrast to most centralized exchanges (CEXs) which match orders continuously following a price-time priority rule, decentralized exchanges (DEXs) process orders in batches and require traders to bid transaction fees to determine the execution priority. We provide evidence that informed traders bid high fees to execute their orders, thus revealing their private information and contributing to price discovery. We further show that they bid high fees not only to avoid execution risk but also to compete with each other. Using a unique dataset of Ethereum mempool orders, we last demonstrate that the competition among informed traders mostly follows a jump bidding strategy.

<hr style="border:2px solid gray">

**Date**: Tuesday November 15th, 2022

**Speaker**: Tim Ruffing (Blockstream) 

**Title**: ROAST: Robust Asynchronous Schnorr Threshold Signatures

**Abstract**: Bitcoin and other cryptocurrencies have recently introduced support for Schnorr signatures whose cleaner algebraic structure, as compared to ECDSA, allows for simpler and more practical constructions of highly demanded "t-of-n" threshold signatures. However, existing Schnorr threshold signature schemes still fall short of the needs of real-world applications due to their assumption that the network is synchronous and due to their lack of robustness, i.e., the guarantee that t honest signers are able to obtain a valid signature even in the presence of other malicious signers who try to disrupt the protocol. This hinders the adoption of threshold signatures in the cryptocurrency ecosystem, e.g., in second-layer protocols built on top of cryptocurrencies.

In this work, we propose ROAST, a simple wrapper that turns a given threshold signature scheme into a scheme with a robust and asynchronous signing protocol, as long as the underlying signing protocol is semi-interactive (i.e., has one preprocessing round and one actual signing round), provides identifiable aborts, and is unforgeable under concurrent signing sessions. When applied to the state-of-the-art Schnorr threshold signature scheme FROST, which fulfills these requirements, we obtain a simple, efficient, and highly practical Schnorr threshold signature scheme.


<hr style="border:2px solid gray">

**Date**: Tuesday November 8th, 2022

**Speaker**: Nikolaos Papadis (Yale)

**Title**: Towards Optimal Scheduling and Rebalancing in Payment Channel Networks

**Abstract**: Permissionless blockchains like Bitcoin enable multiple parties to reach consensus without the need for mutual trust. However, they usually cannot sustain high throughput and low fees for everyday users. This is why the "layer-2" solution of payment channel networks (PCNs) such as the Lightning Network has been introduced, enabling cheap and fast transactions. In this presentation, we will examine how to improve the Lightning Network's performance. First, we will focus on the transaction scheduling problem and describe a theoretically provable throughput-optimal scheduling policy for a payment channel. Second, we will formulate the optimal channel rebalancing problem for PCN relay nodes as a Markov Decision Process and adapt a reinforcement learning algorithm to arrive at approximately optimal policies that outperform current heuristics based on experiments in a custom-built PCN discrete event simulator. Finally, we will discuss future directions related to Lightning's performance improvement and long-term viability.

Related papers:
- *Payment Channel Networks: Single-Hop Scheduling for Throughput Maximization*, INFOCOM 2022, [link](https://ieeexplore.ieee.org/document/9796862); earlier arXiv version: [link](https://arxiv.org/abs/2103.17207)
- *Deep Reinforcement Learning-based Rebalancing Policies for Profit Maximization of Relay Nodes in Payment Channel Networks*, preprint, [link](https://eprint.iacr.org/2022/1385)
- *Blockchain-based Payment Channel Networks: Challenges and Recent Advances*, IEEE Access, [link](https://ieeexplore.ieee.org/document/9300150)


<hr style="border:2px solid gray">

**Date**: Tuesday October 25th, 2022

**Speaker**: Yonatan Sompolinsky (Harvard University)

**Title**: The DAG KNIGHT Protocol -- a Parameterless Generalization of Nakamoto Consensus

**Abstract**: Consensus protocols typically assume a certain bound on the network's latency. Thus, live protocols behave and perform according to this pre-set hard-coded parameter -- e.g., Bitcoin's 10 minutes block interval, Ethereum's 12 seconds, etc. In this work we set out to design a protocol that assumes no such bound (formally, which operates in the partially synchronous setup). That is, we design a POW-based blockDAG protocol that orders blocks and transactions in a way that guarantees eventual agreement across all nodes, and which further guarantees fast optimistic convergence in the order of the network's RTT. Our protocol, DAG KNIGHT, assumes no upper bound on the network's latency, is secure against any attacker with less than 50% of the hashrate, and is the first protocol to achieve these properties. This achievement is in tension with a known impossibility result regarding the security threshold of partially synchronous consensus, which we circumvent by requiring the client (the full node accepting the transaction) to set locally a bound on the recent latency in the network. 

DAG-KNIGHT is a (sophisticated) extension of PHANTOM, which in turn is a generalization of Bitcoin's Nakamoto Consensus. 

In the talk, I will go over the basic concepts and components of the protocol, and will cover practical implications to POW consensus.

(Joint work with Michael Sutton (DAGlabs))


<hr style="border:2px solid gray">

**Date**: Wednesday September 28th, 2022

**Speaker**: Victor Shoup (DFINITY/NYU)

**Title**: A new threshold ECDSA protocol: its design and analysis

**Abstract**: We present and analyze a new protocol that provides a distributed ECDSA signing service, with the following properties: it works in an asynchronous communication model; it works with n parties with up to f < n/3 Byzantine corruptions; it provides guaranteed output delivery; it provides a very efficient, non-interactive online signing phase; it supports additive key derivation according to the BIP32 standard. This service is being implemented and integrated into the architecture of the Internet Computer, enabling smart contracts running on the Internet Computer to securely hold and spend Bitcoin and other cryptocurrencies.

<hr style="border:2px solid gray">

**Date**: Wednesday September 14th, 2022

**Speaker**: Joseph Bonneau (a16z)

**Title**: Short-lived proofs

**Abstract**: This talk will discuss short-lived proofs, a non-interactive proof of knowledge with a novel feature: after a specified period of time, the proof is no longer convincing. This time-delayed loss of soundness happens "naturally" without further involvement from the prover or any third party. The talk will discuss potential applications of short-lived proofs and short-lived signatures (a special case). It will also show several practical constructions built using verifiable delay functions (VDFs), including two novel types of VDFs, re-randomizable VDFs and zero-knowledge VDFs, which may be of independent interest.


<hr style="border:2px solid gray">

**Date**: Wednesday August 8th, 2022

**Speaker**: Aviv Zohar

**Title**: "Twilight: A Differentially Private Payment Channel Network"
Joint work with: Saar Tochner, Maya Dotan and Yossi Gilad. 

**Abstract**: Payment channel networks (PCNs) provide a faster and cheaper alternative to transactions recorded on the blockchain, but unfortunately do not provide privacy: anyone can track a client’s
payments by monitoring changes in coin balances over the network’s channels. We present Twilight, the first PCN that provides a rigorous differential privacy guarantee to its users. Relays in Twilight run a noisy payment processing mechanism that hides the payments they carry and enforce the protocol using a trusted execution environment (TEE). We ensure that even if a relay breaks the TEE’s security, it cannot break the integrity of the PCN.

We analyze Twilight in terms of privacy and cost and study the trade-off between them. We go on to provide performance measurements on a prototype we implemented using Intel’s SGX framework.


<hr style="border:2px solid gray">

**Date**: Tuesday July 19th, 2022

**Speaker**: Aviv Yaish (The Hebrew University)

**Title**: Blockchain Stretching & Squeezing: Manipulating Time For Your Best Interest

**Abstract**: We present a novel way for cryptocurrency miners to manipulate the effective interest-rate on loans or deposits they make on decentralized finance (DeFi) platforms by manipulating difficulty-adjustment algorithms (DAAs) and changing the block-rate. This presents a new class of strategic manipulations available to miners.
These manipulations allow miners to stretch and squeeze the time between consecutive blocks. We analyze these manipulations both analytically and empirically, and show that a 25% miner can stretch the time between consecutive blocks by up to 54% in Ethereum and 33% in Bitcoin, and squeeze it by up to 9% in Ethereum. Ethereum is particularly vulnerable, and even 10% and smaller miners can seriously affect the block-rate.
An interesting application of these manipulations is to create an artificial interest-rate gap between loans taken from one DeFi platform which accrues interest according to block height (such as Compound [Leshner and Hayes, 2019]) and deposited in some other platform that does so according to elapsed time (like a bank, or other DeFi platforms such as Aave [wow, 2020]). Hence, stretching and squeezing the block-rate can decrease the interest paid on DeFi loans relative to external financial platforms.
The profit made from this interest-rate gap provides a large incentive for miners to deviate. For example, a 25% Ethereum miner using our manipulations can increase mining profits by up to 35%, even after taking potential losses into consideration, such as less block-rewards.
Our analysis of these manipulations and their mitigations has broad implications with regards to commonly-used cryptocurrency mechanisms and paradigms, such as Ethereum’s difficulty-adjustment algorithm and reward schemes, with Ethereum’s handling of uncle blocks being particularly manipulable. Interestingly, Bitcoin’s mechanism is more resistant than Ethereum's, owing to its larger incentives and a more resilient DAA.
