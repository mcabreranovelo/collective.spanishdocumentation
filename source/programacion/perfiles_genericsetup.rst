
.. -*- coding: utf-8 -*-

.. _perfiles_genericsetup:

==============================================================
Framework de instalación y exportación de Add-on: GenericSetup
==============================================================

.. sidebar:: Sobre este artículo

    :Autor(es): Carlos de la Guardia, Leonardo J. Caballero G.
    :Correo(s): carlos.delaguardia@gmail.com, leonardocaballero@gmail.com
    :Compatible con: Plone 3, Plone 4
    :Fecha: 29 de Septiembre de 2014

.. _genericsetup_intro:

Introducción
============

El `GenericSetup`_, es un mecanismo basado en XML para importar y exportar
configuraciones de sitios Plone.

Se utiliza principalmente para modificar la configuración de un sitio
al momento de instalar un producto. Entre otras cosas permite:

* Registrar los archivos **CSS** en el :ref:`portal_css <zmi_portal_css>`.

* Registrar los archivos **Javascript** en el :ref:`portal_javascript <zmi_portal_javascripts>`.

* Modificar los valores de diversas **propiedades** del sitio en el ``portal_properties``.

* Registrar de asignación de **portlets**.

* Registrar índices de búsqueda del :ref:`portal_catalog <zmi_portal_catalog>`.

* Y mas...

Perfiles de instalación
=======================

Usualmente los archivos de configuración para ``GenericSetup`` se guardan
bajo la carpeta :file:`profiles/default` dentro del producto.

Toda la configuración que puede realizarse a través del panel de control
de Plone y del :ref:`ZMI <que_es_zmi>`, como por ejemplo el orden de los
viewlets elegido en ``/@@manage-viewlets``, puede guardarse y ser reutilizada
mediante un perfil de ``GenericSetup``.

No es necesario editar manualmente los archivos XML del perfil de
``GenericSetup``, pues siempre es posible modificar la configuración
de Plone desde el sitio y después exportarla completa o en partes a XML.
La herramienta :ref:`portal_setup <zmi_portal_setup>` en el :ref:`ZMI <que_es_zmi>`
permite exportar, importar y generar copias de las configuraciones.

Modificar los archivos de configuración en XML de un producto no ocasiona
cambios inmediatos en el sitio de Plone, aun reiniciando el servidor. La
configuración `real` del portal se almacena en la ZODB, por lo que es
necesario reimportar los perfiles desde :ref:`portal_setup <zmi_portal_setup>`
o reinstalar el producto en cuestión desde el panel de control de Plone.
Solo en ese momento sera modificada la configuración.

.. note::

    Diferencias entre :term:`ZCML` y `GenericSetup`_

    Cambios realizados mediante configuración de :term:`ZCML` afectan el código
    Python de todos los sitios presentes en una instancia de ``Zope``, mientras
    que los cambios en perfiles de ``GenericSetup`` solo afectan el sitio de
    Plone en que se hacen. Al importar un perfil de `GenericSetup`_, se
    realizan cambios directamente en la base de datos del sitio, mientras que
    al cargar archivos de configuración de :term:`ZCML` solo se modifica el código
    cargado en memoria.

* `GenericSetup tutorial <http://plone.org/documentation/tutorial/genericsetup>`_

* `GenericSetup product page <http://pypi.python.org/pypi/Products.GenericSetup/1.4.5>`_.

* `Source code <http://svn.zope.org/Products.GenericSetup/trunk/Products/GenericSetup/README.txt?rev=87436&view=auto>`_.

Términos importantes
====================

.. glossary::

    perfil base
        Del Ingles ``base profile``, es el perfil que todos los otros perfiles extenderá.
        Para usuarios de Plone este es el perfil ``plone`` desde el producto ``CMFPlone``.

    perfil de extensión
        Del Ingles ``extension profile``, es un conjunto de información de configuración
        que extiende el :term:`perfil base`. Las mayoría de los productos define al
        menos un :term:`perfil de extensión` para definir sus producto.

    perfil de versión
        El perfil de versión puede definirse en el archivo :file:`metadata.xml`.
        Este le dice al programa ``GenericSetup`` cual es la versión actual del perfil.

    pasos de importar
        Ver :term:`pasos de importación`.

    pasos de importación
        Del Ingles ``import steps``, son los pasos de importar que le dice al programa
        ``GenericSetup`` como leer la configuración exportada para un perfil dado y aplicarlo
        en su sitio.

    pasos de exportar
        Del Ingles ``export steps``, son los pasos de exportar que le dice al programa
        ``GenericSetup`` como exportar la actual configuración de su sitio.

    manipulador de instalación
        Del Ingles ``setup handler``, un manipulador de instalación es un termino
        dado a un paso de importar que ejecuta algún código de personalización Python
        se estila definir con el nombre :file:`setuphandler.py`. Este es otra forma de
        crear un paso de importar.

    pasos de actualizar
        Del Ingles ``upgrade step``, un paso de actualizar da a usted la habilidad
        para actualizar el código desde una versión del perfil a otro. Esto es útil
        para uno cambios de tiempo que necesitan ser hecho entre las versiones.
        Mas información viste `Upgrade steps`_.

    instantánea
        Del Ingles ``snapshot``, es un perfil que captura el estado de la configuración
        del sitio en un punto en el tiempo (por ejemplo, inmediatamente después de la
        creación del sitio, o después de la importación de un :term:`perfil de extensión`.

        El caso de uso del ``snapshot``, es tomar la configuración actual en el
        :ref:`portal_setup <zmi_portal_setup>`. Este puede después ser usada para comparar
        a otro ``snapshot`` o perfil. Esto puede ser útil cuando usted hace cambios a su
        sitio y quiere saber como afecta a su perfil.

.. _gs_referencia_perfiles:

Referenciando a Perfiles
========================

``GenericSetup`` referencia a los perfiles con el siguiente formato:

.. code-block:: text

  profile-<package name>:<profile name>

Un ejemplo podría ser el perfil desde el producto CMFPlone:

.. code-block:: text

  profile-Products.CMFPlone:plone

Esta es la sintaxis que es usada para dependencias en el archivo :file:`metadata.xml`. 
Por ejemplo, si usted siempre quiere ejecutar por defecto la dependencia 'my.dependency' 
antes de su perfil, usted podría usar:

.. code-block:: xml

  <?xml version="1.0"?>
  <metadata>
     <version>VERSION_NUMBER</version>
     <dependencies>
        <dependency>profile-my.dependency:default</dependency>
     </dependencies>
  </metadata>

.. _gs_creando_perfiles:

Creación de un perfil
=====================

Un perfil se declara utilizando la directriz ``<genericsetup>`` en el archivo
:file:`configure.zcml` del producto. El instalador de Plone importara la
configuración almacenada en el perfil llamado ``default``, pero es posible
declarar otros perfiles con diferentes nombres e importarlos por separado, por
ejemplo para ejecutar pruebas.

Los archivos XML del perfil se colocan en el directorio :file:`profiles/default`
dentro del producto.

.. code-block:: xml

	<configure
	    xmlns="http://namespaces.zope.org/zope"
	    xmlns:genericsetup="http://namespaces.zope.org/genericsetup"
	    i18n_domain="gomobile.mobile">

	    <genericsetup:registerProfile
	      name="default"
	      title="Plone Go Mobile"
	      directory="profiles/default"
	      description='Mobile CMS add-on'
	      provides="Products.GenericSetup.interfaces.EXTENSION"
	      />

	</configure>

También es posible registrar un ``Import various step`` que ejecute código
Python cada vez que se instale el perfil de un producto.

Mas información sobre ejecutar ``steps``:

* http://plone.293351.n2.nabble.com/indexing-of-content-created-by-Generic-Setup-td4454703.html

.. _gs_structure:

Generación de Contenido manualmente
===================================

El programa ``GenericSetup`` le permite a usted importar y exportar contenido 
por la forma llamada ``structure``. Allí puede haber muchos archivos que controlan 
como este trabaja:

.. glossary::

  .objects
    El archivo :file:`.objects` contiene una lista de objeto IDs 
    y su ``portal_types`` que la estructura necesita crear 
    los objetos. Los IDs también listan dentro de la estructura de 
    carpeta con más información acerca de cual crear. Por defecto 
    todos los elementos listados serán removido y se agregaran 
    de nuevo.

    Ejemplo de un archivo :file:`.objects` que toma desde el perfil
    ``Products.CMFPlone:plone``:

      .. code-block:: ini

        Members,Large Plone Folder
        front-page,Document

  .preserve
    El archivo :file:`.preserve` es una lista de IDs que, si están 
    presente, no debería ser removido. Este podría ser usado 
    si usted conoce el perfil que puede ser ejecutado otra ves 
    y posiblemente remover su contenido.

    El archivo :file:`.preserve` típicamente contiene información que
    ``GenericSetup`` usará para cuidar dos objetos existentes:

      .. code-block:: ini

        front-page
        Members

  .delete
    El archivo :file:`.delete` es una lista de IDs que puede ser 
    borrado desde el sitio.

    Al igual que el archivo :file:`.preserve`, el archivo :file:`.delete`
    usan la misma sintaxis. El siguiente podría ser valido para borrar
    dos objetos:

      .. code-block:: ini

        front-page
        Members

  .properties
    El archivo :file:`.properties` típicamente contiene información que
    ``GenericSetup`` utilizará para crear la carpeta en la que reside.
    Esto le permite la exportación a estar representados en una jerarquía
    como lo es en el sitio.

    Ejemplo de un archivo :file:`.properties` tomada desde el perfil de
    ``Products.CMFPlone:plone`` para la carpeta :file:`Members`:

      .. code-block:: ini

        [DEFAULT]
        description = Site Users
        title = Users

.. _gs_listado_perfiles:

Obtener el listado de perfiles disponibles
==========================================

Ejemplo:

.. code-block:: python

  setup_tool = self.portal.portal_setup

  profiles = setup_tool.listProfileInfo()
  for profile in profiles:
      print  str(profile)

Resultados:

.. code-block:: python

  {'product': 'PluggableAuthService', 'description': 'Content for an empty PAS (plugins registry only).', 'for': <InterfaceClass Products.PluggableAuthService.interfaces.authservice.IPluggableAuthService>, 'title': 'Empty PAS Content Profile', 'version': 'PluggableAuthService-1.5.3', 'path': 'profiles/empty', 'type': 1, 'id': 'PluggableAuthService:empty'}
  {'product': 'Products.CMFDefault', 'description': u'Profile for a default CMFSite.', 'for': <InterfaceClass Products.CMFCore.interfaces._content.ISiteRoot>, 'title': u'CMFDefault Site', 'version': 'CMF-2.1.1', 'path': u'profiles/default', 'type': 1, 'id': u'Products.CMFDefault:default'}
  {'product': 'Products.CMFPlone', 'description': u'Profile for a default Plone.', 'for': <InterfaceClass Products.CMFPlone.interfaces.siteroot.IPloneSiteRoot>, 'title': u'Plone Site', 'version': u'3.1.7', 'path': u'/home/moo/sits/parts/plone/CMFPlone/profiles/default', 'type': 1, 'id': u'Products.CMFPlone:plone'}
  {'product': 'Products.Archetypes', 'description': u'Extension profile for default Archetypes setup.', 'for': None, 'title': u'Archetypes', 'version': u'1.5.7', 'path': u'/home/moo/sits/parts/plone/Archetypes/profiles/default', 'type': 2, 'id': u'Products.Archetypes:Archetypes'}
    ...

.. _gs_instalar_perfil_python:

Instalación un perfil desde Python
==================================

Para instalar un perfil desde Python, por ejemplo para pruebas, se puede
llamar por su nombre, en el formato ``profile-${product_name}:${profile_id}``

Ejemplo:

.. code-block:: python

  setup_tool.runAllImportStepsFromProfile('profile-miproducto.miperfil')

.. _gs_instalar_dependencias:

Dependencias
============

GenericSetup permite declarar como dependencias los perfiles de otros
productos, de manera que estos sean instalados antes del perfil de nuestro
producto.

* `Mas información sobre dependencias <http://plone.org/products/plone/roadmap/195/>`_.

Otros Consejos
==============

* Cuando instale un producto de tercero, siempre debe asegurarse de tener un respaldo 
  de su sitio.

* Pruebe la instalación del producto en un entorno local antes de aplicarlo en el entorno 
  de producción.

* Cuando escriba un manipulador de instalación de un perfil especifico como 
  :ref:`setupVarious <producto_policy_setupvarious>`, asegúrese que ellos solamente ejecute 
  el perfil usando el método ``context.readDataFile``.

.. seealso:: 
  
    - `Add-on installation and export framework - GenericSetup`_.

    - `Generic Setup Quick Reference`_.

Referencias
===========

- `Products.GenericSetup documentation`_.

- `Add-on installation and export framework - GenericSetup`_.

- `GenericSetup y Perfiles`_ desde la comunidad Plone México.

- `Generic Setup Quick Reference`_.

.. _Products.GenericSetup documentation: https://pythonhosted.org/Products.GenericSetup/index.html
.. _GenericSetup: http://docs.plone.org/develop/addons/components/genericsetup.html
.. _Upgrade steps: http://docs.plone.org/develop/addons/components/genericsetup.html#upgrade-steps
.. _Add-on installation and export framework - GenericSetup: http://docs.plone.org/develop/addons/components/genericsetup.html
.. _GenericSetup y Perfiles: http://www.plone.mx/docs/gs.html
.. _Generic Setup Quick Reference: http://www.sixfeetup.com/company/technologies/plone-content-management/swag/swag-images-files/generic_setup.pdf
