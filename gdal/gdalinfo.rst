gdalinfo
--------

`gdalinfo <https://gdal.org/programs/gdalinfo.html>`_ - vypíše informace o rastrovém datasetu


.. code-block::

        gdalinfo [--help-general] [-json] [-mm] [-stats | -approx_stats] [-hist] [-nogcp] [-nomd]
                 [-norat] [-noct] [-nofl] [-checksum] [-proj4]
                 [-listmdd] [-mdd domain|`all`]* [-wkt_format WKT1|WKT2|...]
                 [-sd subdataset] [-oo NAME=VALUE]* [-if format]* datasetname

Příklad použití:

.. code-block::

        gdalinfo data/T33UWQ_20220907T095549_TCI.jp2

Příklad výstupu:

.. code-block::

        Driver: JP2OpenJPEG/JPEG-2000 driver based on OpenJPEG library
        Files: data/T33UWQ_20220907T095549_TCI.jp2
        Size is 10980, 10980
        Coordinate System is:
        PROJCRS["WGS 84 / UTM zone 33N",
            BASEGEOGCRS["WGS 84",
                ENSEMBLE["World Geodetic System 1984 ensemble",
                    MEMBER["World Geodetic System 1984 (Transit)"],
                    MEMBER["World Geodetic System 1984 (G730)"],
                    MEMBER["World Geodetic System 1984 (G873)"],
                    MEMBER["World Geodetic System 1984 (G1150)"],
                    MEMBER["World Geodetic System 1984 (G1674)"],
                    MEMBER["World Geodetic System 1984 (G1762)"],
                    MEMBER["World Geodetic System 1984 (G2139)"],
                    ELLIPSOID["WGS 84",6378137,298.257223563,
                        LENGTHUNIT["metre",1]],
                    ENSEMBLEACCURACY[2.0]],
                PRIMEM["Greenwich",0,
                    ANGLEUNIT["degree",0.0174532925199433]],
                ID["EPSG",4326]],
            CONVERSION["UTM zone 33N",
                METHOD["Transverse Mercator",
                    ID["EPSG",9807]],
                PARAMETER["Latitude of natural origin",0,
                    ANGLEUNIT["degree",0.0174532925199433],
                    ID["EPSG",8801]],
                PARAMETER["Longitude of natural origin",15,
                    ANGLEUNIT["degree",0.0174532925199433],
                    ID["EPSG",8802]],
                PARAMETER["Scale factor at natural origin",0.9996,
                    SCALEUNIT["unity",1],
                    ID["EPSG",8805]],
                PARAMETER["False easting",500000,
                    LENGTHUNIT["metre",1],
                    ID["EPSG",8806]],
                PARAMETER["False northing",0,
                    LENGTHUNIT["metre",1],
                    ID["EPSG",8807]]],
            CS[Cartesian,2],
                AXIS["(E)",east,
                    ORDER[1],
                    LENGTHUNIT["metre",1]],
                AXIS["(N)",north,
                    ORDER[2],
                    LENGTHUNIT["metre",1]],
            USAGE[
                SCOPE["Engineering survey, topographic mapping."],
                AREA["Between 12°E and 18°E, northern hemisphere between equator and 84°N, onshore and offshore. Austria. Bosnia and Herzegovina. Cameroon. Central African Republic. Chad. Congo. Croatia. Czechia. Democratic Republic of the Congo (Zaire). Gabon. Germany. Hungary. Italy. Libya. Malta. Niger. Nigeria. Norway. Poland. San Marino. Slovakia. Slovenia. Svalbard. Sweden. Vatican City State."],
                BBOX[0,12,84,18]],
            ID["EPSG",32633]]
        Data axis to CRS axis mapping: 1,2
        Origin = (499980.000000000000000,5500020.000000000000000)
        Pixel Size = (10.000000000000000,-10.000000000000000)
        Image Structure Metadata:
          INTERLEAVE=PIXEL
        Corner Coordinates:
        Upper Left  (  499980.000, 5500020.000) ( 14d59'59.00"E, 49d39' 9.80"N)
        Lower Left  (  499980.000, 5390220.000) ( 14d59'59.02"E, 48d39'54.11"N)
        Upper Right (  609780.000, 5500020.000) ( 16d31'14.14"E, 49d38'33.85"N)
        Lower Right (  609780.000, 5390220.000) ( 16d29'26.41"E, 48d39'19.39"N)
        Center      (  554880.000, 5445120.000) ( 15d45' 9.65"E, 49d 9'23.20"N)
        Band 1 Block=256x256 Type=Byte, ColorInterp=Red
          Overviews: 5490x5490, 2745x2745, 1373x1373, 687x687
          Overviews: arbitrary
          Image Structure Metadata:
            COMPRESSION=JPEG2000
        Band 2 Block=256x256 Type=Byte, ColorInterp=Green
          Overviews: 5490x5490, 2745x2745, 1373x1373, 687x687
          Overviews: arbitrary
          Image Structure Metadata:
            COMPRESSION=JPEG2000
        Band 3 Block=256x256 Type=Byte, ColorInterp=Blue
          Overviews: 5490x5490, 2745x2745, 1373x1373, 687x687
          Overviews: arbitrary
          Image Structure Metadata:
            COMPRESSION=JPEG2000


Ve výpisu můžeme najít informace:

        * Název datového zdroje, jeho formát
        * Informace o projekci
        * Oblast, kterou data pokrývají
        * Rozlišení pixelu
        * Informace o kanálech a nebo overviews (přehledech)

.. task::
   Kolik kanálů datový zdroj obsahuje?

.. task::
   Jaké je rozlišení rastru?

.. task::
   V jakém souřadnicové systému je datový soubor?

.. task::
   Jaký je formát rastrového souboru, jakou používá kompresi?

.. task::
   Porovnejte výpis se souborem v blízkém infračerveném spektru

   gdalinfo data/T33UWQ_20220907T095549_B08.jp2

gdalinfo -stats
^^^^^^^^^^^^^^^

Parametr ``-stats`` provede výpočet základních statistik rastrového souboru. Pokud to formát umožňuje, uloží je pro příští použití. Pokud to formát neumožňuje, vytvoří speciální metadatový soubor s příponou ``.aux.xml``

.. code-block::

        gdalinfo -stats data/T33UWQ_20220907T095549_TCI.jp2

Výpočet trvá déle, statistika se zpracovává pro všechny kanály.

Příklad výstupu:

.. code-block::

        [...]

        Band 1 Block=256x256 Type=Byte, ColorInterp=Red
          Minimum=0.000, Maximum=255.000, Mean=59.435, StdDev=32.406
          Overviews: 5490x5490, 2745x2745, 1373x1373, 687x687
          Overviews: arbitrary
          Metadata:
            STATISTICS_MAXIMUM=255
            STATISTICS_MEAN=59.434880906168
            STATISTICS_MINIMUM=0
            STATISTICS_STDDEV=32.40620283593
            STATISTICS_VALID_PERCENT=100
          Image Structure Metadata:
            COMPRESSION=JPEG2000
        Band 2 Block=256x256 Type=Byte, ColorInterp=Green
          Minimum=1.000, Maximum=255.000, Mean=69.111, StdDev=22.082
          Overviews: 5490x5490, 2745x2745, 1373x1373, 687x687
          Overviews: arbitrary
          Metadata:
            STATISTICS_MAXIMUM=255
            STATISTICS_MEAN=69.110535623638
            STATISTICS_MINIMUM=1
            STATISTICS_STDDEV=22.082178859328
            STATISTICS_VALID_PERCENT=100
          Image Structure Metadata:
            COMPRESSION=JPEG2000
        Band 3 Block=256x256 Type=Byte, ColorInterp=Blue
          Minimum=0.000, Maximum=255.000, Mean=73.839, StdDev=17.678
          Overviews: 5490x5490, 2745x2745, 1373x1373, 687x687
          Overviews: arbitrary
          Metadata:
            STATISTICS_MAXIMUM=255
            STATISTICS_MEAN=73.838878329866
            STATISTICS_MINIMUM=0
            STATISTICS_STDDEV=17.678142817323
            STATISTICS_VALID_PERCENT=100
          Image Structure Metadata:
            COMPRESSION=JPEG2000

Na disku vzniknul nový soubor ``data/T33UWQ_20220907T095549_TCI.jp2.aux.xml``

gdalinfo -hist
^^^^^^^^^^^^^^

Parametr ``-hist`` vypíše tabulku výskytů jednotlivých kategorií pro možnost vykreslení histogramu

.. code-block::

        gdalinfo -hist data/T33UWQ_20220907T095549_B08.jp2

Příklad výstupu:

.. code-block::

   [...]
   
   256 buckets from 579.969 to 8276.03:
   0 0 1 0 0 1 0 0 1 0 0 0 0 0 0 0 1 1 0 1 1 8428 24437 56401 53731 56247 74499 81653 79604 79965 78112 69240 67644 59171 56711 56247 54882 56177 57549 60929 64475 71049 79493 88519 101375 119590 141644 162705 189296 207828 236952 269722 308810 351060 393979 440867 496009 554174 612793 673703 732310 790614 846015 903133 989726 1010958 1059956 1113375 1168598 1229195 1285554 1351145 1420770 1498909 1583723 1668619 1749671 1833678 1904475 1968203 2093270 2066687 2100146 2120025 2133360 2140404 2150282 2157996 2163356 2164500 2169802 2175141 2181199 2183278 2179269 2173487 2226387 2135036 2110848 2070850 2035970 1988539 1943975 1892383 1832933 1774318 1719171 1660722 1595008 1532286 1471973 1407072 1387964 1276859 1217222 1151069 1094475 1037440 982320 931935 881482 833494 786939 742827 700823 660809 621171 585484 567164 514574 483225 452426 423775 394959 370056 345944 322196 302255 280382 261592 243568 227764 213381 207015 187404 176561 165012 156262 146643 138848 131045 124348 118376 111220 106034 100592 95664 90482 86125 84109 77797 74307 70906 67680 63995 60693 57739 54622 51515 48745 46018 43566 40716 38365 36133 35307 32717 30623 29410 28596 26726 25641 24217 22637 21647 20215 19263 18205 16853 16067 14783 13846 12509 11639 10795 9791 9123 8534 7974 7368 6984 6650 6059 5885 5741 5384 5045 4849 4329 3876 3768 3357 3337 3216 3056 2807 2710 2634 2405 2375 2360 2319 2269 2201 2196 2170 2103 2071 2102 1951 1903 1860 1786 1835 1777 1787 1738 1722 1617 1651 1524 1574 1503 1483 1436 1389 1394 1368 1375 1304 1218 1201 1130 1228 1148 33666 
   [...]

gdalinfo -json
^^^^^^^^^^^^^^

Parametr ``-json`` dá stejný výstup, ale místo špatně zpracovatelného textového formátu bude výstup ve formátu JSON

.. code-block::

        gdalinfo -json data/T33UWQ_20220907T095549_B08.jp2

Příklad výstupu:

.. code-block::

        {
          "description":"data/T33UWQ_20220907T095549_B08.jp2",
          "driverShortName":"JP2OpenJPEG",
          "driverLongName":"JPEG-2000 driver based on OpenJPEG library",
          "files":[
            "data/T33UWQ_20220907T095549_B08.jp2",
            "data/T33UWQ_20220907T095549_B08.jp2.aux.xml"
          ],
          "size":[
            10980,
            10980
          ],
          "coordinateSystem":{
            "wkt":"PROJCRS[\"WGS 84 / UTM zone 33N\",\n    BASEGEOGCRS[\"WGS 84\",\n        ENSEMBLE[\"World Geodetic System 1984 ensemble\",\n            MEMBER[\"World Geodetic System 1984 (Transit)\"],\n            MEMBER[\"World Geodetic System 1984 (G730)\"],\n            MEMBER[\"World Geodetic System 1984 (G873)\"],\n            MEMBER[\"World Geodetic System 1984 (G1150)\"],\n            MEMBER[\"World Geodetic System 1984 (G1674)\"],\n            MEMBER[\"World Geodetic System 1984 (G1762)\"],\n            MEMBER[\"World Geodetic System 1984 (G2139)\"],\n            ELLIPSOID[\"WGS 84\",6378137,298.257223563,\n                LENGTHUNIT[\"metre\",1]],\n            ENSEMBLEACCURACY[2.0]],\n        PRIMEM[\"Greenwich\",0,\n            ANGLEUNIT[\"degree\",0.0174532925199433]],\n        ID[\"EPSG\",4326]],\n    CONVERSION[\"UTM zone 33N\",\n        METHOD[\"Transverse Mercator\",\n            ID[\"EPSG\",9807]],\n        PARAMETER[\"Latitude of natural origin\",0,\n            ANGLEUNIT[\"degree\",0.0174532925199433],\n            ID[\"EPSG\",8801]],\n        PARAMETER[\"Longitude of natural origin\",15,\n            ANGLEUNIT[\"degree\",0.0174532925199433],\n            ID[\"EPSG\",8802]],\n        PARAMETER[\"Scale factor at natural origin\",0.9996,\n            SCALEUNIT[\"unity\",1],\n            ID[\"EPSG\",8805]],\n        PARAMETER[\"False easting\",500000,\n            LENGTHUNIT[\"metre\",1],\n            ID[\"EPSG\",8806]],\n        PARAMETER[\"False northing\",0,\n            LENGTHUNIT[\"metre\",1],\n            ID[\"EPSG\",8807]]],\n    CS[Cartesian,2],\n        AXIS[\"(E)\",east,\n            ORDER[1],\n            LENGTHUNIT[\"metre\",1]],\n        AXIS[\"(N)\",north,\n            ORDER[2],\n            LENGTHUNIT[\"metre\",1]],\n    USAGE[\n        SCOPE[\"Engineering survey, topographic mapping.\"],\n        AREA[\"Between 12°E and 18°E, northern hemisphere between equator and 84°N, onshore and offshore. Austria. Bosnia and Herzegovina. Cameroon. Central African Republic. Chad. Congo. Croatia. Czechia. Democratic Republic of the Congo (Zaire). Gabon. Germany. Hungary. Italy. Libya. Malta. Niger. Nigeria. Norway. Poland. San Marino. Slovakia. Slovenia. Svalbard. Sweden. Vatican City State.\"],\n        BBOX[0,12,84,18]],\n    ID[\"EPSG\",32633]]",
            "dataAxisToSRSAxisMapping":[
              1,
              2
            ]
          },
          "geoTransform":[
            499980.0,
            10.0,
            0.0,
            5500020.0,
            0.0,
            -10.0
          ],
          "metadata":{
          },

        [...]
        }


