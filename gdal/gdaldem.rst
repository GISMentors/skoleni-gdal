gdaldem
-------

`gdaldem <https://gdal.org/programs/gdaldem.html>`_ slouží k analýze a vizualizaci digitálních modelů terénu. Můžemem rychle vypočítat expozici, stínovaný reliéf, sklkon, a další výstupy.

.. note::

   Je potřeba pracovat s daty v ne-geografické projekci. Vstupní data nesmí být "ve stupních"::

           gdalwarp -t_srs epsg:5514 _data/Copernicus_DSM_COG_30_N49_00_E015_00_DEM.tif _data/Copernicus_DSM_COG_30_N49_00_E015_00_DEM-krovak.tiff

Výpočet sklonu svahu

.. code-block::

   gdaldem slope _data/Copernicus_DSM_COG_30_N49_00_E015_00_DEM-krovak.tiff _data/Copernicus_DSM_COG_30_N49_00_E015_00_DEM-slope.tiff

Výpočet stínovaného reliéfu

.. code-block::

   gdaldem hillshade _data/Copernicus_DSM_COG_30_N49_00_E015_00_DEM-krovak.tiff _data/Copernicus_DSM_COG_30_N49_00_E015_00_DEM-hillshade.tiff
