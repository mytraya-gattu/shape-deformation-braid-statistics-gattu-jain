# Fig. 12 -- density_reflected_density_two_qhs_filling1_3_sep30.pdf

Far-separation companion to Fig. 11 (fig:two-qh-1-3-shapes): two quasiholes
at nu = 1/3 (N = 144, k1 = 0, k2 in {0,1,2}), conventional construction, at
separation omega = 30.0 lB for the published panel. **This directory also
includes the omega = 12.0 and omega = 24.0 sets**, which are not the
published-figure data themselves but are the data the manuscript text uses
alongside omega = 30.0 to support the "density deformation decays like 1/d
with separation" claim -- see the peak-value cross-check below.

- Source script:
  `manuscript-repo/scripts/plot_two_qh_far_separation.jl`
  (deleted from the working tree; recovered with
  `git -C authors-files/Overleaf/braiding_phase_mystery show 02f36ae4d3f601428695d0d45091dea66d62a8bd:scripts/plot_two_qh_far_separation.jl`,
  commit `02f36ae4d3f601428695d0d45091dea66d62a8bd`, "HF section: state
  M-anyon orbitals explicitly; three-QH figure single-row (drop difference
  maps), honest verified anisotropy caption", 2026-07-21). The script's
  `make_far_separation_figure` is called for `sep in (24.0, 30.0)`; the
  omega = 12.0 panel is the analogous case in
  `plot_post_processed_density.jl` (CompositeFermionsDisk). All three share
  identical loader/smoother functions.
- Source data:
  `manuscript-repo/post_processed_data/density_N144_nu1_3_omega{12.0,24.0,30.0}_k10_k2{0,1,2}_conventional.jld2`

## Columns

| column | meaning | units |
|---|---|---|
| `x_over_lB` | disk-plane coordinate x (`"x centers"` in the source file) | ell_B |
| `density_mean_2pi_rho_lB2` | chain mean of 2*pi*rho(x,0)*ell_B^2 | dimensionless |
| `density_stderr` | standard error of the mean, across chains | dimensionless |

## Statistical method

Chain mean and standard error of the mean across N = 48 chains; N is stored
directly as `"n_chains"` in each source `.jld2` (all nine files here have
n_chains = 48). Only the chain mean and its standard error are stored; the
48 individual chain traces are not included.

## Cross-check: peak density vs. separation (1/d trend)

Peak of the chain-mean density in an 8 ell_B window centered on the far
quasihole at x = +omega/2 (this excludes the unrelated, larger-amplitude
Friedel-oscillation peaks at the disk edge, |x| >~ 25, which are not part of
the near-QH shape-deformation feature the text discusses):

| omega | k2=0 peak | k2=1 peak | k2=2 peak |
|---|---|---|---|
| 12.0 | 0.35456 +/- 0.00046 | 0.55762 +/- 0.00044 | 0.42644 +/- 0.00038 |
| 24.0 | 0.35416 +/- 0.00043 | 0.56144 +/- 0.00073 | 0.41184 +/- 0.00047 |
| 30.0 | 0.35428 +/- 0.00040 | 0.56272 +/- 0.00056 | 0.40940 +/- 0.00053 |

k2 = 0 is flat within error across omega (expected: k2 = 0 carries no shape
deformation). k2 = 1 and k2 = 2 shift monotonically with omega by amounts
several times the combined stderr, consistent with a deformation amplitude
decaying with separation. This export does not itself fit a 1/omega power
law -- that fit, if wanted, should be done from this table, not asserted
here.
