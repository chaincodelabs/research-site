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

**Date**: Tuesday November 8th, 2022

**Speaker**: Nikolaos Papadis (Yale)

**Title**: Towards Optimal Scheduling and Rebalancing in Payment Channel Networks

**Abstract**: Permissionless blockchains like Bitcoin enable multiple parties to reach consensus without the need for mutual trust. However, they usually cannot sustain high throughput and low fees for everyday users. This is why the "layer-2" solution of payment channel networks (PCNs) such as the Lightning Network has been introduced, enabling cheap and fast transactions. In this presentation, we will examine how to improve the Lightning Network's performance. First, we will focus on the transaction scheduling problem and describe a theoretically provable throughput-optimal scheduling policy for a payment channel. Second, we will formulate the optimal channel rebalancing problem for PCN relay nodes as a Markov Decision Process and adapt a reinforcement learning algorithm to arrive at approximately optimal policies that outperform current heuristics based on experiments in a custom-built PCN discrete event simulator. Finally, we will discuss future directions related to Lightning's performance improvement and long-term viability.

Related papers:
- *Payment Channel Networks: Single-Hop Scheduling for Throughput Maximization*, INFOCOM 2022, [link](https://ieeexplore.ieee.org/document/9796862); earlier arXiv version: [link](https://arxiv.org/abs/2103.17207)
- *Deep Reinforcement Learning-based Rebalancing Policies for Profit Maximization of Relay Nodes in Payment Channel Networks*, preprint, [link](https://eprint.iacr.org/2022/1385)
Blockchain-based Payment Channel Networks: Challenges and Recent Advances, IEEE Access, [link](https://ieeexplore.ieee.org/document/9300150)


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
