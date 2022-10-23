Virtuální souborové systémy
---------------------------

`Virtuální souborové systémy GDAL <https://gdal.org/user/virtual_file_systems.html>`_ slouží k tomu, že můžeme pracovat i se zazipovanými soubory nebo soubory uloženými na vzdáleném disku nebo cloudovém uložišti, jako by byly uloženy lokálně.

Virtuální systémy se píší před název souboru a jdou řetězit. 

/vsizip/
        pro práci se sazipovanými soubory
/vsicurl/
        pro práci přes síť
/vsis3_streaming/
        pro práci se soubory uloženými na Amazon S3 úložišti
/vsigs/
        data uložená na Google Cloudu
/vsimem/
        data uložená v paměti

A mnoho dalších

.. code-block:: 

        export AWS_NO_SIGN_REQUEST=YES
        gdalinfo /vsis3_streaming/copernicus-dem-90m/Copernicus_DSM_COG_30_N49_00_E015_00_DEM/Copernicus_DSM_COG_30_N49_00_E015_00_DEM.tif

A výstup

.. code-block::

        Driver: GTiff/GeoTIFF
        Files: /vsis3_streaming/copernicus-dem-90m/Copernicus_DSM_COG_30_N49_00_E015_00_DEM/Copernicus_DSM_COG_30_N49_00_E015_00_DEM.tif
        Size is 1200, 1200
        Coordinate System is:
        GEOGCRS["WGS 84",
            DATUM["World Geodetic System 1984",
                ELLIPSOID["WGS 84",6378137,298.257223563,
                    LENGTHUNIT["metre",1]]],
            PRIMEM["Greenwich",0,
                ANGLEUNIT["degree",0.0174532925199433]],
            CS[ellipsoidal,2],
                AXIS["geodetic latitude (Lat)",north,
                    ORDER[1],
                    ANGLEUNIT["degree",0.0174532925199433]],
                AXIS["geodetic longitude (Lon)",east,
                    ORDER[2],
                    ANGLEUNIT["degree",0.0174532925199433]],
            ID["EPSG",4326]]
        Data axis to CRS axis mapping: 2,1
        Origin = (14.999583333333334,50.000416666666666)
        Pixel Size = (0.000833333333333,-0.000833333333333)
        Metadata:
          AREA_OR_POINT=Point
        Image Structure Metadata:
          COMPRESSION=DEFLATE
          INTERLEAVE=BAND
          LAYOUT=COG
          PREDICTOR=3
        Corner Coordinates:
        Upper Left  (  14.9995833,  50.0004167) ( 14d59'58.50"E, 50d 0' 1.50"N)
        Lower Left  (  14.9995833,  49.0004167) ( 14d59'58.50"E, 49d 0' 1.50"N)
        Upper Right (  15.9995833,  50.0004167) ( 15d59'58.50"E, 50d 0' 1.50"N)
        Lower Right (  15.9995833,  49.0004167) ( 15d59'58.50"E, 49d 0' 1.50"N)
        Center      (  15.4995833,  49.5004167) ( 15d29'58.50"E, 49d30' 1.50"N)
        Band 1 Block=2048x2048 Type=Float32, ColorInterp=Gray
          Overviews: 600x600, 300x300
