# Figs. 6-7 — gaussian_impurity_pseudopotentials.pdf, coulomb_impurity_pseudopotentials.pdf

Source script: `authors-code/braiding_phase_mystery/impurity_pseudopotentials.jl`
(read-only; not modified. Export script: `/private/tmp/claude-501/-Users-aragorn-Documents-code/dfadeb1e-d236-43b5-941b-d7d021d134cc/scratchpad/data/export/export_fig06_07_impurity.jl`)

Source data (read-only, not modified): `V1data_clean.csv` (Gaussian, 60 rows),
`V2data_clean.csv` (Coulomb, 60 rows), both in
`authors-code/braiding_phase_mystery/`.

## Method

**Tabulated data.** `impurity_pseudopotentials.jl` performs no computation of its
own — it reads pre-computed, headerless 4-column CSVs (n, m, σ-or-d, V_{n,m}) and
plots them. This export re-parses the same files with the identical column
convention and writes them with a header. The underlying V_{n,m} values were
computed upstream (not by this script, and not re-derived here) as the projected
single-particle matrix element

    V_{n,m} = ∫ d²r V(r) |η_{n,m}(r)|²                     (paper Eq. projected-potential-matrix-element)

with V(r) the Gaussian or Coulomb impurity potential defined below.

## Parameters / column meaning

Confirmed against `prl.tex` (Figs. \ref{fig:gaussian-impurity},
\ref{fig:coulomb-impurity}):
- **Gaussian** (`V1data_clean.csv` -> `gaussian_impurity_V_nm.csv`):
  V(r) = -exp(-r²/2σ²)/(2πσ²), r and σ in units of ℓ_B (magnetic length, NOT ℓ*).
  n ∈ {0,1} (LL index), m ∈ {-1,...,4}, σ/ℓ_B ∈ {0, 0.4, 0.8, 1.2, 1.6, 2}.
- **Coulomb** (`V2data_clean.csv` -> `coulomb_impurity_V_nm.csv`):
  V(r) = -1/√(r²+d²), r and d in units of ℓ_B. n ∈ {0,1}, m ∈ {-1,...,4},
  d/ℓ_B ∈ {0, 0.4, 0.8, 1.2, 1.6, 2}.

**Units of V_{n,m}**: the paper's formulas for V(r) carry no explicit e²/ε or ℏω_c
prefactor, so V_{n,m} is reported in the natural units of the stated V(r) formula
with lengths in ℓ_B, i.e. ℓ_B^-2 for the Gaussian potential and ℓ_B^-1 for the
Coulomb potential. This is stated exactly as written in the script/paper; no
additional normalization was assumed or introduced.

## Files

- `gaussian_impurity_V_nm.csv` — header comment lines (`#...`) give the potential
  and units, then `n,m,sigma_over_lB,V_nm` (8 significant digits), 60 data rows.
- `coulomb_impurity_V_nm.csv` — same format with `d_over_lB` in place of
  `sigma_over_lB`, 60 data rows.

## Verification

Round-trip check: the just-written CSVs were re-parsed (skipping the header/comment
lines) and diffed against the original in-memory arrays read from
`V1data_clean.csv`/`V2data_clean.csv`.
- Gaussian: n, m, σ columns match exactly; max |V_nm round-trip - source| = 4.9e-9
  (8-sig-fig rounding only).
- Coulomb: n, m, d columns match exactly; max |V_nm round-trip - source| = 3.7e-8
  (8-sig-fig rounding only).

No independent second method exists for this figure within scope — the data are
tabulated inputs to a plotting script, not a quantity computed here. The row
counts (60 = 2 LLs x 6 m-values x 5 σ/d-values... actually 2 n x 6 m x 5 σ = 60,
confirmed against `unique(ngrid)`, `unique(mgrid)`, `unique(σgrid)` in Julia)
match between source and export exactly.
