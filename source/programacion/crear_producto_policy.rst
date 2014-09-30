.. -*- coding: utf-8 -*-

.. _producto_policy:

========================================
Creación de un producto de configuración
========================================

.. sidebar:: Sobre este artículo

    :Autor(es): Carlos de la Guardia, Leonardo J. Caballero G.
    :Correo(s): carlos.delaguardia@gmail.com, leonardocaballero@gmail.com
    :Compatible con: Plone 3, Plone 4
    :Fecha: 29 de Septiembre de 2014

En esta articulo busca explicar como crear paquetes de configuración general de 
un sitio representando las reglas generales de manejo de sitios para Plone 3, 
Plone 4 y Plone 5.

.. _producto_policy_intro:

Introducción
============

Se detallan los pasos para crear un producto de configuración y se describe
cada uno de los directorios y archivos importantes generados.

Un producto de configuración (**"policy product"**) incluye toda la configuración
general del sitio. Representa las reglas generales de manejo de sitios Plone
de una organización y puede incluir:

* Configuraciones del sitio y propiedades de navegación.

* Productos propios y de terceros que deben instalarse automáticamente
  con el sitio Web.

* Configuraciones de los Viewlets utilizados en el sitio Web.

* Estructura inicial de contenido del sitio Web.

* Pasos adicionales a la instalación del producto, como creación de
  cuentas de usuarios y contenido personalizado.

* Configuraciones de los Portlets utilizados en el sitio Web.

* Flujo de trabajos generales de la organización.

Muchos programadores prefieren crear un simple producto de configuración (también
conocido como un producto de despliegue **"deployment product"**) que orquesta
varias dependencias del proyecto.

.. _producto_policy_generar:

Generación con paster
=====================

El primer paso para la creación del producto se hace utilizando el esqueleto
de paquete para Plone proporcionado por :command:`paster`:

.. tip::
    Debe tener instalado el paquete :ref:`ZopeSkel <skel_plone>` para poder 
    usar el comando :command:`paster`.

.. note:: 
    Debe estar dentro el directorio :file:`src/` de su instalación el cual 
    fungirá como directorio que contendrá los paquetes en desarrollo.

.. code-block:: sh

    $ paster create -t plone cliente1.policy
    Selected and implied templates:
      templer.core#basic_namespace  A basic Python project with a namespace package
      ZopeSkel#plone                A project for Plone add-ons

    Variables:
      egg:      cliente1.policy
      package:  cliente1policy
      project:  cliente1.policy
    Expert Mode? (What question mode would you like? (easy/expert/all)?) ['easy']:

A continuación, :command:`paster` realiza algunas preguntas para personalizar 
la generación del paquete. La primera es si desea contestar todas las preguntas 
(``all``) o solo algunas (``easy``). Usted debe contestar ``all``.

Después le pregunta los nombres del paquete ``Namespace`` (primera parte del 
nombre pasado al template) y el nombre del paquete (segunda parte). Como los
valores por omisión son los mismos que le paso como parámetros en el comando 
anterior, basta presiona la tecla ``Enter`` en las siguientes dos preguntas.

.. code-block:: sh

    Namespace Package Name (Name of outer namespace package) ['cliente1']:
    Package Name (Name of the inner namespace package) ['policy']: 

.. tip::
    #. el espacio de nombres se usa para poder agrupar varios paquetes bajo 
       un mismo nombre.

    #. el nombre del paquete en sí.
    
La versión del paquete se utiliza en el :menuselection:`Configuración del sitio --> Complementos`
para mostrar al usuario la versión instalada del producto.

.. code-block:: sh

    Version (Version number for project) ['1.0']: 0.1

Después, se pide una corta descripción del paquete; este y los datos que siguen 
son para los metadatos del proyecto en el :term:`PyPI`:.

.. tip::
    los metadatos del paquete es para definir un perfil de registro para subir 
    el paquete a un repositorio como el :term:`Python Package Index`.

.. code-block:: sh

    Description (One-line description of the project) ['']: Plone site policy for Cliente1 website
    Register Profile (Should this package register a GS Profile) [False]: True
    Long Description (Multi-line description (in ReST)) ['']: a Plone site policy package for Cliente1 website
    Author (Name of author for project) ['']: Leonardo J. Caballero G.
    Author Email (Email of author for project) ['']: plone-developers@lists.sourceforge.net
    Keywords (List of keywords, space-separated) ['']: plone policy package cliente1 website
    Project URL (URL of the homepage for this project) ['http://svn.plone.org/svn/collective/']: https://github.com/plone-ve/cliente1.policy
    Project License (Name of license for the project) ['GPL']: GPLv2
    
Siempre ocupara el valor por defecto, debe ser ``False`` para funcionar bien
en Zope 2.

.. code-block:: sh

    Zip-Safe? (Can this project be used as a zipped egg? (true/false)) [False]: 
    
Finalmente, esta ultima pregunta siempre debe ser ``True`` para funcionar
en Zope 2.

.. code-block:: sh

    Zope2 Product? (Are you creating a product for Zope2/Plone or an Archetypes Product?) [True]: 
    Creating template basic_namespace
    Creating directory ./cliente1.policy
    ...
      Copying setup.py_tmpl to ./cliente1.policy/setup.py
    ------------------------------------------------------------------------------
    The project you just created has local commands. These can be used from within
    the product.

    usage: paster COMMAND

    Commands:
      addcontent  Adds plone content types to your project

    For more information: paster help COMMAND
    ------------------------------------------------------------------------------

Posibles errores
----------------

**IOError: No egg-info directory found**
  Este error se debe a que el directorio :file:`egg-info` fue generado para esto
  acceda al directorio :file:`cliente1.policy` y ejecute el siguiente comando: ::

    $ cd cliente1.policy
    $ python setup.py egg_info
    Traceback (most recent call last):
      File "setup.py", line 10, in <module>
        open(os.path.join("docs", "HISTORY.txt")).read(),
    IOError: [Errno 2] No such file or directory: 'docs/HISTORY.txt'

  La solución a este error es mover el :file:`CHANGES.txt` dentro del directorio
  :file:`docs/` con el nuevo nombre :file:`HISTORY.txt`, ejecutando el siguiente
  comando: ::

    $ mv CHANGES.txt docs/HISTORY.txt

  Luego genere la información del :file:`egg-info`, ejecutando el siguiente
  comando: ::

    $ python setup.py egg_info
    running egg_info
    creating src/cliente1.policy.egg-info
    writing requirements to src/cliente1.policy.egg-info/requires.txt
    writing src/cliente1.policy.egg-info/PKG-INFO
    writing namespace_packages to src/cliente1.policy.egg-info/namespace_packages.txt
    writing top-level names to src/cliente1.policy.egg-info/top_level.txt
    writing dependency_links to src/cliente1.policy.egg-info/dependency_links.txt
    writing entry points to src/cliente1.policy.egg-info/entry_points.txt
    writing paster_plugins to src/cliente1.policy.egg-info/paster_plugins.txt
    writing manifest file 'src/cliente1.policy.egg-info/SOURCES.txt'
    reading manifest file 'src/cliente1.policy.egg-info/SOURCES.txt'
    writing manifest file 'src/cliente1.policy.egg-info/SOURCES.txt'

**Distribution contains no modules or packages for namespace package 'cliente1'**
  Este error se debe a que el archivo :file:`setup.py` no tiene bien definida
  desde donde comenzara la búsqueda de los directorio del paquete, entonces
  corrijalo editando el archivo :file:`setup.py` y agregue las siguientes lineas: ::

      packages=find_packages('src', exclude=['ez_setup']),
      package_dir={'': 'src'},
      namespace_packages=['cliente1'],

.. _producto_policy_generado:

Esqueleto generado
==================

Este comando genera un directorio de distribución donde se encuentra
la información y código para distribuir el paquete resultante como
:term:`Egg`. Dentro de ese directorio se encuentra un sub-directorio
con el espacio de nombres general (en este ejemplo sería :file:`cliente1`)
y dentro de ese último el verdadero directorio del producto para Zope
(en este :file:`cliente1`, :file:`policy`).

::

    ./cliente1.policy/
    |-- cliente1
    |   `-- policy
    |       |-- configure.zcml
    |       |-- __init__.py
    |       |-- profiles
    |       |   `-- default
    |       |       `-- metadata.xml
    |       `-- tests.py
    |-- CONTRIBUTORS.txt
    |-- docs
    |   |-- HISTORY.txt
    |   |-- INSTALL.txt
    |   |-- LICENSE.GPL
    |   `-- LICENSE.txt
    |-- README.txt
    |-- setup.cfg
    |-- setup.py
    `-- src
        |-- cliente1
        |   |-- __init__.py
        |   `-- policy
        |       `-- __init__.py
        `-- cliente1.policy.egg-info
            |-- dependency_links.txt
            |-- entry_points.txt
            |-- namespace_packages.txt
            |-- not-zip-safe
            |-- paster_plugins.txt
            |-- PKG-INFO
            |-- requires.txt
            |-- SOURCES.txt
            `-- top_level.txt

Dentro del directorio del producto se encuentran los dos archivos
imprescindibles para crear un producto para Zope 2, junto con un
esqueleto de módulo para :file:`tests.py`:

* :file:`__init__.py`, incluye un método llamado ``initialize`` para
  que Zope reconozca el paquete como :term:`Producto`.

* :file:`configure.zcml`, es el archivo de :term:`ZCML`, que permite
  al producto utilizar código basado en Zope 3.

* :file:`tests.py`, esqueleto de módulo para ``tests``.

..
  Una vez generado el producto, usted debe agregar un directorio para almacenar la
  configuración de :ref:`Generic Setup <perfiles_genericsetup>`:
  
  .. code-block:: sh

      $ cd cliente1.policy/cliente1/policy
      $ mkdir -p profiles/default
  
  Después registre ese directorio creado como perfil, dentro del archivo :term:`ZCML` 
  :file:`configure.zcml` :
  
  .. code-block:: xml
  
      <genericsetup:registerProfile
           name="default"
           title="Cliente1 site policy"
           directory="profiles/default"
           description="Turn a Plone site into the Cliente1 site."
           provides="Products.GenericSetup.interfaces.EXTENSION"
           />
  
  Ahora ya es posible agregar dentro del directorio del perfil toda la configuración deseada.
  La manera recomendada de generar los archivos xml necesarios para ello, es crear un sitio
  nuevo de Plone y a continuación modificar toda la configuración que se quiere incluir en
  el producto. Una vez hecho esto, se debe exportar la configuración modificada desde la
  herramienta de :ref:`portal_setup <zmi_portal_setup>`, la cual se puede acceder a esta desde
  la raíz del portal desde la :ref:`administración de Zope (ZMI) <zmi>`:

  .. todo::
      Agregar capturas de pantallas para este procedimiento

  Al seleccionar los pasos deseados y presionar el botón de **Export selected steps**,
  se obtiene un archivo comprimido que contiene la configuración expresada en XML para
  todos los pasos seleccionados. Este archivo debe descomprimirse en el directorio del
  perfil creado en el paso anterior:

  .. todo::
      Agregar capturas de pantallas para este procedimiento

  .. code-block:: sh

      $ cd profiles/default
      $ tar xzf setuptool_20080630134421.tar.gz

.. _manipulando_dependencias:

Manipulando dependencias
========================

En Plone la resolución de dependencias de :term:`paquetes Egg`, es de
gran utilidad para garantizar la instalación de todas lo necesario para
el funcionamiento de su sitio Plone. Las dependencias de los :term:`paquetes Egg`
se definen en 2 o 3 lugares (contextos) distintos, entonces a continuación
se detalla donde y la utilidad contextual de cada uno:

.. tip:: Al menos debe realizar el *paso 1* y el *paso 2*.

#. Paso 1: el archivo :ref:`setup.py <policy_archivo_setup_py>`.

#. Paso 2: el archivo :ref:`metadata.xml <policy_archivo_metadata_xml>`.

#. Paso 3: opcionalmente los :ref:`archivos ZCML <policy_archivos_zcml>`.

.. _policy_archivo_setup_py:

El archivo setup.py
-------------------

El archivo :term:`setup.py` en este paquete incluye la declarativa
``install_requires`` a la cual puede indicar que dependencias de
:term:`paquetes Egg` son requeridas para la instalación de este producto.

Esto hace que se garantice que el todas las librerías Python o
productos Zope / Plone necesario para el uso de este paquete
estén instalado desde el contexto de instalación a nivel Python
con sus respectivos registros :term:`PYTHONPATH`.

En este caso se define la librería ``plone.api`` y el producto
``Products.PloneFormGen`` como dependencias de este paquete, la cual
se utilizara mas adelante. A continuación se muestra el código fuente
de ejemplo:

.. code-block:: python

    install_requires=[
        'setuptools',
        # -*- Extra requirements: -*-
        'plone.api',
        'Products.PloneFormGen==1.7.14',
    ],

Esta modificación al archivo :term:`setup.py` permite que se instale
en el :term:`PYTHONPATH` la librería ``plone.api`` y el producto
``Products.PloneFormGen``.

.. _policy_archivo_metadata_xml:

El archivo metadata.xml
-----------------------
El archivo :file:`metadata.xml` se usa para hacer
:ref:`referencia a perfiles <gs_referencia_perfiles>` de instalación de
productos y este archivo se ubica :file:`profiles/default/`. A continuación
se muestra el código fuente de ejemplo:

.. code-block:: xml

    <?xml version="1.0"?>
    <metadata>
      <version>1000</version>
      <dependencies>
        <dependency>profile-Products.PloneFormGen:default</dependency>
      </dependencies>
    </metadata>

Esta modificación al archivo :file:`metadata.xml` agregando la directriz
``<dependencies />`` permite que ``GenericSetup`` haga referencia a los
perfiles de instalación de las dependencias de este paquete.

.. note::
    Solo se agrega la directriz ``<dependency />`` los producto que poseen
    perfil de instalación ``GenericSetup``. Por esta razón librería ``plone.api``
    no se define esta sección.

.. _policy_archivos_zcml:

Los archivos ZCML
-----------------

El archivo :file:`configure.zcml` esta en el directorio
:file:`cliente1.policy/cliente1/policy/`, este define configuraciones
:term:`ZCML`, para este caso de configuraciones se usa para incluir el
:file:`dependencies.zcml` para las dependencias. Entonces debe editar
el archivo :file:`configure.zcml` y agregar el siguiente código a
continuación:

.. code-block:: xml

    <!-- -*- extra stuff goes here -*- -->

    <include file="dependencies.zcml" />

El archivo :file:`dependencies.zcml` debe crearse en el directorio
:file:`cliente1.policy/cliente1/policy/` (al mismo nivel del archivo
:file:`configure.zcml`), para este caso de configuraciones se usa para
incluir de paquetes necesarios como dependencias al contexto :term:`ZCML`.
Entonces debe crear el archivo :file:`dependencies.zcml` y agregar el
siguiente código a continuación:

.. code-block:: xml

    <configure
        xmlns="http://namespaces.zope.org/zope"
        i18n_domain="ploneconf2014.policy">

      <include package="Products.PloneFormGen" />

    </configure>

Esta modificación al archivo :file:`configure.zcml` y agregación del archivo
:file:`dependencies.zcml` la directriz ``<dependencies />`` permite que
``GenericSetup`` haga referencia a los perfiles de instalación de las dependencias
de este paquete.

.. note::
    Solo se agrega la directriz ``<dependency />`` los producto que poseen
    perfil de instalación ``GenericSetup``. Por esta razón librería ``plone.api``
    no se define esta sección.

De esta forma se resuelven dependencias al contexto Python para el :term:`PYTHONPATH`
y perfiles de instalación ``GenericSetup``.

.. _manipulando_instalacion:

Manipulando la Instalación
==========================

En algunas ocasiones hay pasos que requiere realizar al momento de la instalación
de un producto de configuración que no son manejables con
:ref:`Generic Setup <perfiles_genericsetup>`. En esos casos, existe un mecanismo
para ejecutar código Python en el momento que se instala un perfil.

Para ejecución de código Python a través de los :term:`pasos de importación` de
``GenericSetup`` debe crear varios archivos en 3 o 4 lugares (contextos) distintos,
entonces a continuación se detalla donde y la utilidad contextual de cada uno:

.. tip:: Debe realizar *todos los pasos*.

#. Paso 1: el archivo :ref:`config.py <policy_archivo_config_py>`.

#. Paso 2: el archivo :ref:`import_steps.xml <policy_archivo_importsteps_xml>`.

#. Paso 3: el archivo :ref:`setuphandlers.py <policy_archivo_setuphandlers_py>`.

#. Paso 4: el archivo :ref:`cliente1.policy_various.txt <policy_archivo_various_txt>`.

.. _policy_archivo_config_py:

El archivo config.py
--------------------

El archivo :file:`config.py` se usa para definir constantes del producto.

Se debe crear en el directorio :file:`cliente1.policy/cliente1/policy/`
un archivo :file:`config.py` (al mismo nivel del archivo :file:`configure.zcml`),
en la raíz del modulo de paquete, con el siguiente código:

.. code-block:: python

    # -*- coding: utf-8 -*-

    """
    Contains constants used by setuphandler.py
    """

    PROJECTNAME = 'cliente1.policy'

    DEPENDENCIES = [
        'plone.api',
        'Products.PloneFormGen',
        ]

Este archivo se estila usar de forma amplia en el producto, incluyendo
el archivo :ref:`setuphandlers.py <policy_archivo_setuphandlers_py>`.

.. _policy_archivo_importsteps_xml:

El archivo import_steps.xml
---------------------------

El archivo :file:`import_steps.xml` se usa para definir los :term:`pasos de importar`
de :ref:`GenericSetup <perfiles_genericsetup>`. Para enlazar este código con los pasos
de importación, existe un paso especial en ``GenericSetup``, llamado ``import_steps``.

Para activarlo, debe agregar el siguiente código dentro del archivo
:file:`import_steps.xml`, dentro del directorio :file:`profiles/default` (al mismo
nivel del archivo :ref:`metadata.xml <policy_archivo_metadata_xml>`), con el
siguiente código:

.. code-block:: xml

    <?xml version="1.0"?>
    <import-steps>
       <import-step id="cliente1.policy.various"
                    version="20080625-01"
                    handler="cliente1.policy.setuphandlers.setupVarious"
                    title="Cliente1 Policy: miscellaneous import steps">
         <dependency step="plone-content" />
         Various import steps that are not handled by GS import/export
         handlers.
       </import-step>
    </import-steps>

Con este archivo defines un directiva ``<import-step />`` en la cual define
un atributo llamado ``handler`` en el cual define un :term:`Nombre de puntos Python`
haciendo referencia al método :ref:`setupVarious <producto_policy_setupvarious>`
en el modulo :ref:`setuphandlers.py <policy_archivo_setuphandlers_py>`
del paquete ``cliente1.policy``, el cual se encargar de ejecutar las tareas
de importación y/o personalización del sitio Plone.

Lo único que puede variar dependiendo de lo que necesita hacer, es la parte
donde se listan los ``steps`` de dependencia, marcados por la etiqueta
``dependency`` en el XML. En el atributo ``step`` de la etiqueta ``dependency``
se debe colocar el nombre del paso que necesita que sea ejecutado antes que su
código. Se pueden agregar varias etiquetas ``dependency`` con distintos pasos
para el caso de que su código dependa de varios pasos.

.. _policy_archivo_various_txt:

El archivo cliente1.policy_various.txt
--------------------------------------

Para prevenir la ejecución de este código durante la instalación de otros
productos, se agrega un archivo de texto, llamado :file:`cliente1.policy_various.txt`,
dentro del directorio :file:`profiles/default` con el siguiente contenido:

.. code-block:: txt

    This file is used as a marker in setuphandlers.py.

Este archivo se usa para verifica su existencia dentro de este método
:ref:`setupVarious <producto_policy_setupvarious>` en el modulo :ref:`setuphandlers.py <policy_archivo_setuphandlers_py>`.

.. _policy_archivo_setuphandlers_py:

El archivo setuphandlers.py
---------------------------

El archivo :file:`setuphandlers.py` se usa para hacer realizar todas
las tareas que no se puede realizar usando directamente directivas
``GenericSetup``.

Se debe crear en el directorio :file:`cliente1.policy/cliente1/policy/`
un archivo :file:`setuphandlers.py` (al mismo nivel del archivo
:file:`configure.zcml`), en la raíz del modulo de paquete, con el
siguiente código:

.. code-block:: python

    import logging
    from plone import api
    from cliente1.policy.config import PROJECTNAME

    logger = logging.getLogger(PROJECTNAME)

    def setupVarious(context):
        """ miscellaneous import steps for setup """
        if context.readDataFile('cliente1.policy_various.txt') is None:
            return

        portal = api.portal.get()
        # aquí va el código particular

.. _producto_policy_setupvarious:

**método setupVarious**

El método ``setupVarious`` es donde se coloca el código particular para la
instalación, que puede hacer cualquier cosa que se necesite dentro del portal.

**Crear enlace**

A continuación un ejemplo que muestra como crear tipo de contenido de **Enlace**,
*a la vieja ultranza*:

.. code-block:: python

    def createLink(context, title, link):
        """
        Crea y publica un vínculo en el contexto dado.
        """
        id = idnormalizer.normalize(title, 'es')
        if not hasattr(context, id):
            context.invokeFactory('Link', id=id, title=title, remoteUrl=link)

.. tip::
    Este método debe definirse antes el método ``setupVarious`` se invoca en
    el orden que se requiere ejecutar, colocando debajo de la marca
    **"# aquí va el código particular"**.

**Crear carpetas**

A continuación un ejemplo que muestra como crear tipo de contenido de **Carpeta**,
*a la vieja ultranza*:

.. code-block:: python

    def createFolder(context, title, allowed_types=['Topic'], exclude_from_nav=False):
        """Crea una carpeta en el contexto especificado por omisión,
        la carpeta contiene colecciones (Topic).
        """
        id = idnormalizer.normalize(title, 'es')
        if not hasattr(context, id):
            context.invokeFactory('Folder', id=id, title=title)
            folder = context[id]
            folder.setConstrainTypesMode(constraintypes.ENABLED)
            folder.setLocallyAllowedTypes(allowed_types)
            folder.setImmediatelyAddableTypes(allowed_types)
            if exclude_from_nav:
                folder.setExcludeFromNav(True)
            folder.reindexObject()
            logger.info("Created the Folder called {0}".format(folder))
        else:
            folder = context[id]
            folder.setLocallyAllowedTypes(allowed_types)
            folder.setImmediatelyAddableTypes(allowed_types)
            # reindexamos para que el catálogo se entere de los cambios
            folder.reindexObject()

.. tip::
    Este método debe definirse antes el método ``setupVarious`` se invoca en
    el orden que se requiere ejecutar, colocando debajo de la marca
    **"# aquí va el código particular"**.

**Cambiar el flujo de trabajo**

A continuación un ejemplo que muestra como cambiar el Flujo de trabajo del
objeto utilizando CMFPlacefulWorkflow, *a la vieja ultranza*:

.. code-block:: python

    def set_workflow_policy(obj):
        """
        Cambiar el workflow del objeto utilizando CMFPlacefulWorkflow.
        """
        obj.manage_addProduct['CMFPlacefulWorkflow'].manage_addWorkflowPolicyConfig()
        pc = getattr(obj, WorkflowPolicyConfig_id)
        pc.setPolicyIn(policy='one-state')
        logger.info('Workflow changed for element %s' % obj.getId())

.. tip::
    Este método debe definirse antes el método ``setupVarious`` se invoca en
    el orden que se requiere ejecutar, colocando debajo de la marca
    **"# aquí va el código particular"**.

**Eliminación de contenidos**

A continuación un ejemplo que muestra como eliminar contenidos desde la método
``setupVarious`` en el modulo :ref:`setuphandlers.py <policy_archivo_setuphandlers_py>`:

.. code-block:: python

    import logging
    from plone import api
    from cliente1.policy.config import PROJECTNAME

    logger = logging.getLogger(PROJECTNAME)

    def remove_defaults_nav(portal):
        '''Remove defaults navegations and contents'''

        items_removable = ['news', 'events', 'Members', 'front-page']
        for item in items_removable:
          if hasattr(portal, item):
            try:
              api.content.delete(obj=portal[item])
              logger.info("Deleted {0} item".format(item))
            except AttributeError:
              logger.info("No {0} item detected. Hmm... strange. Continuing....".format(item))

    def setupVarious(context):
        """ miscellaneous import steps for setup """
        if context.readDataFile('cliente1.policy_various.txt') is None:
            return

        portal = api.portal.get()
        # aquí va el código particular
        remove_defaults_nav(portal)

.. seealso:: 
  
  -   Articulo sobre :ref:`Generic Setup <perfiles_genericsetup>`.

.. _producto_policy_instalar:

¿Cómo instalarlo?
=================

Luego de generar el producto de configuración debe agregar este a la configuración buildout 
para completar la instalación de este producto. Esto se realiza usando la herramienta 
:ref:`zc.buildout <que_es_zcbuildout>` para esto usted tiene que agregar el producto a las 
sección ``eggs`` del archivo :file:`buildout.cfg` como se muestra a continuación:

.. code-block:: cfg

  eggs =
      cliente1.policy
      
.. note::
    Debe tener habilitado la extensión :ref:`mr.developer <mrdeveloper>` para gestionar localmente
    el producto en desarrollo, y posterior publicación en un sistema de control de versiones.

Quizás dependiendo su configuración en la variable declarativa de ``auto-checkout`` de 
:ref:`mr.developer <mrdeveloper>` tiene que agregar la siguiente linea:

.. code-block:: cfg

  auto-checkout =
      cliente1.policy

.. tip:: Usted puede usar el comodín ``*`` en ves de cada linea con los paquetes en desarrollo, 
    lo cual le indicara a la extensión :ref:`mr.developer <mrdeveloper>` que compruebe local desde 
    el :term:`filesystem` o remotamente desde un :ref:`control de versiones <rcs_index>` todos los 
    paquetes de descritos en la sección ``sources``.

En la su sección declarativa ``sources`` del archivo :file:`buildout.cfg` tiene que agregar 
la siguiente linea:

.. code-block:: cfg

  [sources]
  cliente1.policy = fs cliente1.policy

.. tip:: la opción ``fs`` le indica a la extensión :ref:`mr.developer <mrdeveloper>` que 
    gestione el paquete localmente desde el :term:`filesystem` o sistema de archivo.

Luego ejecute el script :command:`buildout`, de la siguiente forma:

.. code-block:: sh

  $ ./bin/buildout -vN

Con este comando busca el paquete o sus dependencias en el repositorio :term:`PyPI`, 
descarga e instala el producto en su instancia Zope para sus sitios Plone allí hospedados.

.. note::
    Hasta este punto usted **NO** ha publicado *producto de configuración* en el
    repositorio :term:`PyPI`, mas si este tiene dependencias de instalación se
    descargaran e instalaran por usted.

Entonces inicie la :term:`Instancia de Zope`, de la siguiente forma:

.. code-block:: sh

  $ ./bin/instance fg 

Luego de esto ya tiene disponible el producto para ser habilitado en cada sitio 
Plone dentro de su :term:`Instancia de Zope`.

.. _producto_policy_habilitar:

Habilitarlo en Plone
====================

Para instalar de este producto de configuraciones existen varias formas de hacerlo, este 
proceso se hace en la mayoría de los casos manualmente como se describe cada uno a continuación:

.. _producto_policy_creacion_sitio:

Durante la creación del sitio
-----------------------------

Acceda al asistente `Crear un sitio Plone`_ allí indique el **id del sitio**, 
el **título corto** para el sitio,  seleccione el **idioma por defecto** para 
el sitio y seleccione cualquier complemento que quiera activar de forma inmediata 
durante la creación del sitio en la sección **Complementos** en nuestro caso y marque 
la casilla llamada **cliente1.policy** y luego presione el botón **Crear un Sitio Plone**.

.. todo::
    Agregar capturas de pantallas para este procedimiento

.. _producto_policy_post_creacion:

Posterior la creación del sitio
-------------------------------

Si :ref:`durante la creación del sitio <producto_policy_creacion_sitio>` no selecciono en la sección 
**Complementos** el producto **cliente1.policy**, puede realizar accediendo a la herramienta en 
:menuselection:`Configuración del Sitio --> Interfaz de Administración de Zope --> portal_quickinstaller` 
y marque la casilla llamada **cliente1.policy** y luego presione el botón **Install**.

.. todo::
    Agregar capturas de pantallas para este procedimiento

.. _producto_policy_ejecutar_perfil:

Ejecutar perfil de instalación
------------------------------

En **Plone 3** y **Plone 4** acceda a la herramienta en :menuselection:`Configuración del Sitio --> Interfaz de Administración de Zope --> portal_setup --> Import --> Select Profile or Snapshot` seleccione 
la lista desplegable llamada **cliente1.policy** luego desplace al final de la pagina y presione 
el botón **Import all steps**.

.. todo::
    Agregar capturas de pantallas para este procedimiento

.. _producto_policy_ejecutar_buildout:

Durante la ejecución Buildout
-----------------------------

Existe una receta Buildout :ref:`collective.recipe.plonesite <collective_recipe_plonesite>` 
que le permite automatizar la creación del sitio Plone ejecutando el perfiles de instalación 
que aplica las personalizaciones creadas e instala las dependencias descritas en el. 

Este procedimiento ofrece aprovechar las :ref:`ventajas de Buildout <buildout_caracteristicas>` 
para automatizar los procesos :ref:`Durante la creación del sitio <producto_policy_creacion_sitio>`, 
:ref:`Posterior la creación del sitio <producto_policy_post_creacion>` y :ref:`Ejecutar perfil de instalación <producto_policy_ejecutar_perfil>`, ya que el mismo es muy útil para entornos de pruebas o 
configuraciones de despliegue en ambientes de producción.

Para esto usted tiene que agregar una nueva sección en la declarativa ``parts`` del archivo 
:file:`buildout.cfg` como se muestra a continuación:

.. code-block:: cfg

  [buildout]
  parts =
      ...
      plonesite
       
  # For options see http://pypi.python.org/pypi/collective.recipe.plonesite
  [plonesite]
  recipe = collective.recipe.plonesite
  site-id = Plone
  instance = instance
  profiles =
      cliente1.policy:default

Luego ejecute el script :command:`buildout`, de la siguiente forma:

.. code-block:: sh

  $ ./bin/buildout -vN

Con este comando busca el paquete o sus dependencias en el repositorio :term:`PyPI`, 
descarga e instala el producto en su instancia Zope para sus sitios Plone allí hospedados.

Entonces inicie la :term:`Instancia de Zope`, de la siguiente forma:

.. code-block:: sh

  $ ./bin/instance fg 

De esta forma ya tiene disponible el sitio creado con el nombre ``Plone`` con su 
:term:`Producto Plone` de configuraciones aplicado en su :term:`Instancia de Zope` 
configurada de forma :ref:`standalone (autónoma) <ser-zeo-o-no-ser-zeo>`.

.. tip:: Para configuraciones en :ref:`ZEO <ser-zeo-o-no-ser-zeo>` consulte las opciones de 
    la `receta`_.

Comando locales del policy
==========================

.. todo::
    Escribir sobre este punto

Resumen
=======

En este artículo has aprendido a:

- Entender el :ref:`funcionamiento <producto_policy_intro>` del producto.

- ¿:ref:`Cómo generar <producto_policy_generar>` el producto?.

- ¿Cómo :ref:`instalar <producto_policy_instalar>` y :ref:`habilitar <producto_policy_habilitar>` 
  el producto creado en un sitio Plone.

.. todo::
    Terminar de actualizar este resumen!

----

Descarga código fuente
======================

Usted puede descargar el código fuente de este ejemplo, para esto ejecute el siguiente comando:

.. code-block:: sh

  $ git clone https://github.com/plone-ve/cliente1.policy.git cliente1.policy

Referencia
==========

- `Pasos para crear un producto de configuración`_ desde la comunidad Plone México.

.. _Pasos para crear un producto de configuración: http://www.plone.mx/docs/policy.html
.. _Crear un sitio Plone: http://localhost:8080/@@plone-addsite?site_id=Plone
.. _receta: https://pypi.python.org/pypi/collective.recipe.plonesite#options