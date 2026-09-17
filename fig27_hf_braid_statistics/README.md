# Fig. 27 — hf_braid_statistics.pdf

Source script: `authors-code/two_anyon_hf/scripts/plot_hf_braid_statistics.jl`
(read-only; not modified. Export script: `/private/tmp/claude-501/-Users-aragorn-Documents-code/dfadeb1e-d236-43b5-941b-d7d021d134cc/scratchpad/data/export/export_fig27_braid.jl`)

## Method

Exact deterministic quadrature; no Monte Carlo. ΔΘ/2π is extracted from the
infinitesimal overlap along the braid loop ω_a → ω_a e^{iδφ} (δφ = 1e-5):
Θ1/2π = Re[(⟨s(0)|s(δφ)⟩ - 1)/(iδφ)], ΔΘ/2π = Θ1/2π + (|ω1|² + |ω2|²)/4·2 (coded as
`+ d²/4`). Overlaps are exact sums over basis coefficients (`TwoAnyonHF.overlap`,
basis cutoff Mmax). Geometry: ω1 = +d/2, ω2 = -d/2 (w_rel on the positive real axis,
away from the branch cut of `angle()`). Runs in well under a minute.

QP states: HF Slater determinant from the analytic inverse-vortex-packet orbitals
with the Jastrow (z1-z2)^α reattached (`hfqp` = `attach_jastrow(det_state(...), α)`).
QH states: same construction with the dressed-hole finite lowering-series orbitals
(`hfqh`), stored in the conjugate picture, so the physical ΔΘ_QH = -ΔΘ(stored)
(sign flip applied before writing to CSV).

## Parameters

- α ∈ {2/7, 2/5, 2/3}; k1 = 0 (fixed), k2 = k ∈ {0, 1, 2}
- Mmax = 140 (basis cutoff)
- δφ = 1e-5 (finite-difference step for the infinitesimal braid)
- d/ℓ* grid: 4.0:0.5:8.0 then 9.0:1.0:18.0 (19 points; sweep starts at d=4 because
  below that the two HF orbitals are no longer well separated — |⟨f1|f2⟩| = 0.15,
  0.50, 0.72 at d = 5, 4, 3 for k=(0,2) — and ΔΘ, defined only in the
  large-separation limit, ceases to be meaningful)

## Files

- `hf_braid_statistics_qp.csv`
- `hf_braid_statistics_qh.csv`

Columns (8 significant digits):
- `d_over_lstar`: d/ℓ*
- `dTheta_over_2pi_alpha<tag>_k<k>`: ΔΘ/2π for the given (α, k), 9 columns
  (3 α-values x 3 k-values), `<tag>` as in Figs. 19-20 (`0p2857`, `0p4`, `0p6667`).

## Validation performed by the script (also reproduced by the export script)

1. **Flux-dressed QP vs. analytic α**: `dTheta(fdqp, 0, k2, α, d=14.0) ≈ α` to
   atol=1e-4, for all (α,k2) — PASSED.
2. **Conventional QP vs. analytic -α(1+k1+k2)**: `dTheta(conv, 0, k2, α, d=16.0) ≈
   -α(1+k2)` to atol=6e-2, for all (α,k2) — PASSED. This is the flux-dressed → α,
   conventional → -α(1+k1+k2) cross-check requested for this figure.
3. **Basis convergence**: HF-QP and HF-QH ΔΘ at d = max(ds) = 18.0 agree to < 1e-5
   between Mmax=140 and Mmax=180 — PASSED, for all 9 (α,k2) combinations, both QP
   and QH.

All three checks passed identically in both the export run and an independent
regeneration of the actual figure (unmodified-content copy of the original script,
only the output directory redirected to
`/private/tmp/claude-501/-Users-aragorn-Documents-code/dfadeb1e-d236-43b5-941b-d7d021d134cc/scratchpad/data/export/verify_out/`,
never touching the tracked original).

## Additional verification (this export)

The endpoint values (d=18.0) printed by both runs match to all 5 printed digits
for every (α, k2, QP/QH) combination, e.g. α=2/3, k=2: QP=0.66689, QH=0.65015 in
both runs. The exported CSV's last row reproduces these same 5-digit values
exactly after loading and rounding.
