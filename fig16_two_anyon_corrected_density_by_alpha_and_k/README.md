# Fig. 16: flux-dressed two-anyon density

Density `2 pi rho(x,0) lstar^2` along the x axis for the flux-dressed two-anyon state of Eq. (94), with one anyon at the origin (k1 = 0) and the other at omega = 10 lstar in state k, for alpha = 0, 2/7, 2/5, 2/3 and k = 0, 1, 2. Results obtained via Monte Carlo integration.

## Files
`alpha<alpha>_k<k>.csv` for alpha in {0.0, 0.286, 0.4, 0.667} and k in {0, 1, 2}.

## Columns
1. `x / lstar`: position along the x axis
2. `nu(x, 0) = 2 pi rho(x,0) lstar^2`: filling factor / density
3. `Delta nu`: standard error

The curves in the paper are shifted vertically by 0.2 per alpha for display; values here are unshifted.
