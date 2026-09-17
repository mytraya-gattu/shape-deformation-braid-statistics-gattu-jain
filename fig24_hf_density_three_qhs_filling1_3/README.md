# Fig. 24: three QHs at nu = 1/3, density maps

Two-dimensional density `2 pi rho lB^2` for three QHs at nu = 1/3 (N = 64) at the vertices of an equilateral triangle of side 7.5 lB, with two QHs in the k = 0 state and the third in the k = 0 or k = 1 state, for the conventional wave function and for the single-determinant (HF) wave function with the modified hole orbitals of Eq. (116) (Monte Carlo).

Files: `three_qhs_density_N64_nu1_3_d7.5_k{000,001}_conventional.csv`, `three_qhs_density_N64_nu1_3_d7.5_k001_hf.csv`; the companion `*_omegas.csv` files give the intended QH positions (columns `qh_index`, `re_omega_over_lB`, `im_omega_over_lB`, `k`).

Columns: `x_over_lB`, `y_over_lB`, `density_mean_2pi_rho_lB2`, `density_stderr`, one row per grid point.

Error: mean and standard error over 48 independent chains.

Script: `scripts/plot_three_qh_density.jl` (manuscript repository, git history).
