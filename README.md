# Origin-destination data to route networks workflows

The aim of this document is to demonstrate how to convert
Origin-Destination data to route networks. The data for this is from the
[wicid](https://wicid.ukdataservice.ac.uk/flowdata/cider/wicid/downloads.php)
website.

You can download datasets at multiple geographic levels from that
website. We will start with the open MSOA to MSOA dataset.

The study location can be defined as follows:

``` r
study_location_name = "Alder Hay Hospital"
study_location_coodinates = stplanr::geo_code(study_location_name)
study_location_coodinates
```

    [1] -1.921027 53.262318

``` r
study_location_df = data.frame(name = study_location_name, lon = study_location_coodinates[1], lat = study_location_coodinates[2])
study_location_sf = sf::st_as_sf(study_location_df, coords = c("lon", "lat"), crs = 4326)
buffer_distance = 5000
study_location_buffer = sf::st_buffer(study_location_sf, buffer_distance)
```

For the MSOA data we will get data from the `pct` R package as follows:

``` r
msoa_data = pct::get_pct(layer = "z", geography = "msoa", national = TRUE)
```
