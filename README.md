
<!-- README.md is generated from README.Rmd. Please edit that file -->
<style type="text/css">
span > img {
 float:left;
}
</style>

# gp <a href="https://kaiaragaki.github.io/gp/"><img src="man/figures/logo.png" align="right" height="138" /></a>

<!-- badges: start -->
<!-- badges: end -->

**gp** introduces a **g**rammar of **p**lates.

Microwell plates are usually arranged in visually meaningful ways but
are not tidy data, and their manipulation to and from a tidy form is
cumbersome. gp is aimed at both developers that create packages that
ingest and produce plate data as well as for interactive operating on
microwell data.

## Installation

You can install the development version from
[GitHub](https://github.com/) with:

``` r
# install.packages("devtools")
devtools::install_github("KaiAragaki/gp")
```

## Creating plates with gp

Creating a plate plot is simple:

``` r
library(gp)
gp(rows = 16, cols = 24) |>
  gp_plot(as.factor(.row))
```

<img src="man/figures/README-example-1.png" width="100%" /> We can add
rectangular ‘sections’ to our plates:

``` r
gp(rows = 16, cols = 24) |> 
  gp_sec("my_section", nrow = 12, ncol = 6) |> 
  gp_plot(my_section)
```

<img src="man/figures/README-unnamed-chunk-2-1.png" width="100%" />

These sections can have sections of their own, just by layering one
`gp_sec` on the other.

``` r
gp(rows = 16, cols = 24) |> 
  gp_sec("my_section", nrow = 12, ncol = 6) |> 
  gp_sec("secsec", nrow = 3, ncol = 3) |> 
  gp_plot(secsec)
```

<img src="man/figures/README-unnamed-chunk-3-1.png" width="100%" />

`gp` also has a theme - `gp_mini_theme` - that lets you create
sparkline-esque plates.

``` r
mini_plot_cols <- gp(8, 12) |> 
  gp_sec(name = "primers", ncol = 3) |> 
  gp_plot(primers) + 
  gp_mini_theme()
ggplot2::ggsave(filename = "./man/figures/mini-plot_cols.png", 
                plot = mini_plot_cols,
                height = 0.5, 
                width = 0.75, 
                units = "in", 
                scale = 3.5)

mini_plot_rows <- gp(8, 12) |> 
  gp_sec(name = "primers", nrow = 3) |> 
  gp_plot(primers) + 
  gp_mini_theme()
ggplot2::ggsave(filename = "./man/figures/mini-plot_rows.png", 
                plot = mini_plot_rows,
                height = 0.5, 
                width = 0.75, 
                units = "in", 
                scale = 3.5)
```

For instance:

> You should align your primers in columns
> <img src="man/figures/mini-plot_cols.png" width="75" /> instead of in
> rows <img src="man/figures/mini-plot_rows.png" width="75" />
