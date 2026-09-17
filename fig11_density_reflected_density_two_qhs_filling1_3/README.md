# Fig. 11 -- density_reflected_density_two_qhs_filling1_3.pdf

Two quasiholes at nu = 1/3 (N = 64, omega = 12.0 lB, k1 = 0, k2 in {0,1,2}),
conventional (flux-dressed single-excitation-sum) construction. Panel row
k2 = 0, 1, 2 top to bottom. The figure overlays a semi-transparent red
mirror-reflection of the density inside a hand-picked localization window as
a shape-distortion guide; that reflected curve is derived from the same
density column (not separate data) and is not stored here.

- Source script: `authors-code/CompositeFermionsDisk/plot_post_processed_density.jl`
  (the `let` block ending in
  `density_reflected_density_two_qhs_filling$(numerator_nu)_$(denominator_nu).pdf`
  with `N=64, omega=12.0`).
- Source data:
  `authors-code/CompositeFermionsDisk/post_processed_data/density_N64_nu1_3_omega12.0_k1_0_k2_{0,1,2}_conventional.jld2`

## Columns

| column | meaning | units |
|---|---|---|
| `x_over_lB` | disk-plane coordinate x | ell_B |
| `density_mean_2pi_rho_lB2` | chain mean of 2*pi*rho(x,0)*ell_B^2 -- the quantity plotted on the y-axis, per the `Label(...)` call in the source script | dimensionless |
| `density_stderr` | standard error of the mean, across chains | dimensionless |

## Statistical method

Chain mean and standard error of the mean across N = 48 Monte Carlo chains
(`post_process` in
`authors-code/CompositeFermionsDisk/post_processing.jl`:
variance computed over chain means, then divided by sqrt(N-1)). N = number
of entries in the `"source files"` key of the source `.jld2` (48 for every
file in this directory). Only the chain mean and its standard error are
stored here; the 48 individual chain traces are not included.

Note: the rendered figure additionally applies a cosmetic smoothing filter
(outlier clipping + 5-point rolling median + Gaussian, sigma = 1.2 bins; see
`smooth_density` in the source script) purely for visual clarity. The CSV
here holds the raw, unsmoothed chain mean/stderr from the `.jld2` file,
which is the statistically meaningful released quantity.
