# shape-deformation-braid-statistics-gattu-jain

Numerical data generated for the manuscript *Shape Deformation and Braid Statistics of Fractional Quantum Hall Quasiparticles* (Mytraya Gattu and Jainendra K. Jain, 2026, arXiv:2609.XXXXX), presented in Figs. 3, 4, 6, 7, and 9–27.

The remaining figures of the manuscript (Figs. 1, 2, 5, and 8) are schematic illustrations. (The density curves shown in Fig. 8 are the same as the nu = 1/3 curves of Fig. 9 and can be found in the folder for Figs. 9 and 10.)

The data are organized by figure: each folder name starts with the figure number.

## Data Format and Conventions
- **Headerless CSVs**: All data files are plain CSVs without header lines, containing comma-separated numbers ready for direct parsing (e.g. via `numpy.loadtxt(..., delimiter=",")` or gnuplot).
- **Column definitions**: Detailed column order (from left to right) is given in the README of each figure folder.
- **Units**: Lengths are in units of the magnetic length `lB`, or of the effective magnetic length `lstar` for the two-anyon model (Figs. 3, 4, 16, 19, 20, 21, and 27). Densities are reported in units of filling factor, i.e., as `2 pi rho lB^2` or `2 pi rho lstar^2`.
- **Errors**: For Monte Carlo results, both the mean and its standard error are reported in separate columns; for quadrature or analytical calculations, exact values are reported.

## License
CC BY 4.0, see `LICENSE`. Please cite the paper when using these data.
