# GHZ State Preparation via Majority-Voted Boundary Measurements

**Jean-Baptiste Waring, Sébastien Le Beux, Christophe Pere**

Official implementation of *"Robust GHZ State Preparation via Majority-Voted
Boundary Measurements"* — [arXiv:2602.19405](https://arxiv.org/html/2602.19405v1).

This repository contains the reference code accompanying the paper and
reproduces **Figure 2**.

## Reproducing Figure 2

`robust_ghz_prep_via_majority_voted_boundary_measurements.ipynb` regenerates the
6-panel Figure 2 of the paper:

- **(a)–(c)** Example partitions of $N=40$, $K=20$, $L=3$ on Heavy-hex, Grid,
  and Ring topologies. Inter-cluster boundary edges are highlighted in red;
  the Ring auto-reduces $L$ to fit topological constraints.
- **(d)** Large-scale Heavy-hex partition with $N=1000$, $K=125$, $L=3$.
- **(e)** Heavy-hex bar charts of the entanglement witness $\mathcal{W}$ for
  $N\in\{30,40,50,60\}$, comparing four methods.
- **(f)** Same as (e) but on a Grid topology.

The four methods compared:

| Method | Description |
|--------|-------------|
| **Unitary** | Logarithmic CNOT-tree GHZ ($O(\log N)$ depth, no measurements). |
| **Line-Dynamic** | Bell-pair chain + mid-circuit measure + classical feedforward (Bäumer et al., PRX Quantum 2024). |
| **Group-MV $L=1$** | Cluster GHZ + single-link boundary measurement (no protection). |
| **Group-MV $L=3$** | Cluster GHZ + majority vote over 3 redundant boundary links. |

The witness reads
$\mathcal{W} = \tfrac{1}{2}\bigl(P(0^N) + P(1^N) + \langle X^{\otimes N}\rangle\bigr)$
and is a lower bound on GHZ fidelity.

## Running

```bash
uv sync
uv run jupyter notebook
# open robust_ghz_prep_via_majority_voted_boundary_measurements.ipynb
```

Two run modes (`MODE = "..."` in the first code cell):

| Mode   | $N_{\text{TRIALS}}$ | Shots/witness | Wall time |
|--------|---------------------|---------------|-----------|
| `fast` | 3                   | 4 000         | ~2 min    |
| `full` | 10                  | 12 000        | ~30–60 min |

`full` reproduces the paper's figure values.

## Outputs

- `figures/repro_figure2.{pdf,png}` — the 6-panel Figure 2 reproduction.
- `figures/repro_figure2_data_<MODE>.json` — aggregated witness values per
  (topology, $N$, method).
- `figures/repro_fidelity_validation.json` — the §IV-D fidelity-validation
  results at $N=30$ on Heavy-hex.
- The validation cell (§15) reproduces paper §IV-D: a stabilizer-sampling
  fidelity check at $N=30$ on Heavy-hex.
- The correctness check (§16) verifies all four methods produce a true GHZ
  state on a noise-free backend.

## Citation

If you use this code, please cite:

```bibtex
@article{waring2026ghz,
  title  = {Robust GHZ State Preparation via Majority-Voted Boundary Measurements},
  author = {Waring, Jean-Baptiste and Le Beux, S{\'e}bastien and Pere, Christophe},
  journal = {arXiv preprint arXiv:2602.19405},
  year   = {2026},
  url    = {https://arxiv.org/html/2602.19405v1}
}
```
