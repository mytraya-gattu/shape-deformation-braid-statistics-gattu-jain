# Fig. 24 -- hf_density_three_qhs_filling1_3.pdf

Three quasiholes at nu = 1/3 (N = 64) on an equilateral triangle of side
d = 7.5 lB, shapes k = (0,0,0) [reference] and k = (0,0,1) [top hole given
the k = 1 shape]. Panel (a) is the conventional 2-D density map for
k = (0,0,1); panel (b) is the HF map for the same k. This directory exports
the three raw maps that feed those panels and the deformation report: the
k = (0,0,0) reference (identical for HF and conventional by construction),
the k = (0,0,1) conventional map (panel a), and the k = (0,0,1) HF map
(panel b). The difference maps rho_k=(0,0,1) - rho_k=(0,0,0) discussed
quantitatively in the text (via `report_three_qh_numbers`) are not plotted
in the figure itself (per the script's comment) and are not separately
exported here -- they can be reconstructed as
`three_qhs_density_..._k001_*.csv` minus `..._k000_conventional.csv` on
this same (x,y) grid.

- Source script:
  `manuscript-repo/scripts/plot_three_qh_density.jl`
  (deleted from the working tree; recovered with
  `git -C authors-files/Overleaf/braiding_phase_mystery show 02f36ae4d3f601428695d0d45091dea66d62a8bd:scripts/plot_three_qh_density.jl`,
  commit `02f36ae4d3f601428695d0d45091dea66d62a8bd`, 2026-07-21),
  `make_three_qh_figure(7.5)` -> panels (a),(b) from
  `load_three_qh_map(7.5, "001", "conventional")` and
  `load_three_qh_map(7.5, "001", "hf")`.
- Source data (d = 7.5 lB set only; the script also has a d = 12.0
  far-hedge variant not requested here):
  `manuscript-repo/post_processed_data/three_qhs_density_N64_nu1_3_d7.5_k000_conventional.jld2` (reference, k = (0,0,0)),
  `.../three_qhs_density_N64_nu1_3_d7.5_k001_conventional.jld2` (panel a),
  `.../three_qhs_density_N64_nu1_3_d7.5_k001_hf.jld2` (panel b)

## Files

Three long-format CSVs (one row per (x,y) grid point, 186 x 186 = 34596
rows each), plus a small companion `*_omegas.csv` per map giving the
intended quasihole positions used to draw the white crosses in the figure.

## Columns (density CSVs)

| column | meaning | units |
|---|---|---|
| `x_over_lB` | disk-plane coordinate x (`"x centers"`) | ell_B |
| `y_over_lB` | disk-plane coordinate y (`"y centers"`) | ell_B |
| `density_mean_2pi_rho_lB2` | chain mean of 2*pi*rho(x,y)*ell_B^2 (`"density mean"`, labeled `2*pi*rho*ell_B^2` on the figure colorbar) | dimensionless |
| `density_stderr` | standard error of the mean, across chains | dimensionless |

## Columns (omegas CSVs)

| column | meaning | units |
|---|---|---|
| `qh_index` | index into the three quasiholes (1,2,3) | -- |
| `re_omega_over_lB` | Re(omega), quasihole position in the complex disk plane | ell_B |
| `im_omega_over_lB` | Im(omega) | ell_B |
| `k` | shape index k for that quasihole (`"ks"`) | -- |

The three intended positions are identical across the reference, conventional,
and HF files (verified numerically: all three `*_omegas.csv` files here have
the same three (re, im, k) triples).

## Statistical method

Chain mean and standard error of the mean across N = 48 Monte Carlo chains
for all three source files (number of entries in `"source files"`, with
`"n unhealthy skipped"` = 0 and `"n short skipped"` = 0 in each; see
`post_process` in
`authors-code/CompositeFermionsDisk/post_processing.jl` for
the underlying mean/stderr convention). Only the chain mean and its
standard error are stored per grid point, not the 48 individual chain
traces.
