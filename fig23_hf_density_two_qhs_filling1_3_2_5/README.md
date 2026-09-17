# Fig. 23: single-determinant (HF) versus conventional two QHs

Density `2 pi rho(x,0) lB^2` for two QHs at nu = 1/3 (N = 64, omega = 12 lB) and nu = 2/5 (N = 80, omega = 15 lB), k1 = 0, k2 = 0, 1, 2, for the single-determinant wave functions with the modified hole orbitals of Eq. (116) (`hf`, red curves) and the conventional wave functions (`conventional_reference`, black curves) (Monte Carlo, CF wave functions on the disk).

Files: `density_N{64,80}_nu{1_3,2_5}_omega*_k1_0_k2_{0,1,2}_{hf,conventional_reference}.csv`. The file name gives N, nu, the intended separation (omega, in lB), k1, k2, and the construction.

Columns: `x_over_lB`, `density_mean_2pi_rho_lB2`, `density_stderr`.

Error: mean and standard error over 48 independent chains. The curves in the figure are smoothed for display; the values here are the unsmoothed chain averages.

Scripts: `scripts/plot_hf_density.jl` (manuscript repository, git history) and `plot_post_processed_density.jl` (repository `CompositeFermionsDisk`).
