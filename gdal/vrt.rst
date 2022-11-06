Virtual Raster format - VRT
---------------------------

Mezi mnoha formáty, které podporuje knihovna GDAL má `Virtual rastr driver <https://gdal.org/drivers/raster/vrt.html>`_ zvláštní místo. Jedná se soubor XML, kterým můžeme zpracovávat vstupní rastrové soubory za běhu. Soubor tak nezabírá místo. VRT soubory lze řetězit, přidávat do nich kód v jazyce Python a tak podobně.

Transformace souřadnicového systému
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Jako první příklad prostě pouze ztransformujeme souřadnicový systém vstupního souboru:

.. code-block:: text

   gdalwarp -t_srs epsg:5514 -of VRT _data/Copernicus_DSM_COG_30_N49_00_E015_00_DEM.tif _data/Copernicus_DSM_COG_30_N49_00_E015_00_DEM-krovak.vrt

   gdalinfo _data/Copernicus_DSM_COG_30_N49_00_E015_00_DEM-krovak.vrt

Podíváme-li se na VRT soubor blíže, uvidíme, že se jedná o celkem malý soubor XML

.. code-block:: XML

        <VRTDataset rasterXSize="1093" rasterYSize="1524" subClass="VRTWarpedDataset">
          <SRS dataAxisToSRSAxisMapping="1,2">PROJCS["S-JTSK / Krovak East North",GEOGCS["S-JTSK",DATUM["System_of_the_Unified_Trigonometrical_Cadastral_Network",SPHEROID["Bessel 1841",6377397.155,299.1528128,AUTHORITY["EPSG","7004"]],AUTHORITY["EPSG","6156"]],PRIMEM["Greenwich",0,AUTHORITY["EPSG","8901"]],UNIT["degree",0.0174532925199433,AUTHORITY["EPSG","9122"]],AUTHORITY["EPSG","4156"]],PROJECTION["Krovak"],PARAMETER["latitude_of_center",49.5],PARAMETER["longitude_of_center",24.8333333333333],PARAMETER["azimuth",30.2881397527778],PARAMETER["pseudo_standard_parallel_1",78.5],PARAMETER["scale_factor",0.9999],PARAMETER["false_easting",0],PARAMETER["false_northing",0],UNIT["metre",1,AUTHORITY["EPSG","9001"]],AXIS["Easting",EAST],AXIS["Northing",NORTH],AUTHORITY["EPSG","5514"]]</SRS>
          <GeoTransform> -7.1734568408439704e+05,  7.8201966936414763e+01,  0.0000000000000000e+00, -1.0580974742596082e+06,  0.0000000000000000e+00, -7.8201966936414763e+01</GeoTransform>
          <Metadata>
            <MDI key="AREA_OR_POINT">Point</MDI>
          </Metadata>
          <VRTRasterBand dataType="Float32" band="1" subClass="VRTWarpedRasterBand">
            <ColorInterp>Gray</ColorInterp>
          </VRTRasterBand>
          <BlockXSize>512</BlockXSize>
          <BlockYSize>128</BlockYSize>
          <GDALWarpOptions>
            <WarpMemoryLimit>6.71089e+07</WarpMemoryLimit>
            <ResampleAlg>NearestNeighbour</ResampleAlg>
            <WorkingDataType>Float32</WorkingDataType>
            <Option name="INIT_DEST">0</Option>
            <Option name="ERROR_OUT_IF_EMPTY_SOURCE_WINDOW">FALSE</Option>
            <SourceDataset relativeToVRT="1">Copernicus_DSM_COG_30_N49_00_E015_00_DEM.tif</SourceDataset>
            <Transformer>
              <ApproxTransformer>
                <MaxError>0.125</MaxError>
                <BaseTransformer>
                  <GenImgProjTransformer>
                    <SrcGeoTransform>14.9995833333333337,0.000833333333333333387,0,50.0004166666666663,0,-0.000833333333333333387</SrcGeoTransform>
                    <SrcInvGeoTransform>-17999.5,1200,0,60000.4999999999927,0,-1200</SrcInvGeoTransform>
                    <DstGeoTransform>-717345.684084397042,78.2019669364147632,0,-1058097.47425960819,0,-78.2019669364147632</DstGeoTransform>
                    <DstInvGeoTransform>9172.98774169789976,0.012787402148248906,0,-13530.3179154040554,0,-0.012787402148248906</DstInvGeoTransform>
                    <ReprojectTransformer>
                      <ReprojectionTransformer>
                        <SourceSRS>GEOGCS["WGS 84",DATUM["WGS_1984",SPHEROID["WGS 84",6378137,298.257223563,AUTHORITY["EPSG","7030"]],AUTHORITY["EPSG","6326"]],PRIMEM["Greenwich",0],UNIT["degree",0.0174532925199433,AUTHORITY["EPSG","9122"]],AXIS["Latitude",NORTH],AXIS["Longitude",EAST],AUTHORITY["EPSG","4326"]]</SourceSRS>
                        <TargetSRS>PROJCS["S-JTSK / Krovak East North",GEOGCS["S-JTSK",DATUM["System_of_the_Unified_Trigonometrical_Cadastral_Network",SPHEROID["Bessel 1841",6377397.155,299.1528128,AUTHORITY["EPSG","7004"]],AUTHORITY["EPSG","6156"]],PRIMEM["Greenwich",0,AUTHORITY["EPSG","8901"]],UNIT["degree",0.0174532925199433,AUTHORITY["EPSG","9122"]],AUTHORITY["EPSG","4156"]],PROJECTION["Krovak"],PARAMETER["latitude_of_center",49.5],PARAMETER["longitude_of_center",24.8333333333333],PARAMETER["azimuth",30.2881397527778],PARAMETER["pseudo_standard_parallel_1",78.5],PARAMETER["scale_factor",0.9999],PARAMETER["false_easting",0],PARAMETER["false_northing",0],UNIT["metre",1,AUTHORITY["EPSG","9001"]],AXIS["Easting",EAST],AXIS["Northing",NORTH],AUTHORITY["EPSG","5514"]]</TargetSRS>
                        <Options>
                          <Option key="CENTER_LONG">15.4996</Option>
                          <Option key="AREA_OF_INTEREST">14.99958333333333,49.00041666666667,15.99958333333333,50.00041666666667</Option>
                        </Options>
                      </ReprojectionTransformer>
                    </ReprojectTransformer>
                  </GenImgProjTransformer>
                </BaseTransformer>
              </ApproxTransformer>
            </Transformer>
            <BandList>
              <BandMapping src="1" dst="1" />
            </BandList>
          </GDALWarpOptions>
        </VRTDataset>


Soubor lze bez problému načíst do QGIS a zobrazit.

Výhodou je malá velikost. Nevýhodou pomalejší zpracování

Spojení více souborů do jednoho - gdalbuildvrt
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Pomocí ``gdalbuildvrt`` můžeme spojit více souborů do jednoho

.. code-block:: text

   gdalbuildvrt _data/dem.vrt _data/Copernicus_DSM_COG_30_N49_00_E015_00_DEM.tif _data/Copernicus_DSM_COG_30_N50_00_E015_00_DEM.tif

  gdalinfo _data/dem.vrt

Vložení kódu Python do VRT
^^^^^^^^^^^^^^^^^^^^^^^^^^

Do VRT souboru lze přímo vložit kód v jazyce Python. Kód lze i udržovat v externím souboru. Příklad je převod výšky v metrech na stopy:

.. code-block:: XML

        <VRTDataset rasterXSize="1200" rasterYSize="1200">
          <SRS dataAxisToSRSAxisMapping="2,1">GEOGCS["WGS 84",DATUM["WGS_1984",SPHEROID["WGS 84",6378137,298.257223563,AUTHORITY["EPSG","7030"]],AUTHORITY["EPSG","6326"]],PRIMEM["Greenwich",0],UNIT["degree",0.0174532925199433,AUTHORITY["EPSG","9122"]],AXIS["Latitude",NORTH],AXIS["Longitude",EAST],AUTHORITY["EPSG","4326"]]</SRS>
          <GeoTransform>  1.4999583333333334e+01,  8.3333333333333339e-04,  0.0000000000000000e+00,  5.0000416666666666e+01,  0.0000000000000000e+00, -8.3333333333333339e-04</GeoTransform>

          <VRTRasterBand dataType="Float32" band="1" subClass="VRTDerivedRasterBand">
          <PixelFunctionType>feets</PixelFunctionType>
          <PixelFunctionLanguage>Python</PixelFunctionLanguage>
          <PixelFunctionCode><![CDATA[

        import numpy as np
        def feets(in_ar, out_ar, xoff, yoff, xsize, ysize, raster_xsize, raster_ysize, buf_radius, gt, **kwargs):
                out_ar[:] = in_ar[0]*3.28084

              ]]>
          </PixelFunctionCode>
          <SimpleSource>
              <SourceFilename relativeToVRT="1">Copernicus_DSM_COG_30_N49_00_E015_00_DEM.tif</SourceFilename>
          </SimpleSource>
          </VRTRasterBand>

        </VRTDataset>

A můžeme se pokusit získat statistické údaje

.. code-block:: text

   gdalinfo _data/Copernicus_DSM_COG_30_N49_00_E015_00_DEM-feets.vrt -stats

   [...]
   Metadata:
    STATISTICS_MAXIMUM=2752.158203125
    STATISTICS_MEAN=1673.4303891539
    STATISTICS_MINIMUM=648.65942382812
    STATISTICS_STDDEV=365.32895543763
    STATISTICS_VALID_PERCENT=100

.. warning:: Narazíme na problém, že kvůli bezpečnosti nelze vykonávat kód v Pythonu jen tak. Je potřeba nastavit proměnnou ``GDAL_VRT_ENABLE_PYTHON`` na hodnotu ``YES``. Na os Linux: ``export GDAL_VRT_ENABLE_PYTHON=YES``

Soubor by měl jít zobrazit i v QGIS.
