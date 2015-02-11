Forms
=====

The bundle ships with a useful form types for export and import profile, but also for default readers and writers.

Export form
------------

The export profile form type is named ``sylius_export_profile`` and you can create it whenever you need, using the form factory.

.. code-block:: php

    <?php

    // src/Acme/DemoBundle/Controller/DemoController.php

    namespace Acme\DemoBundle\Controller;

    use Symfony\Bundle\FrameworkBundle\Controller\Controller;
    use Symfony\Component\HttpFoundation\Request;

    class DemoController extends Controller
    {
        public function fooAction(Request $request)
        {
            $form = $this->get('form.factory')->create('sylius_export_profile');
        }
    }

The default export profile form consists of following fields.

+-----------------+----------+
| Field           | Type     |
+=================+==========+
| name            | text     |
+-----------------+----------+
| description     | textarea |
+-----------------+----------+
| code            | text     |
+-----------------+----------+
| reader          | choice   |
+-----------------+----------+
| writer          | choice   |
+-----------------+----------+

You can render each of these using the usual Symfony way ``{{ form_row(form.description) }}``.

**SyliusImportExportBundle provides some default export readers and export writers. Each of them have custom configuration and adds diffrent part to export profile form.**

Readers
########

Basic readers extend same time provider. This implementation results in same configuration fields for two different export readers.

.. caution::

    Default export readers are part of SyliusCoreBundle, cause they are strictly connected with Sylius database.

Already available export readers:
    * Product reader
    * User reader

+---------------------------+-------------+
| Field                     | Type        |
+===========================+=============+
| Rows number               | text        |
+---------------------------+-------------+

Product reader
""""""""""""""""""""
Provides data of products in your system

User reader
""""""""""""""""""""
Provides data of users in your system


Writers
############

Csv Writer
""""""""""""""""

+-----------------+------------+
| Field           | Type       |
+=================+============+
| delimiter       | character  |
+-----------------+------------+
| enclosure       | character  |
+-----------------+------------+
| file path       | text       |
+-----------------+------------+

Allows to export data to csv file on given file path, formated with given delimiter and enclosure.


Import form
------------

The import profile form type is named ``sylius_import_profile`` and you can create it whenever you need, using the form factory.

.. code-block:: php

    <?php

    // src/Acme/DemoBundle/Controller/DemoController.php

    namespace Acme\DemoBundle\Controller;

    use Symfony\Bundle\FrameworkBundle\Controller\Controller;
    use Symfony\Component\HttpFoundation\Request;

    class DemoController extends Controller
    {
        public function fooAction(Request $request)
        {
            $form = $this->get('form.factory')->create('sylius_import_profile');
        }
    }

The default import profile form consists of following fields.

+-----------------+----------+
| Field           | Type     |
+=================+==========+
| name            | text     |
+-----------------+----------+
| description     | textarea |
+-----------------+----------+
| code            | text     |
+-----------------+----------+
| reader          | choice   |
+-----------------+----------+
| writer          | choice   |
+-----------------+----------+

You can render each of these using the usual Symfony way ``{{ form_row(form.description) }}``.

**SyliusImportExportBundle provides some default import readers and import writers. Each of them have custom configuration and adds diffrent part to import profile form.**

Readers
########

Csv Reader
""""""""""""""""""""

+-----------------+------------+
| Field           | Type       |
+=================+============+
| delimiter       | character  |
+-----------------+------------+
| enclosure       | character  |
+-----------------+------------+
| batch           | text       |
+-----------------+------------+
| file path       | text       |
+-----------------+------------+

Allows to import csv file (from given file path), formatted with given delimiter and enclosure. Import rows number given in batch field.


Writers
############

Basic writers extend same time provider. This implementation results in same configuration fields for two different import writers.

.. caution::

    Default import writers are part of SyliusCoreBundle, cause they are strictly connected with Sylius database.


Already available export readers:
    * Product reader
    * User reader

+---------------------------+-------------+
| Field                     | Type        |
+===========================+=============+
| Update existing records?  | checkbox    |
+---------------------------+-------------+

Product writer
""""""""""""""""""""
Allows to import data to products' table in database.

User writer
""""""""""""""""""""
Allows to import data to users' table in database.