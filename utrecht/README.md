Open data retrieved from: https://www.jijmaaktutrecht.nl

I've used ogr2ogr to transform the Esri ShapeFiles (in RD) to GeoJSON (in EPSG:4326):

```
ogr2ogr -f "GeoJSON" -t_srs EPSG:4326 -s_srs "+proj=sterea +lat_0=52.15616055555555 +lon_0=5.38763888888889 +k=0.9999079 +x_0=155000 +y_0=463000 +ellps=bessel +units=m +towgs84=565.2369,50.0087,465.658,-0.406857330322398,0.350732676542563,-1.8703473836068,4.0812 +no_defs" wijk.geojson WIJK.shp
```

To convert the CSV files use the following procedure:

 * create an .ovf file:

```
<OGRVRTDataSource>
    <OGRVRTLayer name="mastoverzicht">
        <SrcDataSource>mastoverzicht.csv</SrcDataSource>
        <GeometryType>wkbPoint</GeometryType>
        <LayerSRS>EPSG:28992</LayerSRS>
        <GeometryField encoding="PointFromColumns" x="XPOSITION" y="YPOSITION"/>
        <Field name="BUURT"/>
        <Field name="STRAAT"/>
        <Field name="MASTNUMMER" />
        <Field name="MASTLENGTE" />
    </OGRVRTLayer>
</OGRVRTDataSource>
```

 * run the following ogr2ogr command:

```
ogr2ogr -f "GeoJSON" -t_srs EPSG:4326 -s_srs "+proj=sterea +lat_0=52.15616055555555 +lon_0=5.38763888888889 +k=0.9999079 +x_0=155000 +y_0=463000 +ellps=bessel +units=m +towgs84=565.2369,50.0087,465.658,-0.406857330322398,0.350732676542563,-1.8703473836068,4.0812 +no_defs" -lco COORDINATE_PRECISION=6 mastoverzicht.geojson mastoverzicht.ovf
```
