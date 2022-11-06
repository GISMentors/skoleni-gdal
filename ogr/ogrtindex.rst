ogrtindex
---------

`ogrtindex <https://gdal.org/programs/ogrtindex.html>`_ - vytvoří prostorový
index vektorových dat


.. code-block::


        Usage: ogrtindex [-lnum n]... [-lname name]... [-f output_format]
                         [-write_absolute_path] [-skip_different_projection]
                         [-t_srs target_srs]
                         [-src_srs_name field_name] [-src_srs_format [AUTO|WKT|EPSG|PROJ]
                         [-accept_different_schemas]
                         output_dataset src_dataset...

          -lnum n: Add layer number 'n' from each source file
                   in the tile index.
          -lname name: Add the layer named 'name' from each source file
                       in the tile index.
          -f output_format: Select an output format name.
          -tileindex field_name: The name to use for the dataset name.
                                 Defaults to LOCATION.
          -write_absolute_path: Filenames are written with absolute paths.
          -skip_different_projection: Only layers with same projection ref 
                as layers already inserted in the tileindex will be inserted.
          -accept_different_schemas: by default ogrtindex checks that all layers inserted
                                     into the index have the same attribute schemas. If you
                                     specify this option, this test will be disabled. Be aware that
                                     resulting index may be incompatible with MapServer!
          - If -t_srs is specified, geometries of input files will be transformed to the desired
            target coordinate reference system.
            Note that using this option generates files that are NOT compatible with MapServer < 7.2.
          - Simple rectangular polygons are generated in the same coordinate reference system
            as the vectors, or in target reference system if the -t_srs option is used.

        If no -lnum or -lname arguments are given it is assumed that
        all layers in source datasets should be added to the tile index
        as independent records.

Příklad použití:

.. code-block::

        ogrtindex tindex-shp.gpkg _data/*.shp

