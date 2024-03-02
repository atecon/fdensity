# The 'fdensity' package

This function computes and draws the conditional densities of `x` for each value of the discrete variable `d` (aka "factor"). Hence the package name (factorized density). This can be seen as a companion feature to `boxplot x d --factorized`. It also extends the built-in command `kdplot` and makes internally use of gretl's `kdensity()` function. The optimal bandwitdh is computed by what is known as Silverman's rule of thumb (for details see here: https://gretl.sourceforge.net/gretl-help/funcref.html#kdensity).

_Warning_: the maximum number of different values for the factor is set to `MAXVAL = 12` (the plot would be unreadable otherwise IMO). Moreover, in order to compute the conditional density, at least `MINOBS = 30` valid observations must be available for each category. Categories that don't meet that requirement will be ignored.


The function signature is

``` function bundle fdensity(const series x, const series d, bundle opts_in[null]) ```

Internally, this function uses the `kdensity()` function, and its optional parameters (bandwidth and kernel choice) can be passed via appropiate keys in the option bundle.

## Parameters

- `x`:  `series`, Input series for which to compute conditional densities
- `d`:  `series`, Discrete variable (numeric or string-valued) defining the `p` distinct "factors".

More generally, the option bundle accepts the following keys:

- `control`: as in kdensity: kernel choice, 0 = Gaussian (default), 1 = Epanechnikov
- `scale`: as in gretl's built-in function `kdensity()`: bandwidth adjustment factor; By default this value is `1` and the optimal bandwidth is computed by Silverman's method.
- `bw_skip_na`: `bool`, Indicator for skipping missing values. `FALSE` to include missing values, `TRUE` to remove them (default: `TRUE`).
- `bw_verbose`: `bool`, Indicator for printing bandwidth selection results. `FALSE` to disable, `TRUE` to enable (default: `FALSE`).
- `dest`: string, destination (default = `display`)
- `title`: string, plot title (default = "")
- `ylabel`: string, label at the y-axis (default = "")
- `xlabel`: string, label at the x-axis (default = "")
- `fontsize`: scalar, Size of font for title and labels (default: `10`)
- `fontsize_tics`: scalar, Size of font tics on the y- and the x-axis (default: `10`)
- `linewidth`: scalar, Width of line(s) (default: `2.0`)
- `pointsize`: scalar, Size of points for lines (default: `0.75`; only relevant if `auto_pointtype = TRUE`)
- `auto_dashtype`: bool, Switch on dashed lines with automatic type selection (default = `FALSE`)
- `auto_pointtype`: bool, Switch on lines with points with automatic pointtype selection (default = `FALSE`)
- `monochrome`: bool, Lines are coloured black (default = `FALSE`)
- `nokey`: bool, Do not show key (legend) (default = `FALSE`)
- `single_y_axis`: bool, Enforce single y-axis (default = `FALSE`)
- `add_opts`: string, You may pass additional gnuplot commands as a string (default = "")

The returned bundle has the same keys as the option bundle, plus

- `err`: an error code which is `0` in case of no error, otherwise `1`.
- `f`: a matrix with `p+1` columns. The first `p` columns hold the estimated density or densities at each of these points and the `p+1`-th column holds a set of evenly spaced abscissae.
- `kept`: a vector holding the distinct values of the factors (from input series `f`) actually used for computing the densities. (Others may have been skipped due to insufficient number of observations.)
- `scale`: scalar value holding the optimal bandwitdh if the original value of `scale` is `1` in which case the optimal bandwidth gets computed.


## GUI access

The dialog box can be opened via `View -> Graph specified vars -> Factorized density`.


# Changelog

* **v0.6 (March 2024)**
    * Support for various plotting options
    * Add support for automatic optimal bandwidth selection
    * Internal refactoring

* **v0.5 (April 2022)**
    * Initial version
