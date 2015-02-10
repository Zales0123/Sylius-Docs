Importer and Exporter
=======================

The crucial classes in SyliusImportExportComponent are ``Importer`` and ``Exporter``. They provide main logic of component and control appropriate import/export workflow.


Importer
---------

 <to be written>


Exporter
---------

Exporter manage all export logic, get proper reader and writer and use them to create target effect. Exporter class contains following fields:

+---------------------+------------------------------------------------------------------------+
| Attribute           | Description                                                            |
+=====================+========================================================================+
| readerRegistry      | Registry that containes all correctly registered readers               |
+---------------------+------------------------------------------------------------------------+
| writerRegistry      | Registry that containes all correctly registered writers               |
+---------------------+------------------------------------------------------------------------+
| exportJobRepository | Repository of ExportJob entities, using to create them                 |
+---------------------+------------------------------------------------------------------------+
| entityManager       | EntityManager injected to persist created/updated objects to database  |
+---------------------+------------------------------------------------------------------------+
| logger              | Logger used to log exceptions, but also jobs' startTime and endTime    |
+---------------------+------------------------------------------------------------------------+

.. note::

    This class implements ``ExporterInterface``.


ExporterInterface
------------------

To be able to manage export actions, ``Exporter`` implements ``ExporterInterface``.

+------------------------------------------------+---------------------------------------------+
| Method                                         | Description                                 |
+================================================+=============================================+
| export(ExportProfileInterface $exportProfile)  | Manage export logic for given exportProfile |
+------------------------------------------------+---------------------------------------------+

.. important::

    Function ``export(ExportProfileInterface $exportProfile)`` is clue of exporting system. It get appropriate exportProfile reader, reads data and forward them to exportProfile writer. It also create exportJob for every export action and log crucial informations about them.