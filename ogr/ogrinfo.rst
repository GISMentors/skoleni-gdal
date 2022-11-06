ogrinfo
--------

`ogrinfo <https://gdal.org/programs/ogrinfo.html>`_ - vypíše informace o vektorovém datovém zdroji


.. code-block::

        ogrinfo [--help-general] [-ro] [-q] [-where restricted_where|@filename]
               [-spat xmin ymin xmax ymax] [-geomfield field] [-fid fid]
               [-sql statement|@filename] [-dialect sql_dialect] [-al] [-rl] [-so] [-fields={YES/NO}]
               [-geom={YES/NO/SUMMARY}] [[-oo NAME=VALUE] ...]
               [-nomd] [-listmdd] [-mdd domain|`all`]*
               [-nocount] [-noextent] [-nogeomtype] [-wkt_format WKT1|WKT2|...]
               [-fielddomain name]
               datasource_name [layer [layer ...]]

Příklad použití:

.. code-block::

        ogrinfo _data/659673/KATASTRALNI_UZEMI_L.shp

Příklad výstupu:

.. code-block::

        INFO: Open of `_data/659673/KATASTRALNI_UZEMI_L.shp'
              using driver `ESRI Shapefile' successful.
        1: KATASTRALNI_UZEMI_L (Line String)


Ve výpisu vidíme pouze seznam dostupných vrstev. Formát ESRI Shapfile je
souborový a je v něm pouze jedna vrstva - ta má stejný název jako jméno souboru.

Pro více informací musíme zadat ještě jméno vrstvy.

.. code-block::

        ogrinfo _data/659673/KATASTRALNI_UZEMI_L.shp KATASTRALNI_UZEMI_L

Výstup:

.. code-block::

        INFO: Open of `_data/659673/KATASTRALNI_UZEMI_L.shp'
              using driver `ESRI Shapefile' successful.

        Layer name: KATASTRALNI_UZEMI_L
        Metadata:
          DBF_DATE_LAST_UPDATE=2022-10-15
        Geometry: Line String
        Feature Count: 33
        Extent: (-672804.140000, -1132714.460000) - (-666935.600000, -1126153.790000)
        Layer SRS WKT:
        BOUNDCRS[
            SOURCECRS[
                PROJCRS["S-JTSK / Krovak East North",
                    BASEGEOGCRS["S-JTSK",
                        DATUM["System of the Unified Trigonometrical Cadastral Network",
                            ELLIPSOID["Bessel 1841",6377397.155,299.1528128,
                                LENGTHUNIT["metre",1]]],
                        PRIMEM["Greenwich",0,
                            ANGLEUNIT["degree",0.0174532925199433]],
                        ID["EPSG",4156]],
                    CONVERSION["unnamed",
                        METHOD["Krovak (North Orientated)",
                            ID["EPSG",1041]],
                        PARAMETER["Latitude of projection centre",49.5,
                            ANGLEUNIT["degree",0.0174532925199433],
                            ID["EPSG",8811]],
                        PARAMETER["Longitude of origin",24.8333333333333,
                            ANGLEUNIT["degree",0.0174532925199433],
                            ID["EPSG",8833]],
                        PARAMETER["Co-latitude of cone axis",30.2881397222222,
                            ANGLEUNIT["degree",0.0174532925199433],
                            ID["EPSG",1036]],
                        PARAMETER["Latitude of pseudo standard parallel",78.5,
                            ANGLEUNIT["degree",0.0174532925199433],
                            ID["EPSG",8818]],
                        PARAMETER["Scale factor on pseudo standard parallel",0.9999,
                            SCALEUNIT["unity",1],
                            ID["EPSG",8819]],
                        PARAMETER["False easting",0,
                            LENGTHUNIT["metre",1],
                            ID["EPSG",8806]],
                        PARAMETER["False northing",0,
                            LENGTHUNIT["metre",1],
                            ID["EPSG",8807]]],
                    CS[Cartesian,2],
                        AXIS["x",east,
                            ORDER[1],
                            LENGTHUNIT["metre",1]],
                        AXIS["y",north,
                            ORDER[2],
                            LENGTHUNIT["metre",1]],
                    ID["EPSG",5514]]],
            TARGETCRS[
                GEOGCRS["WGS 84",
                    DATUM["World Geodetic System 1984",
                        ELLIPSOID["WGS 84",6378137,298.257223563,
                            LENGTHUNIT["metre",1]]],
                    PRIMEM["Greenwich",0,
                        ANGLEUNIT["degree",0.0174532925199433]],
                    CS[ellipsoidal,2],
                        AXIS["latitude",north,
                            ORDER[1],
                            ANGLEUNIT["degree",0.0174532925199433]],
                        AXIS["longitude",east,
                            ORDER[2],
                            ANGLEUNIT["degree",0.0174532925199433]],
                    ID["EPSG",4326]]],
            ABRIDGEDTRANSFORMATION["Transformation from S-JTSK to WGS84",
                METHOD["Position Vector transformation (geog2D domain)",
                    ID["EPSG",9606]],
                PARAMETER["X-axis translation",589,
                    ID["EPSG",8605]],
                PARAMETER["Y-axis translation",76,
                    ID["EPSG",8606]],
                PARAMETER["Z-axis translation",480,
                    ID["EPSG",8607]],
                PARAMETER["X-axis rotation",0,
                    ID["EPSG",8608]],
                PARAMETER["Y-axis rotation",0,
                    ID["EPSG",8609]],
                PARAMETER["Z-axis rotation",0,
                    ID["EPSG",8610]],
                PARAMETER["Scale difference",1,
                    ID["EPSG",8611]]]]
        Data axis to CRS axis mapping: 1,2
        ID: String (40.0)
        ID_2: String (40.0)
        TYPPPD_KOD: String (40.0)
        KATUZE_K_1: Integer (6.0)
        KATUZE_K_2: Integer (6.0)
        PRARES_K_1: Integer (3.0)
        PRARES_K_2: Integer (3.0)
        KURAD_K_1: Integer (3.0)
        KURAD_K_2: Integer (3.0)
        OGRFeature(KATASTRALNI_UZEMI_L):0
          ID (String) = 1
          ID_2 (String) = 1884471
          TYPPPD_KOD (String) = 1071
          KATUZE_K_1 (Integer) = 643084
          KATUZE_K_2 (Integer) = 659673
          PRARES_K_1 (Integer) = (null)
          PRARES_K_2 (Integer) = (null)
          KURAD_K_1 (Integer) = (null)
          KURAD_K_2 (Integer) = (null)
          LINESTRING (-671086.54 -1128987.12,-671085.75 -1128987.66,-671082.28 -1128989,-671084.25 -1128993.85,-671085.69 -1128997.39,-671088.25 -1129003.69,-671091.43 -1129011.51,-671092.56 -1129014.3,-671095.11 -1129020.57,-671102.5 -1129038.77,-671103.52 -1129041.28,-671111.44 -1129060.77,-671113.16 -1129064.42,-671112.77 -1129064.8,-671092.98 -1129084.03,-671085.74 -1129091.06,-671084.47 -1129092.29,-671069.66 -1129106.68,-671060.46 -1129115.62,-671055.99 -1129119.97,-671047.11 -1129125.88,-671040.17 -1129130.5,-671036.73 -1129132.79,-671031.49 -1129136.28,-671020.17 -1129143.82,-671014.97 -1129147.28,-671011.48 -1129149.6,-671009.32 -1129151.04,-671004.63 -1129153.64,-670987.23 -1129163.28,-670964.99 -1129175.61,-670926.3 -1129200.28,-670894.7 -1129217.38,-670885.1 -1129222.58,-670875.02 -1129228.03,-670850.79 -1129237.1,-670849.85 -1129237.3,-670839.33 -1129239.61,-670837.53 -1129240,-670826.1 -1129242.51,-670817.39 -1129242.89,-670810.1 -1129243.21,-670802.68 -1129243.53,-670800.96 -1129243.61,-670799.48 -1129243.67,-670777.13 -1129242.29,-670765.82 -1129240.6,-670758.96 -1129239.58,-670750.88 -1129238.38,-670713.87 -1129233.32,-670657.1 -1129212.04,-670656.53 -1129211.83,-670654.28 -1129211.38,-670637.4 -1129207.98,-670634.2 -1129213.22,-670626.5 -1129226.15,-670626.39 -1129226.33,-670618.31 -1129239.9,-670613.51 -1129248.64,-670599.11 -1129271.79,-670582.5 -1129299.43,-670582.31 -1129299.74,-670580.93 -1129302.03,-670580.24 -1129303.19,-670566.96 -1129325.26,-670585.68 -1129353.46,-670585.9 -1129353.8,-670587.12 -1129355.63,-670596.76 -1129363.66,-670600.06 -1129366.41,-670603.58 -1129369.34,-670604.85 -1129370.39,-670615.17 -1129378.98,-670621.28 -1129384.07,-670623.84 -1129386.58,-670628.2 -1129390.94,-670642.65 -1129419.33,-670644.24 -1129422.53,-670647.92 -1129429.7)

        OGRFeature(KATASTRALNI_UZEMI_L):1
          ID (String) = 2
          ID_2 (String) = 2227545
          TYPPPD_KOD (String) = 1071
          KATUZE_K_1 (Integer) = 659673
          KATUZE_K_2 (Integer) = 659827
          PRARES_K_1 (Integer) = (null)
          PRARES_K_2 (Integer) = (null)
          KURAD_K_1 (Integer) = (null)
          KURAD_K_2 (Integer) = (null)
          LINESTRING (-667553.96 -1130035.46,-667537.28 -1130025.01,-667536.97 -1130024.82,-667536 -1130024.21,-667526.69 -1130016.7,-667519.78 -1130011.12,-667517.9 -1130009.6,-667512.2 -1130002.46,-667508.32 -1129997.6,-667506.47 -1129993.29,-667501.11 -1129980.82,-667496.21 -1129973.1,-667481.2 -1129949.43,-667473.01 -1129936.51,-667477.19 -1129931.01,-667481.61 -1129925.19,-667488.28 -1129916.41,-667490.5 -1129918.57,-667489.95 -1129864.35,-667495.71 -1129804.3,-667493.99 -1129783.63,-667487.45 -1129750.36,-667479.97 -1129715.78,-667479.1 -1129680.42,-667481.71 -1129651.59,-667487.98 -1129636.63,-667494.56 -1129613.03,-667498.98 -1129589.04,-667501.77 -1129574.52,-667505.32 -1129553.21,-667511.16 -1129530.21,-667533.1 -1129472.02,-667541.1 -1129455.87,-667548.06 -1129429.89,-667543.73 -1129420.55,-667559.9 -1129413.7,-667586.7 -1129402.3,-667592.38 -1129395.99,-667602.39 -1129385.14,-667608.3 -1129378.15,-667619.76 -1129369.18,-667640.99 -1129351.03,-667641.79 -1129346.09,-667642.81 -1129339.75,-667643.83 -1129333.4,-667644.62 -1129328.46)


.. task::
   Jaké atributy vrstva obsahuje?

.. task::
   O jaký typ geometrie se jedná?

.. task::
   Kolik prvků je ve vrstvě dostupných?

ogrinfo -so
^^^^^^^^^^^^

Přepínač ``-so`` - summary only - nám vypíše všechna potřebná metadata, ale už
ne všechny prvky a jejich geometrie. To je většinou to, co chceme

.. code-block::
   
        ogrinfo -so _data/659673/KATASTRALNI_UZEMI_L.shp KATASTRALNI_UZEMI_L

ogrinfo -al
^^^^^^^^^^^^

Přepínač ``-al`` all layers - vypíše údaje ke všem vrstvám v datasetu. V případě
souborových datasetů tedy pouze k jedné z nich. Nemusíte tedy vypisovat znova
jméno souboru.

.. code-block::
   
        ogrinfo -so -al _data/659673/KATASTRALNI_UZEMI_L.shp


ogrinfo -geom
^^^^^^^^^^^^^

Výpis z geometrie lze trochu zkrátit - někdy stačí pouze datový typ, počet prvků


.. code-block::
   
        ogrinfo _data/659673/KATASTRALNI_UZEMI_P.shp -geom=SUMMARY KATASTRALNI_UZEMI_P

ogrinfo -fields
^^^^^^^^^^^^^^^

Stejně tak můžeme nechat vypsat pouze geometrii, bez dalších atributů


.. code-block::
   
        ogrinfo _data/659673/KATASTRALNI_UZEMI_P.shp -fields=NO KATASTRALNI_UZEMI_P

ogrinfo -spat
^^^^^^^^^^^^^

Můžeme vyfiltrovat pouze některé prvky prostorovým filtrem

Porovnejte výstup

.. code-block::
   
        ogrinfo -so _data/659673/PARCELY_KN_P.shp PARCELY_KN_P

s

.. code-block::

        ogrinfo -so -spat -671296 -1131933 -669825 -1131926 _data/659673/PARCELY_KN_P.shp PARCELY_KN_P


ogrinfo -fid
^^^^^^^^^^^^

Můžeme se doptat na konkrétní prvek podle jeho ID - myslí se tím ID v datové
sadě, ne atributu (např. čísla parcely).

.. code-block::

        ogrinfo -fid 20191 _data/659673/PARCELY_KN_P.shp PARCELY_KN_P

ogrinfo -where
^^^^^^^^^^^^^^

``-where`` nám umožní napsat filtr podle specifikace SQL a doptávat se na
některé atributy, například vybrat parcely pouze z určitého typu území


1. Zjistíme počet prvků v databázi, ve vrstvě ``parcely``

.. code-block::

        ogrinfo _data/ruian_jihlava.gpkg parcely -so

2. Na stránce 
   https://www.cuzk.cz/Katastr-nemovitosti/Poskytovani-udaju-z-KN/Ciselniky-ISKN/Ciselniky-k-nemovitosti/Druh-pozemku.aspx
   lze dohledat číselník druhů pozemků. Je distribuován ve formátu CSV a
   zazipovaný. S GDAL otevřít tento číselník není žádný problém, využijeme k
   tomu virtuální filesystémy ``/vsicurl`` a ``/vsizip`` a dáme je za sebe. Díky tomu můžeme zobrazit obsah CSV ze vzdálené URL přímo:

.. code-block::

        ogrinfo /vsizip/vsicurl/https://www.cuzk.cz/CUZK/media/CiselnikyISKN/SC_D_POZEMKU/SC_D_POZEMKU.zip SC_D_POZEMKU

4. Vybereme pouze zastavěné pozemky a nádvoří

.. code-block::

        ogrinfo /vsizip/vsicurl/https://www.cuzk.cz/CUZK/media/CiselnikyISKN/SC_D_POZEMKU/SC_D_POZEMKU.zip SC_D_POZEMKU -where "KOD='13'"

5. Můžeme prozkoumat vybrané parcely (kód využití ``13``)

.. code-block::

        ogrinfo _data/ruian_jihlava.gpkg parcely -where "ZpusobyVyuzitiPozemku=13" -so

ogrinfo -sql
^^^^^^^^^^^^

Parametr ``-sql`` jde ještě dál - umožní využít síly standardu SQL při dotazování

.. code-block::

        ogrinfo _data/ruian_jihlava.gpkg -sql "SELECT max(ST_Area(geom)) from parcely"

.. note::

   Zde jsme využili vlastnosti formátu OGC GeoPackage, který nám umožňuje využít
   prostorové funkce v prostorových databází. Na formátu Shapefile bychom takové
   možnosti neměli
