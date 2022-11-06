gdalwarp
--------

`gdalwarp <https://gdal.org/programs/gdalwarp.html>`_ - transformuje rastrové soubory do různých formátů, pomáhá s tvorbou výřezů, změna rozlišení, atd.

.. code-block::

    Usage: gdalwarp [--help-general] [--formats]
        [-s_srs srs_def] [-t_srs srs_def] [-to "NAME=VALUE"]* [-vshift | -novshift]
        [[-s_coord_epoch epoch] | [-t_coord_epoch epoch]]
        [-order n | -tps | -rpc | -geoloc] [-et err_threshold]
        [-refine_gcps tolerance [minimum_gcps]]
        [-te xmin ymin xmax ymax] [-tr xres yres] [-tap] [-ts width height]
        [-ovr level|AUTO|AUTO-n|NONE] [-wo "NAME=VALUE"] [-ot Byte/Int16/...] [-wt Byte/Int16]
        [-srcnodata "value [value...]"] [-dstnodata "value [value...]"] -dstalpha
        [-r resampling_method] [-wm memory_in_mb] [-multi] [-q]
        [-cutline datasource] [-cl layer] [-cwhere expression]
        [-csql statement] [-cblend dist_in_pixels] [-crop_to_cutline]
        [-if format]* [-of format] [-co "NAME=VALUE"]* [-overwrite]
        [-nomd] [-cvmd meta_conflict_value] [-setci] [-oo NAME=VALUE]*
        [-doo NAME=VALUE]*
        srcfile* dstfile
    
    Available resampling methods:
        near (default), bilinear, cubic, cubicspline, lanczos, average, rms,
        mode,  max, min, med, Q1, Q3, sum.


Příklad použití:

.. code-block::

        gdalwarp _data/T33UWQ_20220907T095549_TCI.jp2 _data/T33UWQ_20220907T095549_TCI.tiff

Příklad výstupu:

.. code-block::

        Creating output file that is 10980P x 10980L.
        Processing _data/T33UWQ_20220907T095549_TCI.jp2 [1/1] : 0...10...20...30...40...50...60...70...80...90...100 - done.

Výstupní soubor není jinak komprimovaný a je uložený ve formátu GeoTIFF

.. code-block::

        gdalinfo _data/T33UWQ_20220907T095549_TCI.tiff

        Driver: GTiff/GeoTIFF
        Files: _data/T33UWQ_20220907T095549_TCI.tiff
        [...]

* ``129M T33UWQ_20220907T095549_TCI.jp2``
* ``345M T33UWQ_20220907T095549_TCI.tiff``

Změna formátu
^^^^^^^^^^^^^

Většinou stačí použít správnou koncovku souboru (``.tiff``, ``jp2``, ...). Formát souboru můžete vynutit parametrem ``-of``

.. code-block::

        gdalwarp -of GTiff _data/T33UWQ_20220907T095549_B02.jp2 _data/T33UWQ_20220907T095549_B02.tiff

Transformace souřadnicového systému
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Pro přiřazení zdrojového souřadnicového systému (pokud není známý), použijte parametr ``-s_srs``. 

Pro cílový systém použijte parametr ``-t_srs``. Můžete využít zápis pomocí ``EPSG:číslo``.

.. code-block::

   gdalwarp -t_srs epsg:3857 _data/T33UWQ_20220907T095549_B02.jp2 _data/T33UWQ_20220907T095549_B02-mercator.tiff

Výřez z rastru pomocí hraničních souřadnic
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Výřez zájmové oblasti lze získat parametrem  ``-te minx miny maxx maxy`` (target extent). Souřadnice jsou v cílovém souřadnicovém systému.

.. code-block::

        gdalwarp -t_srs epsg:5514 -te -674104 -1132755 -664471 -1125733  _data/T33UWQ_20220907T095549_B02.jp2 _data/T33UWQ_20220907T095549_B02-krovak-jihlava.tiff

Změna rozlišní, velikosti, interpolace
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
* Pro změnu rozlišení rastru slouží parametr ``-tr xres yres`` (target resolution).
* Pro změnu velikosti rastru (nepřímo tedy rozlišení) parametr ``-ts xsize ysize`` (target size).

Ve výchozím nastavení se využívá metoda nejbližšího souseda. Vybrat jiný způsob lze za použití parametru ``-r`` (resampling) a na výběr máme z metod 
        * nearest
        * bilinear
        * cubic
        * cubicspline
        * lanczos
        * average
        * mode

Důležitý je také přepínač ``-tap`` (target aligned pixels) - hraniční souřadnice  výstupního souboru jsou přizpůsobeny požadovanému rozlišení (``-tr``). Přizpůsobení znamená, že poměry xmin/resx, ymin/resy, xmax/resx a ymax/resy jsou celá čísla.

**Příklad:**

Digitální model terénu zájmové oblasti:
.. code-block::

        gdalinfo _data/Copernicus_DSM_COG_30_N49_00_E015_00_DEM.tif 
        [...]

Převod na S-JTSK, region Jihlava, v požadovaném rozlišení:
.. code-block::

        gdalwarp -t_srs epsg:5514 -te -674104 -1132755 -664471 -1125733 -tr 80 80 _data/Copernicus_DSM_COG_30_N49_00_E015_00_DEM.tif _data/dem-krovak-jihlava.tiff

        gdalinfo _data/dem-krovak-jihlava.tiff
        [...]
        Pixel Size = (80.000000000000000,-80.000000000000000)

.. task::

   Porovnejte požadovaný extent ``-te`` s výstupem z ``gdalinfo`` - odpovídají hraniční souřadnice?

Využití parametru ``-tap`` pro přesné "zaříznutí" okrajů.

.. code-block::

        gdalwarp -t_srs epsg:5514 -te -674104 -1132755 -664471 -1125733 -tr 80 80 _data/Copernicus_DSM_COG_30_N49_00_E015_00_DEM.tif _data/dem-krovak-jihlava-tap.tiff

Převzorkování na 2x lepší rozlišení

.. code-block::

        gdalwarp -t_srs epsg:5514 -te -674104 -1132755 -664471 -1125733 -tr 40 40 -r cubicspline _data/Copernicus_DSM_COG_30_N49_00_E015_00_DEM.tif _data/dem-krovak-jihlava-40m.tiff

Ořez pomocí vektorové vrstvy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Parametrem ``-cutline`` můžeme definovat vektorovou vrstvu, která bude použita na ořez rastrových buněk.

.. code-block::

        gdalwarp -t_srs epsg:5514 -cutline _data/659673/KATASTRALNI_UZEMI_P.shp _data/Copernicus_DSM_COG_30_N49_00_E015_00_DEM.tif _data/dem-krovak-jihlava-cut.tiff

Další parametry slouží pro přesnější výběr linie ořezu:

``-cutline_proj``
        Zadat projekci linie, pokud není definována
``-cl``
        Pokud je ve vektorovém datovém zdroji více vrstev, lze vybrat tu správnou
``-cwhere``
        SQL ``WHERE`` podmínka pro výběr prvků z vektorového datasetu.
``-cblend``
        Rozmazání okrajů výřezu. Dá se použít na prolnutí s jinými daty
``-crop_to_cutline``
        Ořízne rastrovou mapu na nejmenší obdélník okolo cutline

Nastavení hodnoty NODATA
^^^^^^^^^^^^^^^^^^^^^^^^
Pro vstupní rastr můžeme hodnotu vynutit, pro výstupní nastavit parametry ``-srcnodata`` a ``-dstnodata``

V našem případě nastavíme hodnotu NODATA na hodnotu -9999, aby při prohlížení nebyl rastr "černý".

.. code-block::

        gdalwarp -t_srs epsg:5514 -dstnodata -9999 -cutline _data/659673/KATASTRALNI_UZEMI_P.shp _data/Copernicus_DSM_COG_30_N49_00_E015_00_DEM.tif _data/dem-krovak-jihlava-nodata.tiff
