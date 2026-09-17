# Figures 25 and 26: two-quasihole / two-quasiparticle state norms vs relative angular momentum

Source script: `authors-code/braiding_phase_mystery/two_cfs_on_sphere/norm.jl`
(the two `let` blocks producing `two_qh_norms.pdf` and `two_qp_norms.pdf`).

Source data (same directory as the script):
`post_processed_two_qh_norms_N{30,60,90}_nu1_3.jld2`, `N{64,96,128}_nu2_5.jld2`,
`N{60,90,120}_nu3_7.jld2` for the QH figure, and the analogous
`post_processed_two_qps_norms_N*_nu*.jld2` files (note the source script reads the
**plural** `"...qps_norms..."` filename for quasiparticles and the **singular**
`"...qh_norms..."` filename for quasiholes — both singular and plural "qh"-named
files exist on disk, e.g. `post_processed_two_qhs_norms_*`, but the script only reads
the singular set for QH; the plural QH set is unused here and not exported).
Keys: `"x"`, `"y"`, `"dy"`.

As labelled on the script's axes:
- `x = L(L+1) / (4 L_QH(L_QH+1))` (or `L_QP` for the QP figure) — a dimensionless
  rescaled total relative angular momentum, x ∈ [0,1].
- `y = N_L = <L,M|L,M>` — the norm of the two-quasihole (or two-quasiparticle) state
  at total angular momentum L, as computed by the companion two-CF-on-sphere code.
- `dy` — standard error of `y` (as literally named/used by the script; the script does
  not distinguish `dy` from the plotted symmetric error bar, i.e. it is used directly
  as `y ± dy`).

Reference curve drawn on every panel: **(1-x)^(α/2)**, with α = 4/3 (ν=1/3), 4/5 (ν=2/5),
4/7 (ν=3/7) — i.e. α = 4/(2n+1) for n = 1,2,3 with p=1 fixed in the script.

## Important: NOT exported — a per-N rescaling applied only in the plot

Before plotting, `norm.jl` computes `constant_fix = norms_actual[1] / norms_expected[1]`
and rescales `norms_actual ./= constant_fix`, i.e. it forces the first data point of
each N-series to sit exactly on the reference curve (1-x)^(α/2) before comparing shapes.
**This rescaling is a display-only normalization choice, not part of the underlying
data, and is deliberately NOT applied here.** The CSVs below are the raw `"x"`, `"y"`,
`"dy"` exactly as stored in the jld2 files, per the task specification for this
directory. Reproducing the published figure from these CSVs requires applying the same
`constant_fix` per N.

## Files

18 CSVs, `{qh,qp}_N{N}_nu{n}_{2n+1}.csv`:
- qh: N30/60/90_nu1_3, N64/96/128_nu2_5, N60/90/120_nu3_7
- qp: N30/60/90_nu1_3, N64/96/128_nu2_5, N60/90/120_nu3_7
All 18 source files were found; none missing.

## Columns (8 significant digits)
- `x` — L(L+1)/(4 L_QH(QP)(L_QH(QP)+1)), as stored (originally `Rational{Int64}`,
  exported as a float to 8 significant digits).
- `y_mean` — the norm N_L, as stored (`"y"`).
- `y_stderr` — the standard error `"dy"`, as stored.

## Cross-check
`qp_N96_nu2_5.csv` reloaded and compared to the source jld2 `"x"`,`"y"`,`"dy"`: max
relative error 4.0e-8 (x), 2.6e-8 (y), 3.0e-8 (dy) — limited by the 8-significant-digit
text format.


## Plotted (rescaled) columns

`y_plotted` and `y_plotted_stderr` are `y_mean` and `y_stderr` divided by the per-file constant `y_mean[1] / (1 - x[1])^(alpha/2)`, i.e. the first point of each N is placed on the reference curve `(1 - x)^(alpha/2)` exactly as `norm.jl` does before plotting (`constant_fix`). These two columns reproduce the markers in the figure; `y_mean`/`y_stderr` are the raw Monte Carlo norms. The rescaling treats the first point as exact, so its own statistical error is not propagated into `y_plotted_stderr`.
