---
layout: page
title: Chaincode Research Seminar
order: 2
---

<div class="message">
  The Chaincode Research Seminar exists to foster and encourage collaboration between the open-source community, industry, and academia towards research advances that benefit Bitcoin.
  Mailing list <a href="https://gmail.us12.list-manage.com/subscribe?u=d60d7dfc73006b95a62450c30&id=7fa7f74340">subscribe</a>.
</div>

<!---

HTML defines a long list of available inline tags, a complete list of which can be found on the [Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/HTML/Element).
- **To bold text**, use `<strong>`.
- *To italicize text*, use `<em>`.
- Abbreviations, like <abbr title="HyperText Markup Langage">HTML</abbr> should use `<abbr>`, with an optional `title` attribute for the full phrase.
- Citations, like <cite>&mdash; Mark otto</cite>, should use `<cite>`.
- <del>Deleted</del> text should use `<del>` and <ins>inserted</ins> text should use `<ins>`.
- Superscript <sup>text</sup> uses `<sup>` and subscript <sub>text</sub> uses `<sub>`.

--->

**Date**: Wednesday September 28th, 2022

**Speaker**: Victor Shoup

**Title**: A new threshold ECDSA protocol: its design and analysis

**Abstract**: We present and analyze a new protocol that provides a distributed ECDSA signing service, with the following properties: it works in an asynchronous communication model; it works with n parties with up to f < n/3 Byzantine corruptions; it provides guaranteed output delivery; it provides a very efficient, non-interactive online signing phase; it supports additive key derivation according to the BIP32 standard. This service is being implemented and integrated into the architecture of the Internet Computer, enabling smart contracts running on the Internet Computer to securely hold and spend Bitcoin and other cryptocurrencies.

<hr style="border:2px solid light gray">

**Date**: Wednesday September 14th, 2022

**Speaker**: Joseph Bonneau 

**Title**: Short-lived proofs

**Abstract**: This talk will discuss short-lived proofs, a non-interactive proof of knowledge with a novel feature: after a specified period of time, the proof is no longer convincing. This time-delayed loss of soundness happens "naturally" without further involvement from the prover or any third party. The talk will discuss potential applications of short-lived proofs and short-lived signatures (a special case). It will also show several practical constructions built using verifiable delay functions (VDFs), including two novel types of VDFs, re-randomizable VDFs and zero-knowledge VDFs, which may be of independent interest.
