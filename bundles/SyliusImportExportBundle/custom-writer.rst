Adding custom writer
=======================

SyliusImportExportBundle has some default writers implemented, however, obviously they can be insufficient for some e-commerce systems. This chapter shows step-by-step way, how to add new import and export writer to make import/export system customization easier and more corresponding to your needs.

Custom import writer
---------------------

<to be written>

Custom export writer
---------------------

Create custom writer class
##############################

First step is creation of our new writer class. It must implement ``Sylius\Component\ImportExport\Writer\WriterInterface``. Because of implementation, writer class must provide three methods:
    - ``write(array $items)``, which export data wherever you need, using given configuration
    - ``setConfiguration(array $configuration)``, which sets writer necessary configuration
    - ``getType``, which returns unique name of writer

.. code-block:: php

    <?php

    namespace Acme\DemoBundle\Writer;

    use Sylius\Component\ImportExport\Writer\WriterInterface;

    class CustomWriter implements WriterInterface
    {
        /**
         * @var array
         */
        private $configuration;

        public function write(array $items)
        {
            //Some operations on given data, that export it however you want
        }

        public function setConfiguration(array $configuration)
        {
            $this->configuration = $configuration; // just an example, you can do this your own way
        }

        public function getType()
        {
            return 'custom_writer';
        }
    }

Create writer configuration type
###################################

Each writer has its own, specific configuration form, which is added to main export profile form. It has to extend ``Symfony\Component\Form\AbstractType``. To be able to configure your writer in form, this class should override ``buildForm(FormBuilderInterface $builder, array $options)`` method. It should also have ``getName`` method, that returns writer's string identifier.

.. code-block:: php

    <?php

    namespace Acme\DemoBundle\Form\Type\Writer;

    use Symfony\Component\Form\AbstractType;
    use Symfony\Component\Form\FormBuilderInterface;

    /**
     * Custom writer configuration form type
     */
    class CustomWriterType extends AbstractType
    {
        public function buildForm(FormBuilderInterface $builder, array $options)
        {
            $builder
                ->add('file', 'text', array(
                    'label' => 'acme.form.export.writer.label',
                    'required' => true,
                ))
            ;
        }

        public function getName()
        {
            return 'acme_custom_writer';
        }
    }


Register custom writer class as service
##########################################

To be able to use your new writer, it must be registered as service in your services' file. You should take care of two classes we just created, means ``CustomWriter`` and ``CustomWriterType``. They have to be tagged with proper tags, to be visible for CompilerPass.

.. code-block:: xml

    <parameters>
        //other parameters
        <parameter key="acme.export.custom_writer.class">Acme\DemoBundle\Writer\CustomWriter</parameter>
        <parameter key="acme.form.type.writer.custom_type.class">Acme\DemoBundle\Form\Type\Writer\CustomWriterType</parameter>
    </parameters>

    <services>
        //other services
        <service id="acme.export.custom_writer" class="%acme.export.custom_writer.class%">
            <tag name="acme.export.writer" writer="custom_writer" label="Custom writer" />
        </service>
        <service id="acme.form.type.writer.custom_type" class="%acme.form.type.writer.custom_type.class%">
            <tag name="form.type" alias="acme_custom_writer" />
        </service>
    </services>


Summary
----------

With this three simple steps, you can create your own, great writer, which allows you to write exported/imported data however and wherever you want.