# RSCS-Q: Reflex-Symbolic Cognitive System with Quorum Governance- A Multi-Layer Governance Stack for Autonomous Cognitive Systems

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![LaTeX](https://img.shields.io/badge/LaTeX-2e-blue.svg)](https://www.latex-project.org/)
[![Tests](https://img.shields.io/badge/Tests-83%2F83%20Passing-green.svg)](#test-coverage)

> **A governance framework for autonomous cognitive systems with formal verification, multi-agent consensus, and human oversight.**

---

## 📚 Publication Series

The RSCS-Q framework is documented across six booklets plus a capstone integration document:

| Booklet | Title | Description | PDF |
|---------|-------|-------------|-----|
| **B1** | [Symbolic Metrics](tex/booklet1.tex) | Foundation layer: EDR, SOC, VSI, Φ metrics | [📄]( booklet1.pdf) |
| **B2** | [Capsule Governance](tex/booklet2.tex) | Memory & lifecycle: RCI, PSR, SHY with capsule state machine | [📄](booklet2.pdf) |
| **B3** | [Reflex Symbol Grammar](tex/booklet3.tex) | RSG state machine (S0-Q4) & RCC v1.1 audit chain | [📄](pdf/booklet3.pdf) |
| **B4** | [Swarm Coherence & RA](tex/booklet4.tex) | Multi-agent consensus: κ_t, S_fork, RA protocol | [📄](pdf/booklet4.pdf) |
| **B5** | [ADM Interface](tex/booklet5.tex) | Operator console: Mission DSL, guardrails, overrides | [📄](pdf/booklet5.pdf) |
| **Cap** | [Survivability & Audit](tex/capstone.tex) | AY metric, Hump Test ablation, H1-H12 acceptance bars | [📄](pdf/capstone.pdf) |
| **B6** | Entropica Integration | *Planned* — Platform deployment bridge | — |

---

## 🎯 Key Concepts

### Autonomy Yield (AY)

The composite metric quantifying threshold crossing for autonomous operation:

```
AY = 0.25·c_RA + 0.25·c_PSR + 0.25·c_MTTR + 0.25·c_forks
```

Where:
- **c_RA**: Recovery Alignment success rate
- **c_PSR**: Policy Satisfaction Rate improvement
- **c_MTTR**: Mean Time To Recovery (normalized)
- **c_forks**: Fork resolution completeness

**Threshold**: AY ≥ 0.65 indicates governed autonomy achieved.

### Governance Stack

```
┌─────────────────────────────────────────────────────────────────┐
│  Capstone: Survivability (AY Metric, Hump Test, H1-H12)        │
├─────────────────────────────────────────────────────────────────┤
│  B5: ADM Interface (Mission DSL, Guardrails, Override Audit)   │
├─────────────────────────────────────────────────────────────────┤
│  B4: Swarm Coherence (κ_t, S_fork) + RA Handshake (RA0-RA4)    │
├─────────────────────────────────────────────────────────────────┤
│  B3: Reflex Symbol Grammar (RSG) + RCC v1.1 Audit Chain        │
├─────────────────────────────────────────────────────────────────┤
│  B1/B2: Symbolic Metrics (EDR, SOC, VSI) + Capsule Memory      │
└─────────────────────────────────────────────────────────────────┘
```

---

## 📊 Test Coverage

All acceptance criteria validated across 83 tests:

| Module | Tests | Status |
|--------|-------|--------|
| B3: reflex_kernel.py | 22 | ✅ PASS |
| B3: rcc_v11.py | 14 | ✅ PASS |
| B4: swarm_sync.py | 17 | ✅ PASS |
| B5: adm_console.py | 16 | ✅ PASS |
| Cap: hump_test_harness.py | 7 | ✅ PASS |
| Cap: mission_trace_validator.py | 7 | ✅ PASS |
| **Total** | **83** | **✅ ALL PASS** |

### Acceptance Bars (H1-H12)

| ID | Metric | Target | Achieved | Status |
|----|--------|--------|----------|--------|
| H1 | MTTD (steps) | ≤6 | ≤6 | ✅ PASS |
| H2 | MTTR₉₅ (steps) | ≤5 | 4.2 | ✅ PASS |
| H3 | ΔPSR post | ≥+0.20 | +0.22 | ✅ PASS |
| H4 | False-gate rate | ≤10% | 0.3% | ✅ PASS |
| H5 | RA success rate | ≥90% | 97% | ✅ PASS |
| H6 | Unresolved forks | =0 | 0 | ✅ PASS |
| H7 | Audit loss (RCC) | =0 | 0 | ✅ PASS |
| H8 | Autonomy Yield | ≥0.65 | 0.68 | ✅ PASS |
| H9 | HashAgree rate | ≥98% | 98.5% | ✅ PASS |
| H10 | Operator accuracy | ≥95% | 97% | ✅ PASS |
| H11 | Dashboard latency | ≤100ms | 0.07ms | ✅ PASS |
| H12 | Quarantine FN | ≤1% | 0.3% | ✅ PASS |

---

## 🔧 Building from Source

### Prerequisites

- LaTeX distribution (TeX Live 2020+ or MiKTeX)
- Required packages: `amsmath`, `amssymb`, `amsthm`, `tikz`, `tcolorbox`, `listings`, `booktabs`, `hyperref`, `natbib`, `algorithm`, `algpseudocode`

### Compilation

```bash
# Build all booklets
make all

# Build individual booklet
cd tex/
pdflatex booklet1.tex
pdflatex booklet1.tex  # Run twice for references

# Build with bibliography
pdflatex booklet1.tex
bibtex booklet1
pdflatex booklet1.tex
pdflatex booklet1.tex
```

### Quick Build Script

```bash
#!/bin/bash
for doc in booklet1 booklet2 booklet3 booklet4 booklet5 capstone; do
    cd tex/
    pdflatex -interaction=nonstopmode $doc.tex
    pdflatex -interaction=nonstopmode $doc.tex
    mv $doc.pdf ../pdf/
    cd ..
done
```

---

## 📁 Repository Structure

```
rscsq-publication/
├── README.md              # This file
├── LICENSE                # MIT License
├── Makefile               # Build automation
├── tex/                   # LaTeX source files
│   ├── booklet1.tex       # Symbolic Metrics
│   ├── booklet2.tex       # Capsule Governance
│   ├── booklet3.tex       # Reflex Symbol Grammar
│   ├── booklet4.tex       # Swarm Coherence & RA
│   ├── booklet5.tex       # ADM Interface
│   └── capstone.tex       # Survivability & Audit
├── pdf/                   # Compiled PDFs
│   ├── booklet1.pdf
│   ├── booklet2.pdf
│   ├── booklet3.pdf
│   ├── booklet4.pdf
│   ├── booklet5.pdf
│   └── capstone.pdf
├── bib/                   # Bibliography
│   └── rscsq.bib          # Unified references
├── src/                   # Python implementation
│   ├── reflex_kernel.py   # RSG state machine
│   ├── rcc_v11.py         # RCC audit chain
│   ├── swarm_sync.py      # Swarm coherence
│   ├── adm_console.py     # ADM interface
│   └── compute_merkle.py  # Merkle utilities
├── tests/                 # Test suites
│   ├── test_reflex.py
│   ├── test_rcc.py
│   ├── test_swarm.py
│   ├── test_adm.py
│   └── test_hump.py
├── docs/                  # Supporting documentation
│   └── BRIDGE_TO_ENTROPICA.md
└── figures/               # TikZ source for diagrams
```

---

## 🚀 Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/entropica/rscsq.git
cd rscsq
```

### 2. Build PDFs

```bash
make all
```

### 3. Run Tests

```bash
cd tests/
python -m pytest test_*.py -v
```

### 4. View Documentation

Open `pdf/capstone.pdf` for the complete integration summary, or start with `pdf/booklet1.pdf` for foundational concepts.

---

## 📖 Reading Order

For new readers, we recommend:

1. **Capstone** (overview) — Understand the AY metric and acceptance criteria
2. **Booklet 1** — Learn symbolic metrics (EDR, SOC, VSI, Φ)
3. **Booklet 2** — Understand capsule governance (RCI, PSR, SHY)
4. **Booklet 3** — Study reflex grammar (RSG states, RCC audit)
5. **Booklet 4** — Explore swarm coherence (κ_t, RA protocol)
6. **Booklet 5** — Review operator interface (ADM console, DSL)
7. **Return to Capstone** — Deep dive into Hump Test ablations

---

## 🔬 Key Theorems

### Theorem 2.4 (RSG Determinism) — Booklet 3
> For any evaluation context C and state s, there exists exactly one valid successor state s' such that G_{s,s'}(C) = true.

### Theorem 2.6 (MTTR Bound) — Booklet 3
> Under RSG governance, MTTR ≤ 5 steps with probability ≥ 0.95.

### Theorem 5.2 (RA Safety) — Booklet 4
> No two agents commit conflicting Merkle roots in the same RA epoch under quorum q ≥ 2f+1.

### Proposition 5.2 (RA Necessary) — Capstone
> The RA mechanism is necessary for threshold crossing: disabling RA causes AY to fall below 0.65.

### Proposition 5.3 (RCC Sufficient) — Capstone
> RCC is sufficient but not necessary: disabling RCC maintains AY ≥ 0.65 (audit integrity, not threshold crossing).

---

## 📬 Citation

If you use RSCS-Q in your research, please cite:

```bibtex
@techreport{rscsq2025,
    author      = {{T.Stanford Erickson}},
    title       = {{RSCS-Q}: Reflex-Symbolic Cognitive System with Quorum Governance},
    institution = {Entropica},
    year        = {2025},
    note        = {Publication Series v2.2a}
}
```

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guidelines](CONTRIBUTING.md) for details.

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📧 Contact

- **Email**: toryerickson@gmail.com
- **GitHub**: [github.com/entropica/rscsq](https://github.com/entropica/rscsq)

---

## 🙏 Acknowledgments

- Reviewers who identified accuracy and completeness improvements
- The broader AI safety research community
- Contributors to foundational works cited in our bibliography

---

<p align="center">
  <strong>RSCS-Q: Governance for Autonomous Cognitive Systems</strong><br>
  <em>From command-and-control to threshold-sensitive self-monitoring</em>
</p>
