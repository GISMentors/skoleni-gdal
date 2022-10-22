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

        gdalwarp data/T33UWQ_20220907T095549_TCI.jp2 _data/T33UWQ_20220907T095549_TCI.tiff

Příklad výstupu:

.. code-block::

        Creating output file that is 10980P x 10980L.
        Processing _data/T33UWQ_20220907T095549_TCI.jp2 [1/1] : 0...10...20...30...40...50...60...70...80...90...100 - done.

Výstupní soubor není jinak komprimovaný a je uložený ve formátu GeoTIFF

.. code-block::

        gdalinfo data/T33UWQ_20220907T095549_TCI.tiff

        Driver: GTiff/GeoTIFF
        Files: _data/T33UWQ_20220907T095549_TCI.tiff
        [...]

* ``129M T33UWQ_20220907T095549_TCI.jp2``
* ``345M T33UWQ_20220907T095549_TCI.tiff``
