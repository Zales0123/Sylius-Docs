Basic Models
============

The Profile
-----------

Profile is the main model in SyliusImportExportComponent. This simple class represents every unique import/export profile in the system.
The default model contains the following attributes with appropriate setters and getters.

 .. warning::

    Profile is an abstract class, so it's impossible to create its instace. It is only used to provide appropriate fields and basic methods for ExportProfile and ImportProfile.

+----------------------+-------------------------------------------------------------------------+
| Attribute            | Description                                                             |
+======================+=========================================================================+
| id                   | Unique id of the profile                                                |
+----------------------+-------------------------------------------------------------------------+
| name                 | Name of the profile                                                     |
+----------------------+-------------------------------------------------------------------------+
| code                 | Unique code of the profile                                              |
+----------------------+-------------------------------------------------------------------------+
| description          | Description of your amazing profile                                     |
+----------------------+-------------------------------------------------------------------------+
| writer               | Name of the writer that is used to import data to or export from system |
+----------------------+-------------------------------------------------------------------------+
| writerConfiguration  | Configuration of used writer                                            |
+----------------------+-------------------------------------------------------------------------+
| reader               | Name of the reader that is used to read data from appropriate source    |
+----------------------+-------------------------------------------------------------------------+
| readerConfiguration  | Configuration of used reader                                            |
+----------------------+-------------------------------------------------------------------------+

.. note::

    This model implements ``ProfileInterface``.


The ImportProfile/ExportProfile
------------------------------

ImportProfile and ExportProfile are representing opposite profile types. They both doesn't contain any extra fields, only extends ``Profile`` class and provides custom implementation of ``addJob(JobInterface $job)`` and ``removeJob(JobInterface $job)`` methods.

.. note::

    ExportProfile model implements ``ExportProfileInterface``.
    ImportProfile model implements ``ImportProfileInterface``.


The Job
-----------

Job model represents every unique elicitation of import or export. The default model contains the following attributes with appropriate setters and getters.

 .. warning::

    Job is an abstract class, so it's impossible to create its instace. It is only used to provide appropriate fields and basic methods for ExportJob and ImportJob.

+--------------+--------------------------------------------+
| Attribute    | Description                                |
+==============+============================================+
| id           | Unique id of the job                       |
+--------------+--------------------------------------------+
| status       | Current status of the job                  |
+--------------+--------------------------------------------+
| startTime    | Date and time when job has started         |
+--------------+--------------------------------------------+
| endTime      | Date and time when job has ended           |
+--------------+--------------------------------------------+
| createdAt    | Date and time when job has been created    |
+--------------+--------------------------------------------+
| updatedAt    | Date and time when job has been updated    |
+--------------+--------------------------------------------+


.. note::

    This model implements ``JobInterface``.

.. tip::

    Currently available statuses are:
        - 'running'
        - 'completed'
        - 'failed'


The ImportJob
---------------

ImportJob represents every single activation of import action. It extends abstract class ``Job`` and provides following extra fields:

+----------------+----------------------------------------------------+
| Attribute      | Description                                        |
+================+====================================================+
| importProfile  | ImportProfile instance that has been accomplished  |
+----------------+----------------------------------------------------+

.. note::

    This model implements ``ImportJobInterface``.


The ExportJob
---------------

ExportJob represents every single activation of export action. It extends abstract class ``Job`` and provides following extra fields:

+----------------+----------------------------------------------------+
| Attribute      | Description                                        |
+================+====================================================+
| exportProfile  | ExportProfile instance that has been accomplished  |
+----------------+----------------------------------------------------+

.. note::

    This model implements ``ExportJobInterface``.


ImportJobInterface
----------------------

To characterize import job object, its class needs to implement the ``ImportJobInterface``.

+------------------------------------------------+---------------------------------------------+
| Method                                         | Description                                 |
+================================================+=============================================+
| getImportProfile                               | Returns importProfile used by this job      |
+------------------------------------------------+---------------------------------------------+
| setImportProfile(ImportProfile $importProfile) | Sets importProfile to allow to use this job |
+------------------------------------------------+---------------------------------------------+

.. note::

    This interface extends ``JobInterface``.


ExportJobInterface
----------------------

To characterize import job object, its class needs to implement the ``ExportJobInterface``.

+------------------------------------------------+---------------------------------------------+
| Method                                         | Description                                 |
+================================================+=============================================+
| getExportProfile                               | Returns exportProfile used by this job      |
+------------------------------------------------+---------------------------------------------+
| setExportProfile(ExportProfile $exportProfile) | Sets exportProfile to allow to use this job |
+------------------------------------------------+---------------------------------------------+

.. note::

    This interface extends ``JobInterface``.


