
<!-- README.md is generated from README.Rmd. Please edit that file -->
geoDK
=====

The goal of geoDK is to make it easy to use danish GIS data in R.
Version modifier pour FOSCAR Mali

Installation
------------

You can install geoDK from github with:

``` r
# install.packages("devtools")
devtools::install_github("mikkelkrogsholm/geoDK")
```

Polygons
--------

geoDK contains polygon data for a range of danish administrative areas. It has data for:

-   parishes
-   zip codes
-   municipalities
-   regions
-   police districts
-   jurisdictions
-   constituencies

Let me show you a few examples.

#### First load packages

``` r
library(geoDK)
library(ggplot2)
library(ggthemes)
```

#### Plot regions

``` r
dk_regions <- geo_get_spatial("Danish regions")

df_regions <- make_tidy_poly(dk_regions)

ggplot(df_regions) +
  geom_polygon(aes(x = lng, y = lat, group = area, fill = regionkode),
               color = "black", show.legend = FALSE) +
  coord_cartesian() +
  theme_map()
```

#### Plot municipalities

``` r
dk_municipalities <- geo_get_spatial("Danish municipalities")

df_municipalities <- make_tidy_poly(dk_municipalities)

ggplot(df_municipalities) +
  geom_polygon(aes(x = lng, y = lat, group = area, fill = komkode),
               color = "black", show.legend = FALSE) +
  coord_cartesian() +
  theme_map()
```

#### Plot police districts

``` r
dk_police_districts <- geo_get_spatial("Danish police districts")

df_police_districts <- make_tidy_poly(dk_police_districts)

ggplot(df_police_districts) +
  geom_polygon(aes(x = lng, y = lat, group = area, fill = polkr_nr),
               color = "black", show.legend = FALSE) +
  coord_cartesian() +
  theme_map()
```

#### Plot zip codes

``` r
dk_zip_codes <- geo_get_spatial("Danish zip codes")

df_zip_codes <- make_tidy_poly(dk_zip_codes)

ggplot(df_zip_codes) +
  geom_polygon(aes(x = lng, y = lat, group = area, fill = postnr_txt),
               color = "black", show.legend = FALSE) +
  coord_cartesian() +
  theme_map()
```

#### Plot parishes

``` r
dk_parishes <- geo_get_spatial("Danish parishes")

df_parishes <- make_tidy_poly(dk_parishes)

ggplot(df_parishes) +
  geom_polygon(aes(x = lng, y = lat, group = area, fill = sognekode),
               color = "black", show.legend = FALSE) +
  coord_cartesian() +
  theme_map()
```

#### Plot jurisdictions

``` r
dk_jurisdictions <- geo_get_spatial("Danish jurisdictions")

df_jurisdictions <- make_tidy_poly(dk_jurisdictions)

ggplot(df_jurisdictions) +
  geom_polygon(aes(x = lng, y = lat, group = area, fill = retskrnr),
               color = "black", show.legend = FALSE) +
  coord_cartesian() +
  theme_map()
```

#### Plot constituencies

``` r
dk_constituencies <- geo_get_spatial("Danish constituencies")

df_constituencies <- make_tidy_poly(dk_constituencies)

ggplot(df_constituencies) +
  geom_polygon(aes(x = lng, y = lat, group = area, fill = storkrnr), show.legend = FALSE) +
  coord_cartesian() +
  theme_map()
```

Place names
-----------

geoDK contains spatial data for a range of danish place names It has data for:

-   areas
-   lines
-   points

Let me show you a few examples.

#### Plot area

``` r
placename_area <- geo_get_spatial("Danish placenames - areas")

# Pick only islands
placename_area_sub <- subset(placename_area, placename_area$feat_type == "ø")

placename_area_sub_df <- make_tidy_poly(placename_area_sub)

ggplot(placename_area_sub_df) +
  geom_polygon(aes(x = lng, y = lat, group = area), show.legend = FALSE,
               fill = "black") +
  coord_cartesian() +
  theme_map()
```

#### Plot lines

``` r
placename_lines <- geo_get_spatial("Danish placenames - lines")

# Pick only water streams
placename_lines_sub <- subset(placename_lines, placename_lines$feat_type == "vandløb")

plot(placename_lines_sub)
```

#### Plot points

``` r
placename_points <- geo_get_spatial("Danish placenames - points")

# Pick only passage graves
placename_points_sub <- subset(placename_points, placename_points$feat_type == "jættestue")

plot(placename_lines_sub)
```
