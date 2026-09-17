# Fig. 22 -- hf_density_two_qps_filling1_3.pdf and hf_density_two_qps_filling2_5.pdf

Two quasiparticles: HF (single-Slater-determinant, vortex-dressed) density
(red/semi-transparent in the figure) overlaid on the conventional
flux-dressed density (black reference), both fillings: nu = 1/3 (N = 80,
omega = 15.0 lB) and nu = 2/5 (N = 80, omega = 18.0 lB), each k1 = 0,
k2 in {0,1,2}.

- Source script:
  `manuscript-repo/scripts/plot_hf_density.jl`
  (deleted from the working tree; recovered with
  `git -C authors-files/Overleaf/braiding_phase_mystery show 02f36ae4d3f601428695d0d45091dea66d62a8bd:scripts/plot_hf_density.jl`,
  commit `02f36ae4d3f601428695d0d45091dea66d62a8bd`, 2026-07-21),
  `make_hf_density_figure(tag="two_qps_density", ...)` calls for
  `nun=1,nud=3,omega=15.0` and `nun=2,nud=5,omega=18.0`.
- Source data:
  - HF: `manuscript-repo/post_processed_data/two_qps_density_N80_nu1_3_omega15.0_k1_0_k2_{0,1,2}_hf.jld2`,
    `.../two_qps_density_N80_nu2_5_omega18.0_k1_0_k2_{0,1,2}_hf.jld2`
  - Conventional reference (overlaid black curve, files suffixed
    `_conventional_reference.csv` here):
    `authors-code/CompositeFermionsDisk/post_processed_data/two_qps_density_N80_nu1_3_omega15.0_k1_0_k2_{0,1,2}_conventional.jld2`,
    `.../two_qps_density_N80_nu2_5_omega18.0_k1_0_k2_{0,1,2}_conventional.jld2`

## Columns

| column | meaning | units |
|---|---|---|
| `x_over_lB` | disk-plane coordinate x (`"x grid"` in the source file) | ell_B |
| `density_mean_2pi_rho_lB2` | chain mean of 2*pi*rho(x,0)*ell_B^2 | dimensionless |
| `density_stderr` | standard error of the mean, across chains | dimensionless |

## Statistical method

Chain mean and standard error of the mean across chains (`post_process`
convention,
`authors-code/CompositeFermionsDisk/post_processing.jl`).
N = number of entries in `"source files"` minus `"n unhealthy skipped"`
minus `"n short skipped"`, checked directly per file:

| file | source files | unhealthy skipped | short skipped | N used |
|---|---|---|---|---|
| two_qps_density_N80_nu1_3_omega15.0..._k2_0_hf | 199 | 1 | 0 | 198 |
| two_qps_density_N80_nu1_3_omega15.0..._k2_1_hf | 200 | 0 | 0 | 200 |
| two_qps_density_N80_nu1_3_omega15.0..._k2_2_hf | 198 | 1 | 1 | 196 |
| two_qps_density_N80_nu2_5_omega18.0..._k2_{0,1,2}_hf | 200 | 0 | 0 | 200 |
| conventional reference files (all six) | 200 | -- | -- | 200 |

Only chain means and their standard errors are stored, not individual chain
traces.

Note: the rendered figure applies the same cosmetic smoothing filter as
Fig. 11 (`smooth_density`) to both curves; these CSVs hold the raw,
unsmoothed chain mean/stderr.
