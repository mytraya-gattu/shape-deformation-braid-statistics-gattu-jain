# Fig. 21 — two_anyon_hf_det_density_qh.pdf

Source script: `authors-code/two_anyon_hf/scripts/plot_hf_det_before_after_qh.jl`
(read-only; not modified. Export script that reproduces its arrays:
`/private/tmp/claude-501/-Users-aragorn-Documents-code/dfadeb1e-d236-43b5-941b-d7d021d134cc/scratchpad/data/export/export_fig21_qh.jl`)

## Method

Exact deterministic quadrature; no Monte Carlo. Mirror of Fig. 4 but for two QHs:
the two orbitals are the dressed-hole finite lowering series `chi_vec(k, ωa, ωb, α,
mp)` (per-orbital factor (ωa-ωb)/√2), combined into a Slater determinant. For k1=0
the determinant coincides with the flux-dressed two-QH pre-vortex state
(`state_nojastrow_qh`) to machine precision; the script asserts
`maximum(abs, before - ρ_fd) < 1e-10` before proceeding, so the "before" curves here
are simultaneously the HF-determinant density and the flux-dressed pre-vortex density.

## Parameters

- α = 2/3
- ω1 = 0, ω2 = 10 ℓ*
- k1 = 0 (fixed); k2 = k ∈ {0, 1, 2} (one CSV per panel)
- mp_max = 180
- Mmax = 160 (noninteracting reference and flux-dressed exactness check)
- x grid: 361 points, x/ℓ* ∈ [-5, 15]
- Vortex-density quadrature workspace: Cartesian grid ±16 ℓ*, 321×321 points

## Files

One CSV per panel (k = 0, 1, 2): `panel_k0.csv`, `panel_k1.csv`, `panel_k2.csv`.

Columns (8 significant digits):
- `x_over_lstar`: x/ℓ*
- `density_noninteracting`: 2π ρ(x,0) ℓ*² noninteracting reference
- `density_before_vortex`: 2π ρ(x,0) ℓ*² HF determinant before vortex attachment
  (= flux-dressed pre-vortex density to < 1e-10, checked below)
- `density_after_vortex`: 2π ρ(x,0) ℓ*² HF determinant after vortex attachment

## Verification

1. **Exactness check performed by the script itself** (both in the export run and
   in an independent regeneration of the actual figure from an unmodified-content
   copy of the original script, only the output directory changed):
   `max|ρ_det,before(x) - ρ_fluxdressed,prevortex(x)|` over the 361-point x grid —
   - k=0: 3.75e-16
   - k=1: 2.57e-16
   - k=2: 1.53e-16

   i.e. the HF-determinant "before" curve and the flux-dressed pre-vortex curve
   agree to double-precision roundoff, exactly as the script requires (it would
   `error()` otherwise).

2. Export-script CSV values vs. the independently regenerated figure's in-memory
   arrays: max absolute deviation across all 3 panels x 3 curves x 361 points =
   **5.0e-9**, consistent with 8-significant-digit CSV rounding.

The original script was never edited in place; a byte-identical copy (outdir line
changed, plus one added `global` stash of the `curves` dict for comparison) was
run from
`/private/tmp/claude-501/-Users-aragorn-Documents-code/dfadeb1e-d236-43b5-941b-d7d021d134cc/scratchpad/data/export/verify_qh_copy.jl`,
producing
`/private/tmp/claude-501/-Users-aragorn-Documents-code/dfadeb1e-d236-43b5-941b-d7d021d134cc/scratchpad/data/export/verify_out/two_anyon_hf_det_density_qh.pdf`.
