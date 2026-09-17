# shape-deformation-braid-statistics-gattu-jain

Processed numerical data for the paper *Shape Deformation and Braid Statistics of Fractional Quantum Hall Quasiparticles* (Mytraya Gattu and Jainendra K. Jain, 2026). One directory per data figure of the paper, named `figNN_<figure file>` after the figure file in the manuscript source. Schematics (Figs. 1, 2, 5, 8) are not included; Fig. 8 overlays the same single-quasihole densities that are released for Fig. 9.

Format: plain CSV, one header line naming the columns, then numbers (8 significant digits). Lengths are in units of the magnetic length `lB` (microscopic data) or the effective magnetic length `lstar` (two-anyon model); densities are `2 pi rho lB^2` or `2 pi rho lstar^2` as on the figure axes. For Monte Carlo quantities the columns are the mean over independent chains and its standard error; for exact (quadrature or closed-form) quantities only the value is given. Curves that the figures shift vertically or smooth for display are stored unshifted and unsmoothed; each README says what the plotting script does on top. Only chain means and errors are stored, not per-chain traces.

## Directory guide

| Directory | Paper figure | Content | Method |
|---|---|---|---|
| `fig03_two_anyon_density` | Fig. 3 | two-anyon line-cut densities, alpha in {0, 2/7, 2/5, 2/3}, k = 0, 1, 2 | Monte Carlo, 20-block standard error |
| `fig04_two_anyon_hf_det_density_qp` | Fig. 4 | single-determinant two-QP densities before/after vortex attachment | exact quadrature |
| `fig06_07_impurity_pseudopotentials` | Figs. 6, 7 | Gaussian and Coulomb impurity matrix elements V_{n,m} | exact |
| `fig09_10_single_qh_qp_density_and_charge` | Figs. 8, 9, 10 | single QH/QP densities and integrated charge Q(r), nu = 1/3, 2/5 | Monte Carlo |
| `fig11_density_reflected_density_two_qhs_filling1_3` | Fig. 11 | two-QH densities, nu = 1/3, d = 12 lB | Monte Carlo |
| `fig12_density_reflected_density_two_qhs_filling1_3_sep30` | Fig. 12 | two-QH densities, nu = 1/3, d = 12, 24, 30 lB (N = 144) | Monte Carlo, jackknife |
| `fig13_density_reflected_density_two_qps_filling1_3` | Fig. 13 | two-QP densities, nu = 1/3 | Monte Carlo |
| `fig14_density_reflected_density_two_qhs_filling2_5` | Fig. 14 | two-QH densities, nu = 2/5 | Monte Carlo |
| `fig15_density_reflected_density_two_qps_filling2_5` | Fig. 15 | two-QP densities, nu = 2/5 | Monte Carlo |
| `fig16_two_anyon_corrected_density_by_alpha_and_k` | Fig. 16 | flux-dressed two-anyon densities | Monte Carlo, 30 chains |
| `fig17_density_two_qps_filling1_3_2_5` | Fig. 17 | conventional vs flux-dressed two-QP densities | Monte Carlo |
| `fig18_density_two_qhs_filling1_3_2_5` | Fig. 18 | conventional vs flux-dressed two-QH densities | Monte Carlo |
| `fig19_20_two_anyon_prevortex_density` | Figs. 19, 20 | flux-dressed two-anyon densities before vortex attachment | exact |
| `fig21_two_anyon_hf_det_density_qh` | Fig. 21 | single-determinant two-QH densities before/after vortex attachment | exact |
| `fig22_hf_density_two_qps_filling1_3_2_5` | Fig. 22 | single-determinant (HF) vs conventional two-QP densities | Monte Carlo |
| `fig23_hf_density_two_qhs_filling1_3_2_5` | Fig. 23 | single-determinant (HF) vs conventional two-QH densities | Monte Carlo |
| `fig24_hf_density_three_qhs_filling1_3` | Fig. 24 | three-QH 2-D density maps, conventional and HF | Monte Carlo |
| `fig25_26_two_qh_two_qp_norms` | Figs. 25, 26 | norms of two-QH / two-QP CF states vs relative angular momentum | Monte Carlo |
| `fig27_hf_braid_statistics` | Fig. 27 | braid statistics of the single-determinant states vs separation | exact overlaps |

Each directory's README names the script that produced the figure, the source data files, the columns and units, and the statistical method (number of chains, error definition, assumptions).

## License

CC BY 4.0, see `LICENSE`. Please cite the paper when using these data.
