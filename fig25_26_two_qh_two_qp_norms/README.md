# Figs. 25 and 26: norms of two-QH and two-QP states on the sphere

Norms of the two-QH (Fig. 25) and two-QP (Fig. 26) CF states as a function of the relative angular momentum, at nu = 1/3, 2/5, 3/7 for several N (Monte Carlo), compared with the two-anyon prediction (1 - x)^(alpha/2), alpha = 2/3, 2/5, 2/7.

Files: `{qh,qp}_N{...}_nu{1_3,2_5,3_7}.csv`.

Columns: `x` (relative angular momentum scaled as on the horizontal axis of the figure), `y_mean`, `y_stderr` (Monte Carlo norm and its standard error), `y_plotted`, `y_plotted_stderr` (the same after the per-N rescaling used in the figure, which places the first point on the reference curve).

Script: `two_cfs_on_sphere/norm.jl` (repository `braiding_phase_mystery`).
