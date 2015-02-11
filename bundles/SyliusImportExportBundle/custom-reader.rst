Adding custom reader
=======================

SyliusImportExportBundle has some default readers implemented, however, obviously they can be insufficient for some e-commerce systems. This chapter shows step-by-step way, how to add new import and export reader to make import/export system customization easier and more corresponding to your needs.

Custom import reader
---------------------

Create custom reader class
##############################

First step is creation of our new reader class. It must implement ``Sylius\Component\ImportExport\Reader\ReaderInterface``. Because of implementation, reader class must provide three methods:
    - ``read()``, which import data from source given in configuration
    - ``setConfiguration(array $configuration)``, which sets reader necessary configuration
    - ``getType``, which returns unique name of reader

.. code-block:: php

    <?php

    namespace Acme\DemoBundle\Reader;

    use Sylius\Component\ImportExport\Reader\ReaderInterface;

    class CustomReader implements ReaderInterface
    {
        /**
         * @var array
         */
        private $configuration;

        public function read()
        {
            //Some operations, that allows you to read data from given source
        }

        public function setConfiguration(array $configuration)
        {
            $this->configuration = $configuration; // just an example, you can do this your own way
        }

        public function getType()
        {
            return 'custom_reader';
        }
    }

Create reader configuration type
###################################

Each reader has its own, specific configuration form, which is added to main import profile form. It has to extend ``Symfony\Component\Form\AbstractType``. To be able to configure your reader in form, this class should override ``buildForm(FormBuilderInterface $builder, array $options)`` method. It should also have ``getName`` method, that returns reader's string identifier.

.. code-block:: php

    <?php

    namespace Acme\DemoBundle\Form\Type\Reader;

    use Symfony\Component\Form\AbstractType;
    use Symfony\Component\Form\FormBuilderInterface;

    /**
     * Custom reader configuration form type
     */
    class CustomReaderType extends AbstractType
    {
        public function buildForm(FormBuilderInterface $builder, array $options)
        {
            $builder
                ->add('file', 'text', array(
                    'label' => 'acme.form.import.reader.label',
                    'required' => true,
                ))
            ;
        }

        public function getName()
        {
            return 'acme_custom_reader';
        }
    }


Register custom reader class as service
##########################################

To be able to use your new reader, it must be registered as service in your services' file. You should take care of two classes we just created, means ``CustomReader`` and ``CustomReaderType``. They have to be tagged with proper tags, to be visible for CompilerPass.

.. code-block:: xml

    <parameters>
        //other parameters
        <parameter key="acme.import.custom_reader.class">Acme\DemoBundle\Reader\CustomReader</parameter>
        <parameter key="acme.form.type.reader.custom_type.class">Acme\DemoBundle\Form\Type\Reader\CustomReaderType</parameter>
    </parameters>

    <services>
        //other services
        <service id="acme.import.custom_reader" class="%acme.import.custom_reader.class%">
            <tag name="acme.import.reader" reader="custom_reader" label="Custom reader" />
        </service>
        <service id="acme.form.type.reader.custom_type" class="%acme.form.type.reader.custom_type.class%">
            <tag name="form.type" alias="acme_custom_reader" />
        </service>
    </services>


Custom export reader
---------------------

<to be written>


Summary
----------

With this three simple steps, you can create your own, great reader, which allows you to read data however you want and use it for one of the writers.