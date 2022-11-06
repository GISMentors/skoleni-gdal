====================
Vektorová data - OGR
====================

Pro práci s vektorovými geodaty se "tradičně" používá knihovna OGR (OpenGIS
Simple Features Reference Implementation) ta je součástí knihovny GDAL. Knihovna
OGR je nízkoúrovňová, přistupuje k datům pokud možno efektivním způsobem. V
současnosti knihovna GDAL podporuje více než 100 vektorových GIS formátů.

    **Driver**
        ovladač pro čtení a zápis dat
    **Datasource**
        zdroj dat, ze kterého a do kterého se čte a zapisuje (soubor, databáze)
    **Layer**
        tzv. "vrstva" - konkrétní sada vektorových prvků - tabulka v databázi
        (těch je v jednom datovém zdroji více).
    **Feature**
        vektorový objekt, který nese atributy a geometrii

Vektorový datový model
----------------------

.. figure:: ../images/ogr-schema.png
   :class: middle

Datasource
^^^^^^^^^^
Datový zdroj - databáze, soubor.

Layer
^^^^^
V případě souborových formátů je přítomna většinou jedna "vrstva". Je to
zbytečná úroveň, ale OGR tím vytváří univerzálně použitelný datový model.

Podporované formáty
-------------------
OGR podporuje více než `100 vektorových formátů <https://gdal.org/drivers/vector/index.html>`_. Ne všechny jsou zakompilované do verze knihovny na vašem počítači (běžně je nainstalována podpora pro cca 90 formátů).

Spolu s knihovnou se nainstaluje do systému celá řada užitečných programů, některé z nich proberem podrobněji. Jejich úplný seznam najdete na `https://gdal.org/programs/index.html <https://gdal.org/programs/index.html>`_


.. toctree::
   :maxdepth: 2

   ogrinfo
   ogr2ogr
   ogrtindex
