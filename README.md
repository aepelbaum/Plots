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

Le o arquivo de UFs com seus status

``` r
df_uf_status <- read_csv2("data/uf_status.csv", col_names = TRUE,
                          locale = locale(encoding = "ISO-8859-1"), col_types = NULL)
```

Le os shapefiles Buscar shp novo em:
<https://cran.r-project.org/web/packages/geobr/vignettes/intro_to_geobr.html>

``` r
st_brasil <- readOGR("./data/bra_adm1", "BRA_adm1", encoding = "UTF-8", use_iconv = TRUE) 
#> OGR data source with driver: ESRI Shapefile 
#> Source: "D:\Ale\Pessoal\R\Projects\plots\data\bra_adm1", layer: "BRA_adm1"
#> with 27 features
#> It has 12 fields
#> Integer64 fields read as strings:  ID_0 ID_1 CCN_1
```

``` r
sf_brasil <- gSimplify(st_brasil, tol = 0.05, topologyPreserve = TRUE) %>%
  st_as_sf() %>% 
  mutate(UF=st_brasil@data$NAME_1)
```

``` r
sf_brasil_status <- sf_brasil %>% 
  left_join(df_uf_status, by = "UF")
```

Desenha o mapa

``` r
sf_brasil_status %>% 
  ggplot() +
  geom_sf(aes(fill = Status)) +
  coord_sf()
```

<img src="README_files/figure-gfm/unnamed-chunk-7-1.png" style="display: block; margin: auto;" />
