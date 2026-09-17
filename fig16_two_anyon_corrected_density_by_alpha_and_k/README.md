# Figure 16: two-anyon corrected density by α and k

Source script:
`authors-code/two_anyon_corrected/plot_corrected_two_anyon_density_by_alpha_and_k.jl`
(function `plot_corrected_density_by_alpha_and_k`).

Source data:
`authors-code/two_anyon_corrected/corrected_two_anyon_density_omega5.0_alpha{0.0,0.286,0.4,0.667}_k{0,1,2}.jld2`
(target α = 0, 2/7, 2/5, 2/3, matched within the script's tolerance 5e-4 to the
alpha-labelled filenames), keys used: `"omega"`, `"x_shift"`, `"xgrid shifted"`,
`"density mean"`, `"density std"`, `"num_chains"`. All 12 files have omega = x_shift = 5.0.

`"density std"` is already a **standard error**, not a per-sample standard deviation: it
is produced upstream (`two_anyon_corrected/two_anyon_density.jl`) as
`std(ρgrid_across_chains, dims=2) ./ sqrt(num_chains - 1)` over `num_chains = 30` MCMC
chains (`num_thermalize = 100000`, `num_samples = 1000000` per chain).

## Normalization and the display offset

The script plots `xgrid_shifted` on the x-axis (label `x/ℓ⋆`) and `density_mean` on the
y-axis (label `2πρℓ⋆²`) with no extra scale factor — the stored arrays are already in
these units (ellstar convention baked into the sampler, `omega_rel_convention`:
"omega_rel = sqrt(2) * omega; nominal centers at -omega and +omega").

Before plotting, the script (1) reflects the curve about x = omega,
`(x, y) -> (2*omega - x, y)` with the resulting array re-reversed to increasing x — this
is a genuine coordinate transform of the physical data (the two-anyon problem here is
symmetric under this reflection), not a cosmetic offset, and **is kept** in the exported
columns; and (2) adds a **vertical display offset** `0.20 * (alpha_idx - 1)` to separate
the four α-curves in each k-panel — this offset is **removed** in these CSVs.

## Files

One CSV per (α, k), 12 files: `alpha{0.0,0.286,0.4,0.667}_k{0,1,2}.csv`.

## Columns (8 significant digits)

- `x_over_lstar` — x/ℓ⋆, after the omega-reflection above, no display offset.
- `density_mean_2pi_rho_lstar2` — 2πρ(x,0)ℓ⋆², reflected, **no** `0.20*(alpha_idx-1)`
  vertical offset.
- `density_stderr` — the `"density std"` field (already a stderr over num_chains=30
  chains), reflected/reordered the same way as the mean (a constant additive offset,
  which was removed, does not change the stderr; the reflection is a relabelling that
  the stderr must follow to stay aligned with its x value).

## Cross-check
`alpha0.4_k1.csv` reloaded and compared against a fresh re-evaluation of the reflection
transform on the source jld2: max relative error 1.4e-14 (x), 4.9e-8 (density mean),
4.2e-8 (density stderr) — the latter two limited by the 8-significant-digit text
format, not a computation error.
