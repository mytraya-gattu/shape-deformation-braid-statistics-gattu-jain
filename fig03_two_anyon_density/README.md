# Figure 3: two-anyon density line cut vs α and k

Source script (defines what is plotted): `authors-code/braiding_phase_mystery/two_anyons/two_anyon_density.jl`,
function `plot_two_anyon_density`. Line-cut binning/caching machinery in the same
directory's `sampler.jl` (functions `_compute_linecut_from_samples`, `linecut_profile`,
`_accumulate_linecut!`).

Processed (mean-only) line-cut caches used for the plotted mean:
`authors-code/braiding_phase_mystery/two_anyons/processed_density/samples10x_omega10_alpha_{...}_k_{...}__linecut__v1__dx0p1__dy0p1__yminm0p25__ymax0p25.jld2`,
keys `"xgrid"`, `"rho0"`, `"metadata"` (metadata gives `dx=0.1`, `dy=0.1`,
`ymin=-0.25`, `ymax=0.25`, `n_ybins=6`, plus the source raw-file bounds used to build
the x/y bin grids).

Raw MCMC samples: `authors-code/braiding_phase_mystery/two_anyons/samples10x_omega10_alpha_*_k_*.jld2`,
12 files, ~150 MB each (~1.8 GB total). Processed one file at a time on this laptop,
freeing memory (`GC.gc()`) between files; peak transient memory per file was
approximately 300 MB (the raw file's chain arrays plus one reconstructed flat copy),
about 1% of this machine's 25.8 GB RAM — well under the 60% caution threshold.

## Unexpected data-layout finding (reported per instructions)

The task assumed the raw files might store samples as `"pooled_x"`/`"pooled_y"`, a
single flat array per file. **They do not**: in all 12 raw files, `"pooled_x"` and
`"pooled_y"` are present but **empty** (`save_samples`'s pooling step was evidently not
populated when these particular files were written). The actual samples live in
`"chain_z1"` and `"chain_z2"`, each a `Vector` of 12 independent MCMC chains of
390000 complex samples each (12 × 390000 × 2 keys = 9,360,000 total single-particle
samples per file, matching the stored metadata `n_single_particle_samples`). This is
also exactly what the production code (`two_anyon_density.jl`'s `_accumulate_linecut!`,
`SAMPLE_KEYS = ("chain_z1","chain_z2")`) reads to build the plotted line cut.

Given this, the flat sequence needed for the task's 20-contiguous-block recipe was
**reconstructed** (not invented) by concatenating, in the same order the production
code iterates them, all 12 chains of `chain_z1` back-to-back, then all 12 chains of
`chain_z2` back-to-back. This reconstruction was validated directly: histogramming the
full reconstructed sequence with the exact binning read from the cache metadata
reproduces the cached `"rho0"` to a relative error of ~7e-15 on the bulk of the grid
(points above 1% of the peak density) for every one of the 12 files — i.e. floating-
point-exact agreement, confirming the reconstruction and binning are correct. Had this
reconstruction not been possible, this directory would report means only with no error
bar, per the task's explicit fallback; that fallback was not needed here.

## Method for the standard error

1. Reconstruct the flat 9,360,000-sample sequence per file as above.
2. Split it into 20 contiguous blocks of 468000 samples each (9,360,000/20 exactly).
3. Histogram each block onto the same x/y bin grid as the cache (dx=dy=0.1,
   ymin=-0.25, ymax=0.25, n_ybins=6, same x/y grid edges from the cache metadata),
   normalizing each block the same way as `_compute_linecut_from_samples`:
   `rho0_block = (2π · 2 / (n_block_samples · dx · dy · n_ybins)) · xcounts_block`.
4. `density_stderr = std(20 block estimates) / sqrt(20)` (sample std, Julia default
   n-1 denominator).
5. The block-average mean was cross-checked against the cached `"rho0"`: relative
   error ~7e-15 on the bulk of the grid for all 12 files (see per-file numbers below) —
   i.e. the blocking is statistically consistent with the full-sample estimate to
   floating-point precision.

The reported `density_mean_2pi_rho_lstar2` column is the cached `"rho0"` (the full
9.36M-sample estimate, matching the published figure exactly), not the block-of-20
average (which agrees with it to ~7e-15 and would give an indistinguishable column at
8 significant digits).

## Normalization / display offset
`plot_two_anyon_density` plots `xgrid` (label `x/ℓ⋆`) against `ρ0 + 0.2*(alpha_idx-1)`
(label `2πρ(x,0)ℓ⋆²`) — the `+0.2*(alpha_idx-1)` is a display-only vertical offset
separating the four α curves in each k panel and is **removed** here. No mirroring is
applied for this figure (unlike Fig. 16). `ellstar = 1.0` in the sampler config, so the
stored x values are already in units of ℓ⋆ with no further rescaling needed.

## Files
12 CSVs, `alpha{0.0,0.286,0.4,0.667}_k{0,1,2}.csv`, corresponding to raw alpha tokens
0.0, 2/7=0.2857142857142857, 0.4, 2/3=0.6666666666666666 and k=0,1,2.

## Columns (8 significant digits)
- `x_over_lstar` — x/ℓ⋆ (cache `"xgrid"`).
- `density_mean_2pi_rho_lstar2` — 2πρ(x,0)ℓ⋆² (cache `"rho0"`), no display offset.
- `density_stderr` — standard error from the 20-block analysis above.

## Cross-check (full-sample reconstruction vs cache, and block-mean vs cache)
For all 12 (α,k) combinations, max relative error on the bulk of the grid
(density > 1% of peak):
- full-sequence recomputation vs cached rho0: 7.09e-15 to 7.17e-15
- 20-block average vs cached rho0: 7.20e-15 to 7.32e-15

Both are floating-point-level agreement, confirming the reconstruction, binning, and
blocking are all correct and mutually consistent.
