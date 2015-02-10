Readers and Writers
=====================

SyliusImportExportComponent provides some default readers and writers, that allows you quickly generate your first import and exports.

Import readers
----------------

CsvReader
***********

CsvReader is default reader, that reads data from given csv file. Its configuration must contains delimiter, enclosure, target file path and batch size (number of rows that is going to be read).
It contains the following attributes:

.. attention::
    
    CsvReader uses ``EasyCSV`` library to manage csv files.

+----------------+----------------------------------------------------------------------------+
| Attribute      | Description                                                                |
+================+============================================================================+
| running        | Shows if csvReader has already been initialized                            |
+----------------+----------------------------------------------------------------------------+
| csvWriter      | EasySCV\Reader object that is used to read from csv file                   |
+----------------+----------------------------------------------------------------------------+
| configuration  | Reader configuration (delimiter, enclosure, batch size, target file path)  |
+----------------+----------------------------------------------------------------------------+

.. note::

    CsvReader class implements ``ReaderInterface``

Import writers
----------------

<import writers description - to be written>

.. warning::
 
    Import writers are part of SyliusCoreBundle cause they are strictly connected with database operations.

Export readers
----------------

<export readers description - to be written>

.. warning::
 
    Export readers are part of SyliusCoreBundle cause they are strictly connected with database operations.

Export writers
----------------

CsvWriter
**********

CsvWriter is default writer, that generates csv file with given configuration. It is possible to set chosen delimiter, enclosure and file path.
It contains the following attributes:

.. attention::
    
    CsvWriter uses ``EasyCSV`` library to manage csv files.

+----------------+----------------------------------------------------------------+
| Attribute      | Description                                                    |
+================+================================================================+
| running        | Shows if csvWriter has already been initialized                |
+----------------+----------------------------------------------------------------+
| csvWriter      | EasySCV\Writer object that is used to generate csv file        |
+----------------+----------------------------------------------------------------+
| configuration  | Writer configuration (delimiter, enclosure, target file path)  |
+----------------+----------------------------------------------------------------+
| isHeaderSet    | Shows has csv headers has already been set                     |
+----------------+----------------------------------------------------------------+

.. note::

    CsvWriter class implements ``WriterInterface``


ReaderInterface
----------------

To be able to import data properly, each reader must implement ``ReaderInterface``.

+-----------------------------------------+-----------------------------------------------------+
| Method                                  | Description                                         |
+=========================================+=====================================================+
| read()                                  | Reads data with given configuration                 |
+-----------------------------------------+-----------------------------------------------------+
| setConfiguration(array $configuration)  | Reader configuration                                |
+-----------------------------------------+-----------------------------------------------------+
| getType()                               | Reader type (necessary to register writer properly) |
+-----------------------------------------+-----------------------------------------------------+


WriterInterface
----------------

To be able to export data properly, each writer must implement ``WriterInterface``.

+-----------------------------------------+-----------------------------------------------------+
| Method                                  | Description                                         |
+=========================================+=====================================================+
| write(array $items)                     | Writes data with given configuration                |
+-----------------------------------------+-----------------------------------------------------+
| setConfiguration(array $configuration)  | Writer configuration                                |
+-----------------------------------------+-----------------------------------------------------+
| getType()                               | Writer type (necessary to register writer properly) |
+-----------------------------------------+-----------------------------------------------------+