# Zero-Knowledge Across the Air-Gap: Verifiable Computation with Strictly Offline Private Witnesses

**Author:** Mert Atakan  
**Status:** Preprint Technical Report (October 2026)  
**License:** [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)
[![DOI](https://zenodo.org/badge/1431609526.svg)](https://doi.org/10.5281/zenodo.23605859)


---

### 📄 Download Preprint PDFs
* **[Read the Standalone Academic Paper (PDF)](./ag-zkp-paper.pdf)** — *Zero-Knowledge Across the Air-Gap: Verifiable Computation and Subliminal-Free Proving with Strictly Offline Private Witnesses*
* **[Read the Extended Architecture Paper (PDF)](./arcanum-airgap-zk.pdf)** — *End-to-End Zero-Plaintext Assurance: Combining Confidential Compilation (Arcanum) with Air-Gapped Zero-Knowledge Proving*

---

### Abstract
Zero-Knowledge Proof (ZKP) systems enable a prover to convince a verifier that a statement $x$ is true with respect to a secret witness $w$ without revealing any information about $w$ across the verification channel. However, prevailing ZKP deployments rely on a flawed systemic assumption: that the proving environment itself is free from operating-system compromise or network-level exfiltration. Even in architectures utilizing hardware security modules or cold cryptographic wallets, "split-proving" protocols offload the computationally intensive witness generation and polynomial arithmetic onto a network-connected host, exposing the entirety of $w$ in volatile memory (RAM). Conversely, strictly air-gapped systems—deployed across critical infrastructure, nuclear telemetry, and genomic data cleanrooms—achieve physical confidentiality of $w$ at the cost of external auditability.

In this research, we introduce the formal framework for **Air-Gapped Zero-Knowledge Proving (AG-ZKP)**. We resolve the *Air-Gap Auditability Paradox* by synthesizing physical network isolation with succinct cryptographic verification over constrained, asymmetric physical channels (specifically optical QR fountain streams and unidirectional optical data diodes). Furthermore, we identify and mitigate three fundamental vulnerabilities unique to air-gapped proving:
1. **The Blinded Witness Synchronization Problem** (mitigated via subtree $k$-anonymity optical ingestion and incremental accumulator folding).
2. **The Optical Bandwidth vs. Proof Complexity Bottleneck** (formalizing the latency regime shift between Groth16, PLONK, and FRI-based zk-STARKs across optical QR links vs. fiber data diodes).
3. **Kleptographic Subliminal Channels** (eliminated via strict deterministic witness-bound derandomization and public bridge rerandomization).

---

### Citation (BibTeX)
If you reference this work, the threat model, or the AG-ZKP latency equations in your research, please cite:

```bibtex
## 📜 Licensing (Dual-License Model)

Arcanum and the AG-ZKP reference implementation are distributed under a **Dual-License** model:

1. **Open-Source License (GNU AGPLv3):** 
   This software is free and open-source under the terms of the [GNU Affero General Public License v3.0](LICENSE). It is fully compliant with open-source research grants (including NLnet / NGI). If you modify or run this software over a network (e.g., as a cloud/SaaS service or managed proxy), you must make your complete source code available under the AGPLv3.

2. **Commercial Enterprise License:** 
   For organizations, cloud backup providers, and enterprise custodians that wish to integrate Arcanum / AG-ZKP into proprietary, closed-source software, hardware appliances, or commercial SaaS platforms without the copyleft obligations of the AGPLv3, a separate **Commercial License** is available from Arcanum Research.

For commercial licensing inquiries, enterprise integrations, or partnerships, please contact: **mertatakan53@gmail.com**
@techreport{atakan2026airgapzk,
  title={Zero-Knowledge Across the Air-Gap: Verifiable Computation and Subliminal-Free Proving with Strictly Offline Private Witnesses},
  author={Atakan, Mert},
  year={2026},
  month={October},
  institution={Arcanum Research},
  note={Preprint available at [https://github.com/Sidistr/airgapped-zk-paper](https://github.com/Sidistr/airgapped-zk-paper)}
}
