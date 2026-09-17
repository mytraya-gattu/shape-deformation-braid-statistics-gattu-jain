# Figs. 19-20 — two_anyon_prevortex_density_qp.pdf, two_anyon_prevortex_density_qh.pdf

Source script: `authors-code/two_anyon_hf/scripts/plot_prevortex_for_paper.jl`
(read-only; not modified. Export script: `/private/tmp/claude-501/-Users-aragorn-Documents-code/dfadeb1e-d236-43b5-941b-d7d021d134cc/scratchpad/data/export/export_fig19_20_prevortex.jl`)

## Method

Pure read of cached exact-quadrature data; no computation performed at export time
and no Monte Carlo anywhere upstream. Densities were originally produced (elsewhere
in the `two_anyon_hf` pipeline) by the same exact deterministic quadrature machinery
as Figs. 4/21 (`TwoAnyonHF.density_line`), then cached to:
- `authors-code/two_anyon_hf/data/nojastrow_densities.jld2` (QP)
- `authors-code/two_anyon_hf/data/nojastrow_densities_qh.jld2` (QH)

Both files store the flux-dressed pre-vortex density Ψ_fd/(z1-z2)^α for k1=0,
k2 = k ∈ {0,1,2}, at four values of α, on a common x grid, keyed by `densities[(k1,
k2, α)]`.

**Display offset removed.** The published figure shifts each α curve upward by
0.2*(index-1) purely for visual separation of the stacked traces; that offset is
not physical and is NOT applied here. The CSVs contain the raw
`2π ρ(x,0) ℓ*²` values exactly as stored in the JLD2 cache.

## Parameters

- α ∈ {0, 2/7, 2/5, 2/3}
- k1 = 0 (fixed); k2 = k ∈ {0, 1, 2}
- ω1 = 0, ω2 = 10 ℓ* (both files)
- Mmax = 140 (basis cutoff used when the cache was generated)
- x grid: 353 points, x/ℓ* ∈ [-6, 16] (as stored; note this is wider than the
  [-5,15] axis limits drawn in the published figure — no data are dropped here)

## Files

- `two_anyon_prevortex_density_qp.csv`
- `two_anyon_prevortex_density_qh.csv`

Columns (8 significant digits):
- `x_over_lstar`: x/ℓ*
- `rho_alpha<tag>_k<k>`: 2π ρ(x,0) ℓ*² for the given (α, k), where `<tag>` is α with
  "0p" replacing the decimal point and truncated to 4 decimal digits:
  `alpha0` (α=0, the reference curve), `alpha0p2857` (α=2/7), `alpha0p4` (α=2/5),
  `alpha0p6667` (α=2/3). 12 data columns total (3 k-values x 4 α-values).

The α=0 column (`rho_alpha0_k<k>`) is simultaneously the physical α=0 curve and the
"noninteracting-shape reference" that the figure draws as a gray dashed line
underneath the α>0 curves (with the display offset); no separate reference column
is needed once the offset is removed, since the reference IS the α=0 data.

## Verification

Compared against an independently loaded copy of the same JLD2 files (loaded fresh
in a separate call, not reusing the export script's in-memory `D`/`Dqh` dict) and
against the `xs` array stored in each file:
- QP: max |CSV - direct JLD2 load| over all 12 columns x 353 rows = **5.0e-9**
- QH: max |CSV - direct JLD2 load| over all 12 columns x 353 rows = **5.0e-9**
- x-grid: exact bitwise match (0.0 deviation) in both files

Both deviations are consistent with 8-significant-digit CSV rounding, not a data
error. No independent second method exists to cross-check these cached densities
within the scope of this export (they are read verbatim, not recomputed); the
underlying exact-quadrature method is the same one cross-checked for Figs. 4/21
above.
