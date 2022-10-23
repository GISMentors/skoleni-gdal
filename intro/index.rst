=====================
Úvod do knihovny GDAL
=====================

GDAL znamená "Geospatial Data Abstraction Library". Vyslovujeme "gee-doll" nebo "gee-dall" nebo "goo-doll". 

Součástí knihovny GDAL je i knihovan OGR - OpenGIS simple features Reference implementation. 

Pamatujte si: 

        * `gdal*` - rastry
        * `ogr*` - vektory

Příkazy GDAL/OGR
----------------
Ve vašem systému je nainstalovaná celá řada příkazů odvozených z knihovny GDAL. Ty pro rastrová data začínají předponou ``gdal``, ty pro vektory začínají předponou ``ogr``

Parametry příkazů
^^^^^^^^^^^^^^^^^

Obecná struktura použití příkazů vypadá následovně:

.. code-block::

        příkaz [-parametr [hodnota]] [--obecny_parametr] soubor [výstupní_soubor]

Příklad

.. code-block::
        
        gdalinfo soubor.tif

        gdalwarp -te 15 50 16 51 -t_srs epsg:3857 soubor.tiff vystup.tiff

        gdal_translate --formats
        
Obecné parametry
^^^^^^^^^^^^^^^^
Všechny příkazy GDAL mají společnou sadu parametrů, které můžete použít pro získání informace o systému:


``--help``
        Rychlá nápověda
``--version``
        Verze knihovny GDAL
``--build``
        Informace o lokální insalaci GDAL
``--formats``
        Seznam všech formátů podporovaných na daném systému
``--format <format>``
        Detailní informace o formátu
``--optfile <filename>``
        Soubor, ze kterého se mají načíst další parametry
``--config <key> <value>``
        Nastavení, které ovlivní běh programů knihovny GDAL
``--debug <value>``
        Vypíše více informativní výstup při běhu programů
``--help-general``
        Dá podrobnější návod k programům

Příklad použití:

.. code-block::
        
        gdalinfo --help
        gdalinfo --formats
        gdalinfo --format gtiff

Na čem stojí GDAL
^^^^^^^^^^^^^^^^^
GDAL nefunguje jako knihovna sám o sobě, je napojen na celou řadu jiných knihoven zásadních pro GIS.

* Proj4 - pro práci s projekcemi
* Geos - pro práci s vektorovými daty a řešení topologických úloh
* SQLite3
* ...
