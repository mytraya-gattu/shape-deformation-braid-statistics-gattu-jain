# Fig. 4 — two_anyon_hf_det_density_qp.pdf

Source script: `authors-code/two_anyon_hf/scripts/plot_hf_det_before_after_qp.jl`
(read-only; not modified. Export script that reproduces its arrays:
`/private/tmp/claude-501/-Users-aragorn-Documents-code/dfadeb1e-d236-43b5-941b-d7d021d134cc/scratchpad/data/export/export_fig04_qp.jl`)

## Method

Exact deterministic quadrature (Laguerre-polynomial LLL orbital recurrences +
Cartesian-grid 2D quadrature for the vortex-attached density); no Monte Carlo,
no randomness. Runs in a few seconds.

Two orthonormal HF orbitals are built from the analytic inverse-vortex-packet
formula (`inverse_vortex_pair`, exact to O(1/|ω1-ω2|)), combined into a Slater
determinant (`det_state`). The single-particle density along the x-axis
(`density_line`) is computed exactly via the reduced density matrix in the
η_{0,m} basis (no truncation error beyond the basis cutoff mp_max). The
"after vortex attachment" curve multiplies the determinant by (z1-z2)^α and
recomputes the density by 2D Cartesian quadrature (`density_line_vortex`,
Cartesian grid ±16 ℓ*, 321×321 points).

## Parameters

- α = 2/3 (statistical exponent)
- ω1 = 0, ω2 = 10 ℓ* (first anyon at origin, second at ω)
- k1 = 0 (fixed); k2 = k ∈ {0, 1, 2} (one CSV per panel)
- mp_max = 180 (single-particle orbital truncation for the determinant/vortex orbitals)
- Mmax = 160 (basis cutoff for the noninteracting reference state)
- x grid: 361 points, x/ℓ* ∈ [-5, 15]
- Vortex-density quadrature workspace: Cartesian grid ±16 ℓ*, 321×321 points

## Files

One CSV per panel (k = 0, 1, 2): `panel_k0.csv`, `panel_k1.csv`, `panel_k2.csv`.

Columns (8 significant digits):
- `x_over_lstar`: x/ℓ*
- `density_noninteracting`: 2π ρ(x,0) ℓ*² for the noninteracting (gray dashed) reference,
  `state_noninteracting(0, k, ω1, ω2; Mmax=160)`
- `density_before_vortex`: 2π ρ(x,0) ℓ*² for the HF determinant BEFORE vortex attachment
  (black curve)
- `density_after_vortex`: 2π ρ(x,0) ℓ*² for the HF determinant AFTER vortex attachment
  (orange curve)

## Verification

The export script's arrays were compared against an independent regeneration of
the actual figure: the original script was copied byte-for-byte into scratch with
only the output directory changed (never touching the tracked original at
`authors-code/two_anyon_hf/scripts/plot_hf_det_before_after_qp.jl`),
run to completion (figure saved to
`/private/tmp/claude-501/.../scratchpad/data/export/verify_out/two_anyon_hf_det_density_qp.pdf`),
and its in-memory `curves` dict diffed against the CSVs.

Max absolute deviation across all 3 panels x 3 curves x 361 points: **4.4e-7**,
consistent with the 8-significant-digit rounding of the CSV (not a physics
discrepancy — verified against the unrounded double-precision values held in
memory during the same run).

No cross-check against an independent method (e.g. a different basis/algorithm)
was performed beyond this reproduction; the underlying physics cross-check
(HF-vs-flux-dressed exactness) is done for the QH companion figure (Fig. 21),
where the script itself asserts agreement to 1e-10.
