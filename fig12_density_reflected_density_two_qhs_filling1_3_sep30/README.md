# Fig. 12: two QHs at nu = 1/3 at larger separation

Density `2 pi rho(x,0) lB^2` along the line joining two QHs at nu = 1/3 with N = 144, at omega = -15 lB and +15 lB (k1 = 0, k2 = 0, 1, 2), conventional construction (Monte Carlo). The files at separations 12 lB and 24 lB, used in the text for the 1/d decay of the deformation, are included as well.

Files: `density_N144_nu1_3_omega{12.0,24.0,30.0}_k10_k2{0,1,2}_conventional.csv` (omega = total separation in lB).

Columns: `x_over_lB`, `density_mean_2pi_rho_lB2`, `density_stderr`.

Error: leave-one-out jackknife over the independent chains (48 per file).

Script: `scripts/plot_two_qh_far_separation.jl` (manuscript repository, git history).
