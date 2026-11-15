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

\documentclass[11pt,a4paper]{article}
\usepackage[utf8]{inputenc}
\usepackage[T1]{fontenc}
\usepackage{amsmath,amssymb,amsfonts}
\usepackage{hyperref}
\usepackage[margin=1in]{geometry}

\title{\textbf{AG-ZKP (v1.3): An Air-Gapped Sanitization Architecture and Three-Channel Leakage Model for Untrusted Groth16 Provers and zkML Containers}}

\author{
  \textbf{Mert Atakan} \\
  \small Conceptual Framework, Threat Modeling, and System Architecture
  \and
  \textbf{Muhammad Zidan Fatonie} \\
  \small System Architecture and Threat Surface Analysis
  \and
  \textbf{Anjul Khatri} \\
  \small Cryptographic Formalization and Protocol Analysis
}

\date{November 2026 \\ \small Version 1.3}

\begin{document}

\maketitle

\begin{abstract}
Zero-knowledge proof (ZKP) systems guarantee that a verifier learns nothing beyond the validity of a statement, yet standard definitions assume an honest prover that faithfully samples randomness and executes within a benign environment. When high-throughput proof generation---such as zero-knowledge machine learning (zkML) inference---is delegated to untrusted, containerized, or air-gapped third-party provers, a compromised prover or poisoned model weights can exfiltrate sensitive witness data ($w$) without violating completeness or soundness.

In this work, we formalize \textbf{AG-ZKP (v1.3)}, an applied boundary sanitization architecture that adapts the theoretical frameworks of Cryptographic Reverse Firewalls (Mironov \& Stephens-Davidowitz, EUROCRYPT 2015; Ganesh et al., ICALP 2020), Subversion-Resilient ZK (Bellare, Fuchsbauer \& Scafuro, ASIACRYPT 2016; Fuchsbauer, PKC 2018), and Steganography-Free Zero-Knowledge (Abdolmaleki et al., TCC 2022) to non-interactive Groth16 proving pipelines. Rather than claiming a new cryptographic primitive, AG-ZKP introduces a unified \textbf{Three-Channel Leakage Model}
\[
\mathcal{L}_{\text{total}} = \mathcal{L}_{\pi} + \mathcal{L}_{\Delta t} + \mathcal{L}_{y}
\]
across a unidirectional air-gapped boundary:
\begin{enumerate}
    \item \textbf{Algebraic Proof Channel ($\mathcal{L}_{\pi} = 0$):} A stateless boundary sanitizer parses candidate Groth16 proofs into canonical group representations, rejects trailing bytes or malformed encodings, verifies the pairing equation against data-owner-supplied public inputs ($x$), and applies standard $(z, s')$ algebraic rerandomization:
    \[
    A' = zA, \quad B' = z^{-1}B + s'[\delta]_2, \quad C' = C + s'A'
    \]
    (Baghery et al., FC 2021) using independent hardware entropy ($z \leftarrow \mathbb{F}_r^*, s' \leftarrow \mathbb{F}_r$). This produces a fresh proof distributionally identical to an honest proof without requiring auxiliary prover elements.
    
    \item \textbf{Timing and Abort Channel ($\mathcal{L}_{\Delta t} = 0$):} Witness-dependent execution variance (such as MSM and NTT Hamming-weight timing side channels) and selective prover aborts are neutralized via deterministic epoch time-bucketing (Askarov, Zhang \& Myers, CCS 2010) combined with a strict fail-stop container quarantine policy.
    
    \item \textbf{Public Output Channel ($\mathcal{L}_{y} \le N \log_2 |\mathcal{Y}|$):} Addressing covert exfiltration through high-precision floating-point output mantissas in untrusted zkML inference, AG-ZKP enforces in-circuit discrete $\operatorname{argmax}$ quantization, strictly bounding cumulative multi-query leakage across $N$ inferences while preserving model commitment integrity.
\end{enumerate}
\end{abstract}

\section*{What's New in Version 1.3 (Release Notes)}
\begin{itemize}
    \item \textbf{Expanded Literature Grounding:} Added comprehensive citations and comparative positioning covering Cryptographic Reverse Firewalls (Mironov \& Stephens-Davidowitz 2015; Ganesh et al.\ 2020), Subversion-ZK (Bellare et al.\ 2016; Fuchsbauer 2018), Steganography-Free ZK (Abdolmaleki et al.\ 2022), Predictive Timing Mitigation (Askarov et al.\ 2010; Zhang et al.\ 2012), and AI Control containment protocols (Greenblatt et al., ICML 2024; Roger \& Greenblatt 2023).
    \item \textbf{Standard Groth16 Rerandomization (Proposition 1):} Replaced the auxiliary-element construction with standard $(z, s')$ Groth16 rerandomization (Baghery et al., FC 2021), ensuring compatibility with unmodified off-the-shelf Groth16 provers alongside strict canonical point re-serialization.
    \item \textbf{Three-Channel Leakage Budget \& Multi-Query Analysis:} Formalized cumulative public output leakage ($\mathcal{L}_{y} \le N \log_2 |\mathcal{Y}|$), explicit data-owner binding for public inputs ($x$), and fail-stop quarantine against invalid-proof/abort signalling.
    \item \textbf{Asymptotic Complexity \& Scope Refinement:} Replaced unbenchmarked latency estimates with exact algebraic operation counts ($2\text{ }\mathbb{G}_1\text{ scalar multiplications} + 2\text{ }\mathbb{G}_2\text{ scalar multiplications} + 1\text{ pairing verification}$), explicitly scoped out physical hardware emissions (TEMPEST/acoustic channels) and post-quantum security, and included an AI assistance disclosure.
\end{itemize}

\section*{Keywords}
\noindent Zero-Knowledge Proofs $\cdot$ Groth16 Rerandomization $\cdot$ Cryptographic Reverse Firewalls $\cdot$ Kleptography and Subliminal Channels $\cdot$ Zero-Knowledge Machine Learning (zkML) $\cdot$ Timing Side-Channel Mitigation $\cdot$ AI Control and Prover Isolation

\end{document}

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
