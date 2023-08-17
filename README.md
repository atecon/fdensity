# Introduction

Calculate the bandwidth for kernel density estimation (KDE) using various methods for uni-variate data only (at the moment).

Please report bugs or comments on the gretl mailing list, write to
atecon@posteo.de or report an issue on github
(https://github.com/atecon/KdeBandwidt).


# Public function

```
function scalar (matrix m, string method, const int df[0::1], const int skip_na[0:1:1], const int verbose[0:1:0])
```

Calculate the bandwidth for kernel density estimation (KDE) using various methods for uni-variate data only (at the moment).


## Parameters

- `m`:     `matrix`, Input data as a column vector
- `method`:  `string`, Method for bandwidth selection. Supported values: "scott" or "silverman".
- `df`: bool, Indicator for degrees of freedom correction. 0 not to correct, 1 to correct.
- `skip_na`: `bool`, Indicator for skipping missing values. 0 to include missing values, 1 to remove them.
- `verbose`: `bool`, Indicator for printing bandwidth selection results. 0 to disable, 1 to enable.

## Returns

scalar: The calculated bandwidth for KDE.


# Changelog

* **v0.1 (August 2023)**
    * Initial version
