# Figs. 6 and 7: single-electron energies in impurity potentials

Energies `V_{n,m}` of an electron in the n-th Landau level and angular-momentum-m orbital about the impurity. Results obtained analytically.

## Files
- `gaussian_impurity_V_nm.csv` (Fig. 6: Gaussian impurity `V(r) = -exp(-r^2/2 sigma^2) / (2 pi sigma^2)`)
- `coulomb_impurity_V_nm.csv` (Fig. 7: Coulomb impurity `V(r) = -1 / sqrt(r^2 + d^2)`)

## Columns
- **Gaussian (`gaussian_impurity_V_nm.csv`)**:
  1. `n`: Landau level index
  2. `m`: angular momentum index
  3. `sigma / lB`: impurity width
  4. `V_{n,m}`: energy in units of `lB^-2`
- **Coulomb (`coulomb_impurity_V_nm.csv`)**:
  1. `n`: Landau level index
  2. `m`: angular momentum index
  3. `d / lB`: setback distance
  4. `V_{n,m}`: energy in units of `lB^-1`
