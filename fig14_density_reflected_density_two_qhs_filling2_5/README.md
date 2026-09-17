# Fig. 14: two QHs at nu = 2/5

Density `2 pi rho(x,0) lB^2` along the line joining two QHs at nu = 2/5, N = 80, at omega = -7.5 lB and +7.5 lB (k1 = 0, k2 = 0, 1, 2), conventional construction (Monte Carlo, CF wave functions on the disk).

Files: `density_N80_nu2_5_omega15.0_k1_0_k2_{0,1,2}_conventional.csv`. The file name gives N, nu, the intended separation (omega, in lB), k1, k2, and the construction.

Columns: `x_over_lB`, `density_mean_2pi_rho_lB2`, `density_stderr`.

Error: mean and standard error over 48 independent chains. The curves in the figure are smoothed for display; the values here are the unsmoothed chain averages.

Script: `plot_post_processed_density.jl` (repository `CompositeFermionsDisk`).
