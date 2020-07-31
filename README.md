Mapa do Brasil
================

Carrega as libraries

``` r
library(tidyverse)
library(readxl)
library(sf)
library(rgdal)
library(rgeos)
```

Lê o arquivo de UFs com seus status

``` r
df_uf_status <- read_csv2("data/uf_status.csv", col_names = TRUE,
                          locale = locale(encoding = "ISO-8859-1"), col_types = NULL)
```

Desenha o mapa

``` r
sf_brasil_status %>% 
  ggplot() +
  geom_sf(aes(fill = Status)) +
  coord_sf()
```

<img src="README_files/figure-gfm/unnamed-chunk-7-1.png" style="display: block; margin: auto;" />
