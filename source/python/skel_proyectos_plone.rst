.. -*- coding: utf-8 -*-

.. _skel_plone:

==================================
Esqueletos de proyectos Zope/Plone
==================================

.. sidebar:: Sobre este artículo

    :Autor(es): Leonardo J. Caballero G.
    :Correo(s): leonardoc@plone.org
    :Compatible con: Plone 3 y Plone 4
    :Fecha: 21 de Marzo de 2015

Introducción
============

Son una serie de colecciones de :ref:`plantillas esqueletos <scaffolding_python>` que
permiten iniciar rápidamente proyectos, existente diversos *esqueletos* orientados a
tipos de desarrollos específicos, a continuación se muestran algunos esqueletos útiles:

- **Esqueletos de proyectos Plone**:

  .. note::
      :ref:`Plone <que_es_plone>`, Además de ser un sistema de gestión de contenidos,
      es como un Framework para desarrollo de aplicaciones, mas NO es de propósito
      general.

  - `ZopeSkel`_, es una colección de esqueletos para crear automáticamente paquetes e
    instancias en Zope.

  - `zopeskel.dexterity`_, es una plantilla Paster para la herramienta de desarrollo de
    tipos de contenidos Dexterity para Plone.

- **Esqueletos de proyectos Zope**:

  .. note::
      :ref:`Zope <que_es_zope>`,  es un entorno de desarrollo para la creación de sitios
      web dinámicos y/o aplicaciones web escrito en el lenguaje de programación
      :ref:`Python <python_index>`.

  - `zopeproject`_, Herramientas y scripts para la creación de entornos de pruebas de
    desarrollo para aplicaciones Web que usen principalmente Zope.


- **Esqueletos de proyectos Grok**:

  .. note::
      :ref:`Grok <grok>`, es un Framework para desarrollo de aplicaciones en Zope 3.

  - `grokcore.startup`_,  Soporte a Paster para proyectos Grok.
  
  - `grokproject`_, Script que instala un directorio de proyecto instalando ``Zope 3``
    con el framework ``grok``, además creando un plantilla para una aplicación ``grok``.
  
.. _instalacion_zopeskel:

Instalación
===========

Para realizar este paso debe tener creado previamente y activado un entorno virtual creado,
ejecutando el siguiente comando:

.. code-block:: sh

  (python) pip install 'ZopeSkel==2.21.2'

.. note::

  No olvidar que estos paquetes han sido instalados con el :ref:`entorno virtual <por_que_virtualenv>`
  que previamente usted activo, eso quiere decir que los paquetes previamente instalados con
  :ref:`Easy Install <que_es_easyinstall>` o :ref:`PIP <que_es_pip>` están instalados en el
  directorio :file:`~/virtualenv/python/lib/python2.x/site-packages/` en ves del directorio
  de su versión de Python del sistema :file:`/usr/lib/python2.x/site-packages/`.

Uso de ZopeSkel
===============

Al finalizar la instalación podrá opcionalmente consultar cuales plantillas tiene disponible
para usa, ejecutando el siguiente comando:

.. code-block:: sh

  (python)$ paster create --list-templates
    Available templates:
      archetype:          A Plone project that uses Archetypes content types
      basic_buildout:     A basic buildout skeleton
      basic_namespace:    A basic Python project with a namespace package
      basic_package:      A basic setuptools-enabled package
      basic_zope:         A Zope project
      kss_plugin:         A project for a KSS plugin
      nested_namespace:   A basic Python project with a nested namespace (2 dots in name)
      paste_deploy:       A web application deployed through paste.deploy
      plone:              A project for Plone add-ons
      plone2.5_buildout:  A buildout for Plone 2.5 projects
      plone2.5_theme:     A theme for Plone 2.5
      plone2_theme:       A theme for Plone 2.1
      plone3_buildout:    A buildout for Plone 3 installation
      plone3_portlet:     A Plone 3 portlet
      plone3_theme:       A theme for Plone 3
      plone4_buildout:    A buildout for Plone 4 developer installation
      plone_app:          A project for Plone add-ons with a nested namespace (2 dots in name)
      plone_basic:        A project for Plone products
      plone_hosting:      Plone hosting: buildout with ZEO and Plone versions below 3.2
      plone_pas:          A project for a Plone PAS plugin
      recipe:             A recipe project for zc.buildout
      silva_buildout:     A buildout for Silva projects


Creando un proyecto Buildout de Plone 4
---------------------------------------

Usted debe usar el comando :command:`paster` para crear el proyecto Buildout.

.. code-block:: sh

  (python)$ paster create -t plone4_buildout cliente1-portal.buildout
    Selected and implied templates:
      ZopeSkel#plone4_buildout  A buildout for Plone 4 developer installation

    Variables:
      egg:      cliente1-portal.buildout
      package:  cliente1-portal.buildout
      project:  cliente1-portal.buildout

    **************************************************************************
    **   *** NOTE: This template is for developers.
    
    **  If you just want to install Plone, the preferred way to get a
    **  buildout-based setup for Plone is to use the standard installer
    **  for your operating system (the Windows installer, the Mac
    **  installer, or the Unified Installer for Linux/Unix/BSD). These
    **  give you a best-practice, widely-used setup with an isolated
    **  Python and a well-documented buildout.
    **************************************************************************

    Plone Version (Plone version # to install) ['4.1']: 
    Creating template plone4_buildout
    Creating directory ./cliente1-portal.buildout
      Copying README.txt to ./cliente1-portal.buildout/README.txt
      Copying bootstrap.py to ./cliente1-portal.buildout/bootstrap.py
      Copying buildout.cfg_tmpl to ./cliente1-portal.buildout/buildout.cfg
      Recursing into src
        Creating ./cliente1-portal.buildout/src/
        Copying README.txt to ./cliente1-portal.buildout/src/README.txt
      Recursing into var
        Creating ./cliente1-portal.buildout/var/
        Copying README.txt to ./cliente1-portal.buildout/var/README.txt
    
    **************************************************************************
    **   Generation finished.
    
    **  Now run bootstrap and buildout:
    
    **  python bootstrap.by
    
    **  bin/buildout
    
    **  See ZopeSkel add-on page for more details:
    
    **  http://plone.org/products/zopeskel
    
    **************************************************************************

Usted puede verificar el paquete previamente creado y observará como este paquete básico
ha habilitado el setuptools.

.. code-block:: sh

    cliente1-portal.buildout
    |-- README.txt
    |-- bootstrap.py
    |-- buildout.cfg
    |-- src
    |   `-- README.txt
    `-- var
    `-- README.txt


Para iniciar el proyecto Plone ejecute los siguientes comandos:

.. code-block:: sh

  (python)$ cd cliente1-portal.buildout/
  (python)$ python bootstrap.py

Observe la estructura de directorio creada ejecutando el siguiente comando:

.. code-block:: sh

    cliente1-portal.buildout
    |-- README.txt
    |-- bin
    |   `-- buildout
    |-- bootstrap.py
    |-- buildout.cfg
    |-- develop-eggs
    |-- eggs
    |-- parts
    |   `-- buildout
    |-- src
    |   `-- README.txt
    `-- var
    `-- README.txt

Iniciar la construcción de proyecto Plone:

.. code-block:: sh

  (python)$ ./bin/buildout -vN


De esta forma se inicia la construcción de proyecto Plone 4.

Esqueletos y estilos de trabajo
===============================

Una de las características interesante de los esqueletos es que usted puede crear
sus propias plantillas de proyecto que apliquen sus propias estilos de desarrollo
y configuraciones en sus proyectos de desarrollo.

Esto es muy útil cuando requieres trabajar con un equipo de desarrolladores a los
cuales debes definir pautas sobre estilos de desarrollos, de sintaxis de código y
otras más, a continuación muestro una lista de diversos esqueletos hecho por
diversas compañías:

- `A collection of skeletons for quickstarting projects with Ingeniweb products`_.

- `ifPeople's Additional templates for paster`_.

- `Paster templates for standard NiteoWeb Plone projects`_.

- `Simples Consultoria's skeleton for a buildout`_.

- `Simples Consultoria's skeleton for a policy package`_.

- `Simples Consultoria's skeleton for a package`_.

- `Simples Consultoria's skeleton for a theme`_.

- `Quintagroup theme template for Plone 3 with nested namespace`_.

- `Project templates creating Web and Mobile themes for Plone`_.

- `Zopeskel template for plone.app.theming based theme development`_.


Recomendaciones
===============

Si desea trabajar con algún proyecto de desarrollo basado en esqueletos
(plantillas ``paster``) y Buildout simplemente seleccione cual esqueleto
va a utilizar para su desarrollo y proceso a instalarlo con 
:ref:`Easy Install <que_es_easyinstall>` o :ref:`PIP <que_es_pip>`
(como se explico anteriormente) y siga sus respectivas instrucciones para
lograr con éxito la tarea deseada.

.. seealso::
    Artículos sobre:

   - :ref:`Esqueletos de proyectos Python <skel_python>`.

Referencias
===========

- `Gestión de proyectos con Buildout, instalando Zope/Plone con este mecanismo`_ desde la comunidad Plone Venezuela.

.. _ZopeSkel: http://pypi.python.org/pypi/ZopeSkel
.. _zopeskel.dexterity: http://pypi.python.org/pypi/zopeskel.dexterity/
.. _zopeproject: http://pypi.python.org/pypi/zopeproject/
.. _grokcore.startup: http://pypi.python.org/pypi/grokcore.startup
.. _grokproject: http://pypi.python.org/pypi/grokproject/
.. _A collection of skeletons for quickstarting projects with Ingeniweb products: http://pypi.python.org/pypi/IngeniSkel/
.. _ifPeople's Additional templates for paster: http://pypi.python.org/pypi/ifpeople.pastertemplates/
.. _Paster templates for standard NiteoWeb Plone projects: http://pypi.python.org/pypi/zopeskel.niteoweb/
.. _Simples Consultoria's skeleton for a buildout: http://pypi.python.org/pypi/sc.paster.buildout/
.. _Simples Consultoria's skeleton for a policy package: http://pypi.python.org/pypi/sc.paster.policy/
.. _Simples Consultoria's skeleton for a package: http://pypi.python.org/pypi/sc.paster.package/
.. _Simples Consultoria's skeleton for a theme: http://pypi.python.org/pypi/sc.paster.theme/
.. _Quintagroup theme template for Plone 3 with nested namespace: http://pypi.python.org/pypi/quintagroup.themetemplate/
.. _Project templates creating Web and Mobile themes for Plone: http://pypi.python.org/pypi/gomobile.templates/
.. _Zopeskel template for plone.app.theming based theme development: https://github.com/hexagonit/hexagonit.themeskel
.. _Gestión de proyectos con Buildout, instalando Zope/Plone con este mecanismo: http://coactivate.org/projects/ploneve/gestion-de-proyectos-con-buildout
