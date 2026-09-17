# Fig. 23 -- hf_density_two_qhs_filling1_3.pdf and hf_density_two_qhs_filling2_5.pdf

Two quasiholes: HF (single-Slater-determinant, vortex-dressed) density
(red/semi-transparent in the figure) overlaid on the conventional
flux-dressed density (black reference), both fillings: nu = 1/3 (N = 64,
omega = 12.0 lB) and nu = 2/5 (N = 80, omega = 15.0 lB), each k1 = 0,
k2 in {0,1,2}.

- Source script:
  `manuscript-repo/scripts/plot_hf_density.jl`
  (deleted from the working tree; recovered with
  `git -C authors-files/Overleaf/braiding_phase_mystery show 02f36ae4d3f601428695d0d45091dea66d62a8bd:scripts/plot_hf_density.jl`,
  commit `02f36ae4d3f601428695d0d45091dea66d62a8bd`, 2026-07-21),
  `make_hf_density_figure(tag="density", ...)` calls for
  `nun=1,nud=3,omega=12.0` and `nun=2,nud=5,omega=15.0`.
- Source data:
  - HF: `manuscript-repo/post_processed_data/density_N64_nu1_3_omega12.0_k1_0_k2_{0,1,2}_hf.jld2`,
    `.../density_N80_nu2_5_omega15.0_k1_0_k2_{0,1,2}_hf.jld2`
  - Conventional reference (overlaid black curve, files suffixed
    `_conventional_reference.csv` here):
    `authors-code/CompositeFermionsDisk/post_processed_data/density_N64_nu1_3_omega12.0_k1_0_k2_{0,1,2}_conventional.jld2`,
    `.../density_N80_nu2_5_omega15.0_k1_0_k2_{0,1,2}_conventional.jld2`

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
Checked directly per file: all six HF files have
`"source files"` length 48, `"n unhealthy skipped"` = 0, `"n short
skipped"` = 0, so N = 48; all six conventional reference files likewise
have N = 48. Only chain means and their standard errors are stored, not
individual chain traces.

Note: the rendered figure applies the same cosmetic smoothing filter as
Fig. 11 (`smooth_density`) to both curves; these CSVs hold the raw,
unsmoothed chain mean/stderr.
