# Fig. 17 -- density_two_qps_filling1_3.pdf and density_two_qps_filling2_5.pdf

Two quasiparticles, conventional (flux-dressed single-excitation-sum,
red/semi-transparent in the figure) vs. corrected (black) density, for both
fillings shown side by side in the manuscript: nu = 1/3 (N = 80,
omega = 15.0 lB) and nu = 2/5 (N = 80, omega = 18.0 lB), each k1 = 0,
k2 in {0,1,2}.

- Source script:
  `authors-code/CompositeFermionsDisk/plot_post_processed_density.jl`
  (the two `let` blocks ending in `density_two_qps_filling1_3.pdf` /
  `density_two_qps_filling2_5.pdf`, `density_tag = "two_qps_density"`).
- Source data:
  `authors-code/CompositeFermionsDisk/post_processed_data/two_qps_density_N80_nu1_3_omega15.0_k1_0_k2_{0,1,2}_{conventional,corrected}.jld2`,
  `authors-code/CompositeFermionsDisk/post_processed_data/two_qps_density_N80_nu2_5_omega18.0_k1_0_k2_{0,1,2}_{conventional,corrected}.jld2`

## Columns

| column | meaning | units |
|---|---|---|
| `x_over_lB` | disk-plane coordinate x | ell_B |
| `density_mean_2pi_rho_lB2` | chain mean of 2*pi*rho(x,0)*ell_B^2 (conventional or corrected family, per filename) | dimensionless |
| `density_stderr` | standard error of the mean, across chains | dimensionless |

## Statistical method

Chain mean and standard error of the mean across chains (see
`post_process` in
`authors-code/CompositeFermionsDisk/post_processing.jl`);
N = 200 chains for every file in this directory (number of entries in
`"source files"`). Only the chain mean and its standard error are stored,
not the 200 individual chain traces.

Note: the rendered figure applies the same cosmetic smoothing filter as
Fig. 11 (`smooth_density`) to both curves; this CSV holds the raw,
unsmoothed chain mean/stderr for whichever family (`conventional` or
`corrected`) the filename names.
