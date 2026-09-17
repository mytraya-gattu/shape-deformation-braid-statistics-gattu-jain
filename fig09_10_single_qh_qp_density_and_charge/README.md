# Figures 9 and 10: single quasihole/quasiparticle density and enclosed charge

Also used for Fig. 8 (same ν=1/3, N=64 data as the qh_nu1_3/qp_nu1_3 files below;
not duplicated in a separate directory).

Source script: `authors-code/braiding_phase_mystery/plotting_single_qh_qp.jl`
(function `get_density`, and the `for (N,n,defect_type,xmax) in [...]` loop that makes
`qh_nu1_3`, `qp_nu1_3`, `qh_nu2_5`, `qp_nu2_5` panels for m/k = 0,1,2).

Source data: `authors-code/defect_densities/densities/density_{N}_particles_{filling}_filling_factor_defect_{qh,qp}_mdefect_{m}.jld2`,
keys `"r grid"`, `"mean density"`, `"std density"`. These are themselves post-processed
from raw MCMC chains by `authors-code/defect_densities/post_processing.jl`
(`mean_density`, `std_density = std(chains)/sqrt(n_chains-1)`, i.e. `"std density"` in the
jld2 is already a standard error over chains, not a per-sample standard deviation).

## Files

One CSV per (filling, defect type, m): `{qh,qp}_nu{n}_{d}_mdefect_{m}.csv`, 12 files:
- `qh_nu1_3_mdefect_{0,1,2}.csv`, `qp_nu1_3_mdefect_{0,1,2}.csv` — N=64, n=1, p=2, ν=1/3
- `qh_nu2_5_mdefect_{0,1,2}.csv`, `qp_nu2_5_mdefect_{0,1,2}.csv` — N=80, n=2, p=2, ν=2/5

## Columns (8 significant digits)

- `r_over_lB` — radial coordinate r/ℓ_B (the jld2 `"r grid"`, already in these units).
- `density_mean_2pi_rho_lB2` — 2πρ(r)ℓ_B², i.e. the quantity plotted on the density axis.
  Equal to jld2 `"mean density"` + ν, exactly as `plotting_single_qh_qp.jl` does
  (`lines!(ax1, rgrid, ρsingle .+ ν; ...)`); the raw `"mean density"` field is ν-subtracted
  at the post-processing stage.
- `density_stderr` — standard error of `density_mean_2pi_rho_lB2`, equal to the jld2
  `"std density"` field unchanged (adding the constant ν does not change the stderr).
- `Q_mean` — enclosed-charge deviation Q(r), reproduced exactly as
  `plotting_single_qh_qp.jl`'s `get_density`:
  `Q = (qh) ? (N - p*n/(p*n+1)) / (2ν) : (N + p*n/(p*n+1)) / (2ν)` (computed with exact
  rational arithmetic, then converted to Float64),
  `dc = step(LinRange(-1.0, 1.0, 1000))` (= 2/999, fixed, independent of N),
  `Q(r) = cumsum("mean density" .* Q .* dc)`.
- `Q_stderr` — propagated from `density_stderr` through the same cumulative sum,
  **assuming the 1000 r-grid bins are statistically independent**:
  `Q_stderr[i] = |Q| * dc * sqrt(cumsum(density_stderr.^2))[i]`.
  This is an approximation: the underlying MCMC density estimate is a smooth histogram,
  so adjacent bins are correlated and this assumption likely understates the true
  error on Q(r) at large r. Flagged here, not corrected.

## ν and Q per file
- qh_nu1_3, qp_nu1_3: N=64, n=1, p=2, ν=1/3, Q=95 (qh) / 97 (qp)
- qh_nu2_5, qp_nu2_5: N=80, n=2, p=2, ν=2/5, Q=99 (qh) / 101 (qp)

## Number of MCMC chains behind "std density"
The raw per-chain files that `post_processing.jl` averages over are not present on this
machine as individual files; only an archive `defect_densities/mcmc_data_defects_densities.tar.gz`
exists, and it contains **only the ν=1/3 (N=64) combinations** — 50 chain files per
(defect type, m). For the ν=1/3 CSVs here, n_chains=50 is therefore directly verified
from the archive. For the ν=2/5 (N=80) CSVs, the corresponding raw per-chain archive is
not present on this machine, so n_chains cannot be independently verified here; by
pipeline convention (same `post_processing.jl`, `for chain_number in 1:100`, keeping
existing files) it is presumably comparable but this is **unverified**.

## Cross-check
`qh_nu1_3_mdefect_0.csv` was reloaded and compared against a fresh re-evaluation of the
transform above from the source jld2: max relative error 4.7e-8 (r), 2.7e-8 (density),
max absolute error 5.0e-9 (Q_mean) — consistent with the 8-significant-digit text
formatting (not a computation bug).
