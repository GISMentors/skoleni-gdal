gdal_translate
--------------
Na rozdíl od  ``gdalwarp``, který slouží hlavně pro práci s projekcí, 
`gdal_translate <https://gdal.org/programs/gdal_translate.html>`_ slouží hlavně pro změnu formátu.

``gdalwarp`` i ``gdal_transalte`` jsou do určité míry zaměnitelné. 

Výřez pomocí okna pixelů
^^^^^^^^^^^^^^^^^^^^^^^^
``gdalwarp`` umí vyříznout cílový extent, což umí ``gdal_translate`` také, ale líp. Můžete nastavit extent, ale i souřadnicový systém extentu

.. code-block:: text

        gdal_translate -projwin 15 50 16 51 -projsrs epsg:5514 

Praktické může být získat výřez podle pixelů

.. code-block:: text

        gdal_translate -srcwin 100 100 500 500 _data/Copernicus_DSM_COG_30_N49_00_E015_00_DEM.tif _data/Copernicus_DSM_COG_30_N49_00_E015_00_DEM-cutwin.tiff


