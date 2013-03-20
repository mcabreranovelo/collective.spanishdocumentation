.. -*- coding: utf-8 -*-

.. _easyinstall_setuptools:

========================
Setuptools y EasyInstall
========================

:Autor(es): Carlos de la Guardia, Leonardo J. Caballero G.
:Correo(s): carlos.delaguardia@gmail.com, leonardocaballero@gmail.com
:Lanzamiento: Python 4 o versiones superiores
:Fecha: 20 de Marzo de 2013

Este articulo explica como instalar paquetes Python con ``setuptools`` y ``EasyInstall``.

.. _que_es_setuptools:

¿Qué es Setuptools?
===================

`Setuptools`_, es una colección de mejoras para el módulo distutils de Python,
que permiten a un desarrollador construir y distribuir :term:`Paquetes Python` 
de forma sencilla, en especial cuando dependen de otros :term:`Paquetes Python` 
para funcionar. 

Entre sus características principales están:

* Por defecto, utiliza :term:`PyPI` para buscar los paquetes, lo que permite acceso
  inmediato e instalación transparente de miles de paquetes.

* Permite crear :term:`paquetes Egg` Python, que son :term:`Paquetes Python` 
  empaquetados en un sólo archivo para su distribución.

* Incluye archivos de configuración y todos los archivos que forman parte del
  directorio de trabajo, sin necesidad de listarlos individualmente o crear
  archivos de manifiesto.

.. _que_es_easyinstall:

¿Qué es EasyInstall?
====================

`easy_install`_, es una herramienta que se basa en `Setuptools` para automáticamente 
encontrar y descargar desde Internet las dependencias, para instalarlas o actualizarlas 
al momento de construir, que además esta herramienta es capaz de bajar de Internet las 
dependencias utilizando HTTP, FTP, sistema de control de versiones como *Subversion*, 
*Git*, *Mercurial*, entre otros o desde forjas como *SourceForge.net*, *Launchpad.net*, 
*Github.com*, *Bitbucket.org*, etc.

.. _instalacion_easyinstall:

Instrucciones de Instalación
============================

Siempre existen más de dos formas de instalar :term:`Paquetes Python` con **setuptools** y
**easy_install** ;)

Instalación manual
------------------

Para ambas es recomendable que instale ciertas dependencias en su sistema
operativo como las que se muestran a continuación: 

.. code-block:: sh

  # aptitude install build-essential python-dev

La instalación es muy sencilla, solo se necesita bajar de Internet el
archivo `ez_setup.py`_ y ejecutarlo con el Python que se desea utilizar, 
con los siguientes comandos: 

.. code-block:: sh

  # wget http://peak.telecommunity.com/dist/ez_setup.py
  # python ez_setup.py

Esto instalará un programa llamado ``easy_install`` junto a los demás 
ejecutables de Python.


Instalación en sistemas Debian
------------------------------

La instalación en sistemas Debian es recomendable que instale ciertas dependencias 
en su sistema operativo como las que se muestran a continuación: 

.. code-block:: sh

  # aptitude install build-essential python-dev python-setuptools

Esto instalará un programa llamado ``easy_install`` junto a los demás 
ejecutables de Python.

.. _uso_easyinstall:

Ejemplos de uso
===============

El programa ``easy_install`` ofrece varias formas de uso, para instalar los paquetes
de diversas fuentes, como se describe a continuación con los siguientes ejemplos:

.. tip::
    
    Para poder utilizar el ``easy_install``, primero debe instalar ``setuptools``. 
    Si utiliza :ref:`virtualenv <que_es_virtualenv>`, una copia del ``easy_install`` 
    será automáticamente instalados en cada entorno virtual que usted crea. 
    
    ``easy_install`` se puede complementar con ``virtualenv``, y se recomienda que lo 
    utilice para :ref:`aislar a la instalación <creacion_entornos_virtuales>` de los 
    :term:`paquetes Egg`.

**Ejemplo 1.** Instalar un paquete por nombre, buscando en :term:`PyPI` la versión más
reciente: 

.. code-block:: sh

    $ easy_install SQLObject

**Ejemplo 2.** Instalar o actualizar un paquete por nombre y versión utilizando una 
dirección URL donde encontradas en una "página de descargas": 

.. code-block:: sh

    $ easy_install -f http://dist.plone.org/packages/ 'Pillow==1.7.3'

**Ejemplo 3.** Instalar o actualizar un paquete desde su propio :ref:`replica del repositorio PyPI <creando_propio_repositorio_pypi>` o su repositorio de :term:`paquetes Egg` privado: 

.. code-block:: sh

    $ easy_install -i http://pypi.ejemplo.com/simple SQLObject

**Ejemplo 4.** Descargar e instalar una distribución de código fuente: 

.. code-block:: sh

    $ easy_install http://ejemplo.com/ruta/a/MiPaquete-1.2.3.tgz

**Ejemplo 5.** Instalar un :term:`paquete Egg` ya descargado: 

.. code-block:: sh

    $ easy_install ./Descargas/OtroPaquete-3.2.1-py2.7.egg

**Ejemplo 6.** Instalar un paquete con una versión especifica: 

.. code-block:: sh

    $ easy_install "ZopeSkel==2.21.2"

**Ejemplo 7.** Actualizar un paquete ya instalado con la versión más reciente de :term:`PyPI`: 

.. code-block:: sh

    $ easy_install --upgrade PyProtocols


Para más información consulte la ayuda disponible por que paquete ``easy_install``
ejecutando el siguiente comando: 

.. code-block:: sh

    $ easy_install --help



.. _easy_install_zope_plone:

Utilización con Zope/Plone
==========================

El mecanismo más moderno para la instalación de distribuciones de Zope y
Plone, llamado :ref:`buildout <que_es_zcbuildout>`, formalmente 
:ref:`zc.buildout <que_es_zcbuildout>`, hace uso de ``easy_install`` para 
obtener e instalar todas las dependencias. 

Adicionalmente, existe una herramienta llamada ZopeSkel que permite crear 
fácilmente "esqueletos" de distintos tipos de proyectos de Zope y Plone, 
mediante una herramienta llamada ``paster`` y un sistema de plantillas. 
Es recomendado instalar esta última herramienta para proyectos nuevos, de 
la siguiente manera:

.. code-block:: sh

    $ easy_install "ZopeSkel==2.21.2"

Una vez instalado, ofrece una buena variedad de esqueletos para diversos 
tipos de proyectos, como temas visuales, componentes de Plone, buildouts, 
tipos de contenido con Archetypes o entre otros mas. 

Se utiliza mediante el comando de sistema ``paster``, pasando la opción 
``create`` para crear un proyecto y la opción ``--list-templates`` ver 
las diversas plantillas de proyectos disponibles para crear, como se 
muestra a continuación:

.. code-block:: sh

    $ paster create --list-templates
    Available templates:
      archetype:          A Plone project that uses Archetypes
      basic_namespace:    A project with a namespace package
      basic_package:      A basic setuptools-enabled package
      basic_zope:         A Zope project
      kss_plugin:         A KSS plugin template
      nested_namespace:   A project with two nested namespaces.
      paste_deploy:       A web application deployed through paste.deploy
      plone:              A Plone project
      plone2.5_buildout:  A buildout for Plone 2.5 projects
      plone2.5_theme:     A Theme for Plone 2.5
      plone2_theme:       A Theme Product for Plone 2.1 & Plone 2.5
      plone3_buildout:    A buildout for Plone 3 projects
      plone3_portlet:     A Plone 3 portlet
      plone3_theme:       A Theme for Plone 3.0
      plone_app:          A Plone App project
      plone_hosting:      Plone hosting: buildout with ZEO and any Plone version
      plone_pas:          A Plone PAS project
      recipe:             A recipe project for zc.buildout
      silva_buildout:     A buildout for Silva projects
      zope_app:           Package that contains a Zope application
      zope_deploy:        (Paste) deployment of a Zope application

Para mas información de las opciones disponibles de ``ZopeSkel``, ejecute el siguiente comando:

.. code-block:: sh

    $ paster --help
      Usage: paster [paster_options] COMMAND [command_options]
      
      Options:
        --version         show program's version number and exit
        --plugin=PLUGINS  Add a plugin to the list of commands (plugins are Egg
                          specs; will also require() the Egg)
        -h, --help        Show this help message
      
      Commands:
        create       Create the file layout for a Python distribution
        help         Display help
        make-config  Install a package and create a fresh config file/directory
        points       Show information about entry points
        post         Run a request for the described application
        request      Run a request for the described application
        serve        Serve the described application
        setup-app    Setup an application, given a config file

Referencia
==========

- `Instalación de setuptools y EasyInstall para Python`_ desde la comunidad Plone México.

.. _Setuptools: http://pypi.python.org/pypi/setuptools/
.. _ez_setup.py: http://peak.telecommunity.com/dist/ez_setup.py
.. _easy_install: http://peak.telecommunity.com/DevCenter/EasyInstall
.. _Instalación de setuptools y EasyInstall para Python: http://plone.org/countries/mx/instalacion-de-setuptools-y-easyinstall-para-python
