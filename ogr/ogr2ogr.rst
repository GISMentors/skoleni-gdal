ogr2ogr
-------

`ogr2ogr <https://gdal.org/programs/ogr2ogr.html>`_ - nám pomůže s konverzemi
mezi formáty. 

.. code-block:: text

        Usage: ogr2ogr [--help-general] [-skipfailures] [-append] [-update]
                       [-select field_list] [-where restricted_where|@filename]
                       [-progress] [-sql <sql statement>|@filename] [-dialect dialect]
                       [-preserve_fid] [-fid FID] [-limit nb_features]
                       [-spat xmin ymin xmax ymax] [-spat_srs srs_def] [-geomfield field]
                       [-a_srs srs_def] [-t_srs srs_def] [-s_srs srs_def] [-ct string]
                       [-f format_name] [-overwrite] [[-dsco NAME=VALUE] ...]
                       dst_datasource_name src_datasource_name
                       [-lco NAME=VALUE] [-nln name] 
                       [-nlt type|PROMOTE_TO_MULTI|CONVERT_TO_LINEAR|CONVERT_TO_CURVE]
                       [-dim XY|XYZ|XYM|XYZM|layer_dim] [layer [layer ...]]

        Advanced options :
                       [-gt n] [-ds_transaction]
                       [[-oo NAME=VALUE] ...] [[-doo NAME=VALUE] ...]
                       [-clipsrc [xmin ymin xmax ymax]|WKT|datasource|spat_extent]
                       [-clipsrcsql sql_statement] [-clipsrclayer layer]
                       [-clipsrcwhere expression]
                       [-clipdst [xmin ymin xmax ymax]|WKT|datasource]
                       [-clipdstsql sql_statement] [-clipdstlayer layer]
                       [-clipdstwhere expression]
                       [-wrapdateline][-datelineoffset val]
                       [[-simplify tolerance] | [-segmentize max_dist]]
                       [-makevalid]
                       [-addfields] [-unsetFid] [-emptyStrAsNull]
                       [-relaxedFieldNameMatch] [-forceNullable] [-unsetDefault]
                       [-fieldTypeToString All|(type1[,type2]*)] [-unsetFieldWidth]
                       [-mapFieldType srctype|All=dsttype[,srctype2=dsttype2]*]
                       [-fieldmap identity | index1[,index2]*]
                       [-splitlistfields] [-maxsubfields val]
                       [-resolveDomains]
                       [-explodecollections] [-zfield field_name]
                       [-gcp ungeoref_x ungeoref_y georef_x georef_y [elevation]]* [-order n | -tps]
                       [[-s_coord_epoch epoch] | [-t_coord_epoch epoch] | [-a_coord_epoch epoch]]
                       [-nomd] [-mo "META-TAG=VALUE"]* [-noNativeData]

        Note: ogr2ogr --long-usage for full help.

Příklad použití:

.. code-block:: text

        ogr2ogr _data/katastralni_uzemi.gpkg _data/659673/KATASTRALNI_UZEMI_L.shp

.. note::

        Všimněte si: pořadí souborů je obráceně oproti běžně užívanému. Nejprve
        výstupní a nakonec vstupní soubor.

Základní použití
^^^^^^^^^^^^^^^^
Základní použití je převod z jednoho formátu na druhý. Formát může být
specifikovaný koncovkou souboru, předponou (např. ``PG:``) nebo pomocí parametru
``-f`` (output format). Jako první argument se udává výstup a jako poslední
argument vstup.

.. code-block:: text

        ogr2ogr -f GPKG _data/katastralni_uzemi.gpkg _data/659673/KATASTRALNI_UZEMI_L.shp

Seznam podporovaných formátů samozřejmě získáme pomocí ``--formats``

.. code-block:: text

   ogr2ogr --formats

Výstupní (a vstupní) speciality formátů se dočteme v dokumentaci k jednotlivým
formátům, ať už na webových stránkách https://gdal.org/drivers/vector/index.html
nebo pomocí přepínače ``--format``

.. code-block:: text

        ogr2ogr --format "ESRI Shapefile"


Pokud chceme vidět postup zpracování, přidáme přepínač `-progress`

.. code-block:: text

        ogr2ogr -progress _data/katastralni_uzemi.gpkg _data/659673/KATASTRALNI_UZEMI_L.shp


Přidání prvků vs. jejich přepsání
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Pomocí přepínačů ``-apend`` nebo ``-overwrite`` řídíme, zda se v cílovém datasetu
bude aktualizovat celá vrstva nebo se pouze přidají další prvky na konec tabulky.

Celý soubor přepíšeme "natvrdo" díky přepínači ``-overwrite``

.. code-block:: text

        ogr2ogr _data/jihlava_parcely.gpkg _data/ruian_jihlava.gpkg parcely
        ogr2ogr -append _data/jihlava_parcely.gpkg _data/ruian_polna.gpkg parcely
        ogrinfo _data/jihlava_parcely.gpkg

Porovnejte s


.. code-block:: text

        ogr2ogr _data/jihlava_parcely.gpkg _data/ruian_jihlava.gpkg parcely -overwrite
        ogr2ogr -update _data/jihlava_parcely.gpkg _data/ruian_polna.gpkg parcely
        ogrinfo _data/jihlava_parcely.gpkg 57123

Výběr atributů ze zdrojového souboru
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Výběr atributů můžeme ovlivnit parametrem ``-select``

.. code-block:: text

        ogr2ogr -select Id,KmenoveCislo,PododdeleniCisla,VymeraParcely,ZpusobyVyuzitiPozemku,KatastralniUzemiKod _data/jihlava_parcely.gpkg _data/ruian_jihlava.gpkg parcely -overwrite
        ogrinfo _data/jihlava_parcely.gpkg parcely -so

Výběr konkrétních prvků
^^^^^^^^^^^^^^^^^^^^^^^

Můžeme vybrat konkrétní provek na základě jeho ID ``-fid`` (a uložení do
existujícího souboru, do nové vrstvy)

.. code-block:: text

        ogr2ogr -fid 23214 _data/jihlava_parcely.gpkg -nln prior _data/ruian_jihlava.gpkg parcely
        ogrinfo _data/jihlava_parcely.gpkg prior

Můžeme omezit maximální počet prvků ``-limit``

.. code-block:: text

        ogr2ogr -limit 10 _data/jihlava_parcely.gpkg -nln parcely_10 _data/ruian_jihlava.gpkg parcely
        ogrinfo _data/jihlava_parcely.gpkg parcely_10

Můžeme uplatnit SQL podmínku ``-where``

.. code-block:: text

        ogr2ogr -where "DruhPozemkuKod=14" _data/jihlava_parcely.gpkg -nln zahrady _data/ruian_jihlava.gpkg parcely
        ogrinfo _data/jihlava_parcely.gpkg zahrady

Plná kontrola nad výběrem prvků pomocí SQL
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

S parametrem ``-sql`` můžeme využít veškeré možnosti, které nám tento jazyk
nabízí

.. code-block:: text

   ogr2ogr -sql "SELECT * FROM parcely AS pa INNER JOIN katastralniuzemi AS ku ON pa.KatastralniUzemiKod = ku.Kod WHERE ku.nazev = 'Kosov u Jihlavy' AND ST_Area(pa.geom) > 10000" _data/jihlava_parcely.gpkg -nln kosov_1ha _data/ruian_jihlava.gpkg

Čitelněji zapsaný SQL výraz:

.. code-block:: text

        SELECT * FROM 
                parcely AS pa 
        INNER JOIN 
                katastralniuzemi AS ku 
        ON 
                pa.KatastralniUzemiKod = ku.Kod 
        WHERE 
                ku.nazev = 'Kosov u Jihlavy' 
          AND 
                ST_Area(pa.geom) > 10000"

Pomohli jsme si funkcí ``ST_Area``, která vypočítá z geometri ``pa.geom``
plochu.

Plošné výřezy
^^^^^^^^^^^^^

``ogr2ogr`` má značně univerzální možnosti jak plošně limitovat výběr prvků.

Nejjednodušší je možnost klasického boundingboxu (obálky). Můžeme dokonce
specifikovat souřadnicový systém, ve kterém je filtr nastavený.

.. code-block:: text

   ogr2ogr -spat 15.5784 49.3919 15.6013 49.4050 -spat_srs EPSG:4326 _data/jihlava_parcely.gpkg -nln centrum _data/ruian_jihlava.gpkg parcely

Můžeme ale také místo výběru geometrie natvrdo oříznout pomocí ``-clip``

To může být seznam hodnot ``minx miny maxx, maxy`` nebo přímo jiný datový zdroj,
v našem případě natvrdo napsaný WKT (well known text) trojúhelník.

.. code-block:: text

   ogr2ogr -clipsrc "POLYGON ((-670036 -1130583, -668421 -1130579, -669195 -1129067, -670036 -1130583))" _data/jihlava_parcely.gpkg -nln orez _data/ruian_jihlava.gpkg parcely -nlt MULTIPOLYGON

.. note::

   Musíme ještě natvrdo přetypovat typ výstupní geometrie

Generalizace a segmentace
^^^^^^^^^^^^^^^^^^^^^^^^^

Pomocí parametrů ``-simplify`` a ``segmentize`` můžeme měnit charakter liniových
(a plošných) geometrií

.. code-block:: text

   ogr2ogr -simplify 200 _data/jihlava_parcely.gpkg -nln ku_simple _data/ruian_jihlava.gpkg katastralniuzemi -nlt MULTIPOLYGON

Geometrii lze "zvalidnit" pomocí ``-makevalid``, ale na polygony se musí vzít
jiný postup.

Změna typu geometrie
^^^^^^^^^^^^^^^^^^^^

Volbu ``-nlt`` už jsme používali. Na tomto místě jenom zmíníme, že kromě přímo
datového typu lze ovlivnit, bude-li výstup jako ``MULTI``-geometrie, nebo
například zápis pomocí křivek (u formátů, kde toto lze.

Změna souřadnicového systému
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

``-t_srs`` - cílový souřadnicový systém, ``-s_srs`` zdrojový souřadnicový systém
- pokud je potřeba (např. Shapefile bez ``.prj`` souboru).

.. code-block:: text

        ogr2ogr -s_srs EPSG:4326 _data/katastralni_uzemi-wgs84.gpkg _data/659673/KATASTRALNI_UZEMI_L.shp

nebo komplikovaněji

.. code-block:: text

        ogr2ogr -t_srs EPSG:3857 -s_srs "+proj=krovak +lat_0=49.5 +lon_0=24.8333333333333 +alpha=30.2881397527778 +k=0.9999 +x_0=0 +y_0=0 +ellps=bessel +towgs84=572.213,85.334,461.94,-4.9732,-1.529,-5.2484,3.5378 +units=m +no_defs +type=crs" _data/katastralni_uzemi-krovak.gpkg _data/659673/KATASTRALNI_UZEMI_L.shp


Specifické formáty
^^^^^^^^^^^^^^^^^^

Většina formátů má specifické volby pro čtení a zápis, více lze nalézt v
dokumentaci.

OGC GeoPackage
""""""""""""""

* ...

ESRI Shapefile
""""""""""""""

* Max 2GB
* Kódování
* Délka názvů
* ...

.. code-block:: text

        ogr2ogr -oo ENCODING=Windows-1250 -lco ENCODING=UTF-8 -lco 2GB_LIMIT=NO -lco SPATIAL_INDEX=YES _data/katastralni_uzemi-utf.shp _data/659673/KATASTRALNI_UZEMI_L.shp

CSV
"""

* ...
