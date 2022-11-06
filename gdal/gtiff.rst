Parametry specifické pro formát GeoTIFF a COG
---------------------------------------------
Každý formát má specifické možnosti, jak jeho použití zoptimalizovat. Někdy je to komprese, nastavení hodnoty ``NULLDATA``, paralelní procesing, atd.

Hodnoty specifické pro vstupní i výstupní formáty jsou popsány v dokumentaci ale i pomocí ``gdalinfo``

.. code-block:: text

        gdalinfo --format geotiff

Čtení dokumentace je ale pohodlnější na webové stránce `https://gdal.org/drivers/raster/gtiff.html <https://gdal.org/drivers/raster/gtiff.html>`_

Při vytváření výstupu ve formátu GeoTIFF je dobré některé parametry uvádět vždy nebo alespoň vědět, že existují a v případě problému je použít. Typickým problémem je, že dojde místo na disku, s daty se pracuje pomalu (při procesingu) nebo nejdou zobrazit (jsou moc velké i na QGIS).

Parametry výstupního rastru se většinou nastavují pomocí parametru programu ``gdalwarp`` a dalších přepínačem ``-co`` (creation option):

Nastavení komprese formátu GeoTIFF
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
GeoTIFF ve výchozím nastavení nepoužívá vnitřní kompresi. To vede k velkým souborům a rychlému zaplnění disku. Kompresi nastavím hodnotou ``COMPRESS`` a na výběr náme z

* JPEG
* LZW
* PACKBITS
* DEFLATE

a mnoha dalších.

.. code-block:: text

   gdalwarp -co COMPRESS=DEFLATE _data/T33UWQ_20220907T095549_TCI.jp2 _data/T33UWQ_20220907T095549_TCI-compress.tiff

        129M _data/T33UWQ_20220907T095549_TCI.jp2 # <- toto je vstupní soubor

        89M _data/T33UWQ_20220907T095549_TCI-compress-jpg.tiff
        624M _data/T33UWQ_20220907T095549_TCI-compress.tiff
        345M _data/T33UWQ_20220907T095549_TCI-uncompress.tiff
        751M _data/T33UWQ_20220907T095549_TCI-compress-lzw.tiff

Ne všechny kompresní algoritmy fungují dobře pro všechna data a je potřeba je vyzkoušet.

``gdalinfo`` vám vypíše, jaký algoritmus je pro dataset využit.

Block Window
^^^^^^^^^^^^

Většinou jsou data uložena po řádcích, a to není moc vhodné na čtení a následné zpracování. Může být vhodné organizovat data do bloků (block window):

.. code-block:: text

   gdalinfo _data/Copernicus_DSM_COG_30_N49_00_E015_00_DEM.tif

   [...]
   Band 1 Block=2048x2048 Type=Float32, ColorInterp=Gray

Bloky můžeme nastavit atributy ``BLOCKYSIZE`` a ``BLOCKXSIZE``. Bloky musí být dělitelné 16.

.. code-block:: text

   gdalwarp -co TILED=YES -co BLOCKXSIZE=1024 -co BLOCKYSIZE=1024 _data/T33UWQ_20220907T095549_TCI.jp2 _data/T33UWQ_20220907T095549_TCI-block.tiff

   gdalinfo _data/T33UWQ_20220907T095549_TCI-block.tiff
   [...]


   Band 1 Block=1024x1024 Type=Byte, ColorInterp=Red
   Band 2 Block=1024x1024 Type=Byte, ColorInterp=Green
   Band 3 Block=1024x1024 Type=Byte, ColorInterp=Blue

Velký TIFF
^^^^^^^^^^
Formát TIFF má omezení velikosti souboru. Toto omezení lze obejít přepínačem ``BIGTIFF``

.. code-block:: text

        gdalwarp -co BIGTIFF=YES input.tiff output.tiff
