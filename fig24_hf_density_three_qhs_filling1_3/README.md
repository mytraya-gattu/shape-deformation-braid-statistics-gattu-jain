# Fig. 24: three QHs at nu = 1/3, density maps

Two-dimensional density `2 pi rho(x,y) lB^2` for three quasiholes at nu = 1/3 (N = 64) at the vertices of an equilateral triangle of side 7.5 lB, comparing conventional and single-determinant (Eq. 116) wave functions. Results obtained via Monte Carlo integration.

## Files
- Density grids: `three_qhs_density_N64_nu1_3_d7.5_k{000,001}_conventional.csv`, `three_qhs_density_N64_nu1_3_d7.5_k001_hf.csv`
- Quasihole positions: companion `*_omegas.csv` files

## Columns
- **Density files**:
  1. `x / lB`: x coordinate
  2. `y / lB`: y coordinate
  3. `2 pi rho lB^2`: density (mean)
  4. `Delta (2 pi rho)`: standard error
- **Position files (`*_omegas.csv`)**:
  1. Quasihole index (1, 2, 3)
  2. `Re(omega) / lB`
  3. `Im(omega) / lB`
  4. `k`: angular momentum state
