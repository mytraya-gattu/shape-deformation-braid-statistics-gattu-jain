# Fig. 16: flux-dressed two-anyon density

Density `2 pi rho(x,0) lstar^2` along the x axis for the flux-dressed two-anyon state corresponding to Eq. (94), one anyon at the origin (k1 = 0) and the other at omega = 10 lstar in the k state, alpha = 0, 2/7, 2/5, 2/3 and k = 0, 1, 2 (Metropolis Monte Carlo).

Files: `alpha{0.0,0.286,0.4,0.667}_k{0,1,2}.csv`.

Columns: `x_over_lstar`, `density_mean_2pi_rho_lstar2`, `density_stderr`.

Error: mean and standard error over 30 independent chains. The curves in the figure are shifted vertically by 0.2 per alpha for display; the values here are unshifted.

Script: `plot_corrected_two_anyon_density_by_alpha_and_k.jl` (repository `two_anyon_corrected`).
