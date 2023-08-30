gdal_merge.py
-------------

Některé programy nejsou C++ binárky, ale skripty v jazyce Python. Příkladem je ``gdal_merge.py``, který umožní spojit více rastrů do jednoho souboru. Je to jedna z možných cest (jiná je pomocí virtuálního rastru).

.. code-block:: text

        gdal_merge.py -o _data/big_dem.tiff _data/Copernicus_DSM_COG_30_N49_00_E015_00_DEM.tif _data/Copernicus_DSM_COG_30_N50_00_E015_00_DEM.tif
