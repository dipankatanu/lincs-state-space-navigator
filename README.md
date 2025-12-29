# LINCS State-Space Navigator

## 🚀 Research Aim
To model the LINCS L1000 perturbation landscape as a transcriptional state-space,
enabling prediction of perturbations (single or sequential) that optimally transition
a disease-associated expression state toward a therapeutic attractor.

**Core Question:**
By navigating the high-dimensional signature space, can we identify perturbations that
drive a disease state vector closer to a desired target state?

The core idea is simple:

\[
\text{Score}(p) = \cos(D + p,\; T)
\]

Where:

| Symbol | Meaning |
|--------|---------|
| D | disease state vector (for example EMT program) |
| p | LINCS perturbation signature (Level 5 COMPZ consensus) |
| T | target attractor vector (for example epithelial or MET state) |

Positive scores indicate movement toward the target therapeutic state.  
Negative scores indicate reinforcement of the disease state.

---

## Current Case Study: EMT to MET in MCF7

The first example provided in this repository focuses on reversing the Epithelial to Mesenchymal Transition (EMT) toward an epithelial or MET-like state in MCF7 cells (trt_cp, 24 h).

- D is built from MSigDB Hallmark EMT genes.
- T is built from epithelial or apical surface marker genes.
- p is the LINCS L1000 Level 5 (COMPZ) perturbation signature for MCF7, trt_cp, 24 h.

The framework is general and can be reused for other disease and target state pairs.

---

## Repository Structure

Example structure (your local tree may differ slightly):

```text
lincs-state-space-navigator/
├─ README.md
├─ LICENSE
├─ environment.yml
├─ requirements.txt        # optional, if you prefer pip
├─ .gitignore
├─ config/
│  └─ example_config.yaml  # example configuration for paths and options
├─ data/
│  ├─ example/             # small sample dataset for testing (committed)
│  ├─ raw/                 # store downloaded LINCS data here (not committed)
│  └─ processed/           # processed matrices and intermediate results
├─ notebooks/
│  ├─ 01_data_loading.ipynb
│  ├─ 02_build_signatures_and_state_vectors.ipynb
│  └─ 03_EMT_to_MET_state_transition_full.ipynb
├─ src/
│  ├─ __init__.py
│  ├─ scoring.py           # state transition scoring functions
│  ├─ sequential.py        # sequential and combination scoring
│  ├─ plotting.py          # plotting utilities
│  └─ utils.py             # helper functions
└─ results/
   └─ EMT_MET_MCF7/
      └─ MCF7_EMT_to_Epithelial/
         ├─ MET_single_step.csv
         ├─ MET_sequential_combos.csv
         ├─ MET_score_hist.png
         ├─ MET_top30_lollipop.png
         ├─ MET_top_bottom_strip.png
         ├─ MET_top20_gene_heatmap.png
         ├─ MET_top_combos_heatmap.png
         ├─ MET_sequential_scatter.png
         └─ MET_PCA_labeled.png

