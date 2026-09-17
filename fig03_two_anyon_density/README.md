# Fig. 3: density of two anyons in the effective model

Density `2 pi rho(x,0) lstar^2` along the x axis for the two-anyon wave function of Eq. (10), with one anyon at the origin in the k1 = 0 state and the other at omega = 10 lstar in the k state, for alpha = 0, 2/7, 2/5, 2/3 and k = 0, 1, 2 (Metropolis Monte Carlo).

Files: `alpha{0.0,0.286,0.4,0.667}_k{0,1,2}.csv`.

Columns: `x_over_lstar`, `density_mean_2pi_rho_lstar2`, `density_stderr`.

Error: standard error over 20 contiguous blocks of the 9.36 x 10^6 samples (12 independent chains). The curves in the figure are shifted vertically by 0.2 per alpha for display; the values here are unshifted.

Script: `two_anyons/two_anyon_density.jl` (repository `braiding_phase_mystery`).
