This function computes and draws the conditional densities of x for
each value of the discrete variable "d" (aka "factor"). Hence the
package name (factorized density). This can be seen as a companion
feature to "boxplot x d --factorized".

_Warning_: the maximum number of different values for the factor is
set to 12 (the plot would be unreadable otherwise IMO). Moreover, in
order to compute the conditional density, at least 30 valid
observations must be available for each category. Categories that
don't meet that requirement will be ignored.

The function signature is

```
function bundle fdensity(const series x, const series d, 
                         bundle opts_in[null])
```


Internally, this function uses the "kdensity" function, and its
optinal parameters (bandwidth and kernel choice) can be passed via
appropiate keys in the option bundle. More generally, the option
bundle accepts the following keys:

- *scale*: as in kdensity: bandwidth adjustment factor (default 1)
- *control*: as in kdensity: kernel choice, 0 = normal (default), 1 = Epanechnikov
- *dest*: string, destination (default = "display")
- *title*: string, plot title

The returned bundle has the same keys as the option bundle, plus

- *err*: an error code
- *kept*: a vector holding the values of the factor actually used for
  computing the densities
- *f*: a matrix with the estimated densities
