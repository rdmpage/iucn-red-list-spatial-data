# iucn-red-list-spatial-data
Converting IUCN Red List to GeoJSON

## Download IUCN data
Once you have created an account at http://www.iucnredlist.org/ you can [download data as shapefiles](http://www.iucnredlist.org/technical-documents/spatial-data).

## Converting to GeoJSON

For background see [Managing GeoJSON data using GDAL](https://savaslabs.com/2015/05/25/manage-geojson.html).

IUCN shapefiles can be big, and the resulting GeoJSON can be huge (for example, if a species distribution is based on geographic provinces, and the polygons follow those the geographical boundaries with a high degree of precision).

### Extract GeoJSON for one species

The GDAL utility **ogr2ogr** can be used to extract and simplify GeoJSON. For example, given the data for shrimps (FW_SHRIMP) we can extract data for *Euryrhynchus amazoniensis* like this:

```
ogr2ogr -f GeoJson Euryrhynchus_amazoniensis.geojson FW_SHRIMP.shp -sql "SELECT * FROM FW_SHRIMP WHERE binomial='Euryrhynchus amazoniensis'" -simplify 0.1
```

Note the use of **-simplify 0.1** to simplify the polygon (without this the file is huge), and the SQL to extract just the data for one species (the species in the dataset are listed din the *.dbf file).




