gdaladdo
--------
Pro rychlejší zobrazování je nutné - často životně nutné, protože jinak QGIS nic nevykreslí, ale za to spadne - vytvořit tzv. přehledy v rostrových datech.

GDAL projde rastrový soubor a vytvoří náhledy s horším rozlišením. Subor sice trochu naroste, ale pro zobrazování v malých měříctích je možné.

Přehledy lze vytvářet přímo při vytváření, např. ``gdalwarp`` má parametr ``-ovr``. Pokud ale dostanete už hotový rastrový soubor nebo prostě přehledy zapomete vytvořit, ``gdaladdo`` vám pomůže. 

Pro většinu případů je zbytečné zabývat se parametry. ``gdaladdo`` vám umožní hrát si s interpolační metodou, počtem úrovní, kompresí a podobně. Nejčastější použití je ale velice přímočaré:

Ověříme velikost vstupního souboru
.. code-block:: text

        ls -lha _data/T33UWQ_20220907T095549_TCI.tiff 
        
        -rw-rw-r-- 1 user user 345M říj 22 14:16 _data/T33UWQ_20220907T095549_TCI.tiff

Přidáme přehledy
.. code-block:: text

        gdaladdo _data/T33UWQ_20220907T095549_TCI.tiff

A opět ověříme velikost
.. code-block:: text

    ls -lha _data/T33UWQ_20220907T095549_TCI.tiff 
    
    -rw-rw-r-- 1 user user 463M říj 23 14:14 _data/T33UWQ_20220907T095549_TCI.tiff

``gdalinfo`` nám prozradí, jak jsou přehledy vytvořeny

.. code-block:: text

        gdalinfo _data/T33UWQ_20220907T095549_TCI.tiff
        [...]
        Band 1 Block=10980x1 Type=Byte, ColorInterp=Red
          Overviews: 5490x5490, 2745x2745, 1373x1373, 687x687, 344x344, 172x172
        Band 2 Block=10980x1 Type=Byte, ColorInterp=Green
          Overviews: 5490x5490, 2745x2745, 1373x1373, 687x687, 344x344, 172x172
        Band 3 Block=10980x1 Type=Byte, ColorInterp=Blue
          Overviews: 5490x5490, 2745x2745, 1373x1373, 687x687, 344x344, 172x172

Po otevření v QGIS se bude soubor chovat pocitově "svižněji".
