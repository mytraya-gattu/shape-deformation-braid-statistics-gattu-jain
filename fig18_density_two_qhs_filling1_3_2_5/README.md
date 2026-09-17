# Fig. 18 -- density_two_qhs_filling1_3.pdf and density_two_qhs_filling2_5.pdf

Two quasiholes, conventional vs. corrected density, for both fillings shown
side by side: nu = 1/3 (N = 64, omega = 12.0 lB) and nu = 2/5 (N = 80,
omega = 15.0 lB), each k1 = 0, k2 in {0,1,2}.

- Source script:
  `authors-code/CompositeFermionsDisk/plot_post_processed_density.jl`
  (the two `let` blocks ending in `density_two_qhs_filling1_3.pdf` /
  `density_two_qhs_filling2_5.pdf`, `density_tag = "density"` (default)).
- Source data:
  `authors-code/CompositeFermionsDisk/post_processed_data/density_N64_nu1_3_omega12.0_k1_0_k2_{0,1,2}_{conventional,corrected}.jld2`,
  `authors-code/CompositeFermionsDisk/post_processed_data/density_N80_nu2_5_omega15.0_k1_0_k2_{0,1,2}_{conventional,corrected}.jld2`

## Columns

| column | meaning | units |
|---|---|---|
| `x_over_lB` | disk-plane coordinate x | ell_B |
| `density_mean_2pi_rho_lB2` | chain mean of 2*pi*rho(x,0)*ell_B^2 (conventional or corrected family, per filename) | dimensionless |
| `density_stderr` | standard error of the mean, across chains | dimensionless |

## Statistical method

Chain mean and standard error of the mean across N = 48 chains for every
file in this directory (number of entries in `"source files"`; see
`post_process` in
`authors-code/CompositeFermionsDisk/post_processing.jl`).
Only the chain mean and its standard error are stored, not the 48
individual chain traces.

Note: the rendered figure applies the same cosmetic smoothing filter as
Fig. 11 (`smooth_density`) to both curves; this CSV holds the raw,
unsmoothed chain mean/stderr for whichever family the filename names.
