# Figs. 9 and 10 (and the curves of Fig. 8): single QH and QP density and integrated charge

Density `2 pi rho(r) lB^2` and integrated charge Q(r) of a single localized QH or QP at nu = 1/3 (N = 64) and nu = 2/5 (N = 80), in the angular-momentum state m = 0, 1, 2 about the origin (Monte Carlo).

Files: `{qh,qp}_nu{1_3,2_5}_mdefect_{0,1,2}.csv`.

Columns: `r_over_lB`, `density_mean_2pi_rho_lB2`, `density_stderr`, `Q_mean`, `Q_stderr` (Q in units of the electron charge).

Error: mean and standard error over independent chains (50 chains at nu = 1/3). `Q_stderr` is propagated from the density error through the radial integral treating bins as independent.

Script: `plotting_single_qh_qp.jl` (repository `braiding_phase_mystery`); densities from `defect_densities`.
