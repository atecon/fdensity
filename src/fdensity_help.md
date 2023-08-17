This function computes and draws the conditional densities of `x` for each value of the discrete variable `d` (aka "factor"). Hence the package name (factorized density). This can be seen as a companion feature to `boxplot x d --factorized`.

_Warning_: the maximum number of different values for the factor is set to 12 (the plot would be unreadable otherwise IMO). Moreover, in order to compute the conditional density, at least 30 valid observations must be available for each category. Categories that don't meet that requirement will be ignored.

The function signature is

```
function bundle fdensity(const series x, const series d, 
                         bundle opts_in[null])
```

Internally, this function uses the `kdensity()` function, and its
optional parameters (bandwidth and kernel choice) can be passed via
appropiate keys in the option bundle. If the `scale` parameter is set to `-1`, the optimal bandwidth is computed by means of the "KdeBandwidth" package written by A. Tarassow.

## Parameters

- `x`:  `series`, Input series for which to compute conditional densities
- `d`:  `series`, Discrete variable (numeric or string-valued) defining the "factors".

More generally, the option bundle accepts the following keys:

- `control`: as in kdensity: kernel choice, 0 = normal (default), 1 = Epanechnikov
- `scale`: as in kdensity: bandwidth adjustment factor (default 1), Set to `-1` for computing the optimal bandwidth automatically (see the following options)
- `bw_method`: string, Method for computing optimal bandwidth, either "silverman" or "scott" (default: "silverman")
- `bw_df`: bool, Indicator for degrees of freedom correction. 0 not to correct, 1 to correct (default).
- `bw_skip_na`: `bool`, Indicator for skipping missing values. 0 to include missing values, 1 to remove them.
- `bw_verbose`: `bool`, Indicator for printing bandwidth selection results. 0 to disable, 1 to enable.
- `dest`: string, destination (default = "display")
- `title`: string, plot title

The returned bundle has the same keys as the option bundle, plus

- `err`: an error code
- `kept`: a vector holding the values of the factor actually used for
  computing the densities
- `f`: a matrix with the estimated densities


# Changelog

* **v0.6 (August 2023)**
    * Add support for automatic optimal bandwidth selection
    * Internal refactoring

* **v0.5 (April 2022)**
    * Initial version
