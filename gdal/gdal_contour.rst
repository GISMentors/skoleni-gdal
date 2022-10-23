gdal_contour
------------

Tvorba vrstevnic rastrové mapy. Můžeme zvolit vše potřebné, včetně 3D výstupu, intervalu, vypsat požadované úrovně atd. 

Vrstevnice nejsou nijak vyhlazené, pro to je potřeba rastr předem buď zgeneralizovat nebo naopak zgeneralizovat výstup.

V příkladu vytvoříme vrstevnice vstupního DEM s intervalem 10m ve formátu GPKG. Výstupní atribut s výškou se bude jmenovat ``vyska``.

.. code-block::

   gdal_contour -a vyska -i 10 -f GPKG _data/Copernicus_DSM_COG_30_N49_00_E015_00_DEM.tif _data/vrstevnice.gpkg
