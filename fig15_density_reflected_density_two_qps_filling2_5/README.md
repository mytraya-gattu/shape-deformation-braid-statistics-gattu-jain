# Fig. 15 -- density_reflected_density_two_qps_filling2_5.pdf

Two quasiparticles at nu = 2/5 (N = 80, omega = 18.0 lB, k1 = 0, k2 in
{0,1,2}), conventional construction. Same layout/convention as Fig. 11.

- Source script:
  `authors-code/CompositeFermionsDisk/plot_post_processed_density.jl`
  (the `let` block producing `density_reflected_density_two_qps_filling2_5.pdf`,
  `density_tag = "two_qps_density"`, `N=80, omega=18.0`).
- Source data:
  `authors-code/CompositeFermionsDisk/post_processed_data/two_qps_density_N80_nu2_5_omega18.0_k1_0_k2_{0,1,2}_conventional.jld2`

## Columns

| column | meaning | units |
|---|---|---|
| `x_over_lB` | disk-plane coordinate x | ell_B |
| `density_mean_2pi_rho_lB2` | chain mean of 2*pi*rho(x,0)*ell_B^2 | dimensionless |
| `density_stderr` | standard error of the mean, across chains | dimensionless |

## Statistical method

Chain mean and standard error of the mean across N = 200 Monte Carlo chains
(number of entries in `"source files"`; see `post_process` in
`authors-code/CompositeFermionsDisk/post_processing.jl`).
Only the chain mean and its standard error are stored, not the 200
individual chain traces.

Note: the rendered figure applies the same cosmetic smoothing filter as
Fig. 11 (`smooth_density`); this CSV holds the raw, unsmoothed chain
mean/stderr.
