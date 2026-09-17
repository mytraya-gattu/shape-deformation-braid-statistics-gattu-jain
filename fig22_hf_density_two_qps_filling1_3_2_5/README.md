# Fig. 22: single-determinant (HF) versus conventional two QPs

Density `2 pi rho(x,0) lB^2` for two QPs at nu = 1/3 (N = 80, omega = 15 lB) and nu = 2/5 (N = 80, omega = 18 lB), k1 = 0, k2 = 0, 1, 2, for the single-determinant wave functions of Eq. (112) (`hf`, red curves) and the conventional wave functions (`conventional_reference`, black curves) (Monte Carlo, CF wave functions on the disk).

Files: `two_qps_density_N80_nu{1_3,2_5}_omega*_k1_0_k2_{0,1,2}_{hf,conventional_reference}.csv`. The file name gives N, nu, the intended separation (omega, in lB), k1, k2, and the construction.

Columns: `x_over_lB`, `density_mean_2pi_rho_lB2`, `density_stderr`.

Error: mean and standard error over up to 200 independent chains. The curves in the figure are smoothed for display; the values here are the unsmoothed chain averages. For the `hf` files at nu = 1/3, 196 to 200 chains contributed after discarding unconverged ones.

Scripts: `scripts/plot_hf_density.jl` (manuscript repository, git history) and `plot_post_processed_density.jl` (repository `CompositeFermionsDisk`).
