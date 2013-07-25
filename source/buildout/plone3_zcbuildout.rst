.. -*- coding: utf-8 -*-

.. _buildout_plone3:

==================
Buildout y Plone 3
==================

:Autor(es): Leonardo J. Caballero G.
:Correo(s): leonardocaballero@gmail.com
:Lanzamiento: |version|
:Fecha: |today|

Descripción general
===================

Una herramienta para administrar, a través de un archivo de configuración
declaratoria, las partes y componentes de un desarrollo con Python. Dichas
partes no están limitadas a componentes o código Python.

La parte más poderosa de buildout es que puede extenderse con el uso de
"recetas" que pueden instalar componentes más complicados simplemente
agregando nuevas secciones a la configuración. Buildout puede instalar
diversos paquetes de Python fácilmente porque está conectado con el índice
de paquetes de Python (http://www.python.org/pypi).

Algunos términos importantes
============================

Hay que entender varios conceptos antes de continuar tales como :term:`Paquete Python`, 
:term:`paquetes Egg`, :term:`Cheese shop`, :term:`Producto Zope`, :term:`Instalación de Zope`,  
:term:`Instancia de Zope` y :ref:`easy_install <que_es_easyinstall>`.

.. _buildout_plone3_requisitos:

Requisitos previos
------------------

Existen instrucciones detalladas para la instalación de requisitos, pero en
general se necesita lo siguiente:

* Python 2.4.x.
* Instalar :ref:`entornos virtuales de Python <creacion_entornos_virtuales>` para aislar a su instalación de la del sistema.
* El Python :ref:`paquete Setuptools <que_es_setuptools>` (:ref:`easy_install <que_es_easyinstall>`).
* Para instalar instancias Zope / sitios Plone, es necesario el paquete :term:`Egg` de :ref:`ZopeSkel <instalacion_zopeskel>`.
* Para Plone, Python Imaging Library (PIL) instalado en ese Python.

Instalando entornos virtuales de Python
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Para esto consulte los diversos :ref:`modos de instalación <instalacion_virtualenv>` 
de entornos virtuales de Python.

Instalando Setuptools
~~~~~~~~~~~~~~~~~~~~~

Para esto consulte los diversos :ref:`modos de instalación <instalacion_easyinstall>` 
de setuptools y easy_install.


Instalando ZopeSkel
~~~~~~~~~~~~~~~~~~~

Para esto consulte los diversos :ref:`modos de instalación <instalacion_zopeskel>` 
de ZopeSkel.

Instalando dependencias en distribuciones basadas en Debian GNU/Linux
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Para para distribuciones basadas en Debian GNU/Linux, debe instalar los
requisitos previos con el siguiente comando:

.. code-block:: sh

  # aptitude install python2.4-dev python2.4-imaging python-profiler python2.4-setuptools libc6-dev

Creación de un buildout
=======================

Se puede generar un buildout utilizando un template de :ref:`paster <que_es_pastescript>`:

.. code-block:: sh

  $ paster create -t plone3_buildout buildout.plone3

El template hace varias preguntas:

.. code-block:: sh

  Selected and implied templates:
    ZopeSkel#plone3_buildout  A buildout for Plone 3 projects

    Variables:
      egg:      buildout.plone3
      package:  buildout.plone3
      project:  buildout.plone3

    Enter zope2_install (Path to Zope 2 installation; leave blank to fetch one) ['']:
    <si ya se tiene una instalación de Zope se puede usar poniendo aquí el path>
    Enter plone_products_install (Path to directory containing Plone products; leave blank to fetch one) ['']:
    <lo mismo aquí si ya se tienen los productos de Plone>
    Enter zope_user (Zope root admin user) ['admin']:
    <el usuario administrador del sitio>
    Enter zope_password (Zope root admin password) ['']:
    <el password para este usuario>
    Enter http_port (HTTP port) [8080]:
    <el puerto donde escuchará el servicio de Zope>
    Enter debug_mode (Should debug mode be "on" or "off"?) ['off']:
    <'on' para activar el modo de debug>
    Enter verbose_security (Should verbose security be "on" or "off"?) ['off']:
    <'on' para presentar detalles cuando ocurran errores de privilegios>
    ...
    ...
    ...
    -----------------------------------------------------------
    Generation finished
    You probably want to run python bootstrap.py and then edit
    buildout.cfg before running bin/buildout -v

    See README.txt for details
    -----------------------------------------------------------

Activación de un buildout
=========================

Para activar un buildout hay que ejecutar el script `bootstrap.py` con el
mismo python con que se desea trabajar:

.. code-block:: sh

  $ cd buildout.plone3
  $ python2.4 bootstrap.py
  ...
  ...
  ...
  $ bin/buildout -v
  ...
  ...
  ...
  $ bin/instance fg

Directorios creados
-------------------

.. glossary::
    :sorted:

    bin/
        Ejecutables de buildout y producidos por las partes.

    bin/buildout
        Script de zc.buildout.

    bin/instance
        Script de arranque de la instancia Zope.

    bin/repozo
        Script de ``repozo``, es una herramienta que puede ser 
        usado para crear un respaldo completo de la ZODB.

    bin/zopepy
        Script para hacer inmersiones interactivas de Python en 
        el contexto de la instalación Zope / Plone.

    eggs/
        Los eggs obtenidos e instalados de PyPI.

    downloads/
        Software adicional descargado.

    src/
        Código fuente de nuestros desarrollos.

    products/
        Productos tradicionales de zope.

    parts/
        Todo el código, configuración y datos manejados por buildout.

    var/
        Logs y archivo de ZODB de Zope (buildout nunca sobre escribe estos archivos).

    var/filestorage
        Contiene archivos de ZODB de Zope tales como ``Data.fs``, ``Data.fs.index``, 
        ``Data.fs.lock`` y ``Data.fs.tmp`` de su sitio web Plone.

    var/log
        Contiene archivos de Logs de Zope tales como ``instance.log`` (archivo de errores) 
        y ``instance-Z2.log`` (archivo de acceso).

Descripción de este ejemplo
---------------------------

Un ejemplo de un buildout funcional se muestra a continuación:

.. code-block:: cfg

    # definición de las partes que va a tener el buildout, cada parte es una
    # sección de configuración y generalmente utiliza una receta específica
    [buildout]
    
    newest = false
    
    parts =
        zope2
        productdistros
        instance
        zopepy
    
    extends = http://dist.plone.org/release/3.3.6/versions.cfg
    
    # ligas adicionales a pypi.python.org donde pueden encontrarse eggs
    find-links =
        http://dist.plone.org/release/3.3.6
        http://dist.plone.org/thirdparty/
        
    versions = versions
    
    # Agregar eggs adicionales aquí elementtree es requerido por Plone
    eggs =
        elementtree
        PIL
    
    # Por cada paquete en desarrollo (dentro de src) se debe agregar una línea
    # e.g.: develop = src/my.package
    develop =
    #    src/my.package
    
    # Esta receta instala zope 2. Para usar la misma url que requiere plone se
    # utiliza ${versions:zope2-url}. Es posible referirse con esta sintaxis a
    # cualquier variable de una de las partes, así: ${parte:variable}
    [zope2]
    recipe = plone.recipe.zope2install
    url = ${versions:zope2-url}
    
    # Ligas a distribuciones de productos tradicionales de Zope.
    # En nested-packages se pone el nombre del archivo (sin path) cuando
    # una distribución incluye varios productos.
    [productdistros]
    recipe = plone.recipe.distros
    urls = 
    nested-packages =
    version-suffix-packages = 
    
    # esta receta inicializa la instancia de zope y utiliza los datos de las
    # respuestas que se dieron al crear el buildout
    [instance]
    recipe = plone.recipe.zope2instance
    zope2-location = ${zope2:location}
    user = admin:admin
    http-address = 8080
    debug-mode = on
    verbose-security = on
    
    # Aquí se deben listar todos los eggs que zope debe poder ver
    # incluyendo los de desarrollo que se definen arriba
    # e.g. eggs = ${buildout:eggs} my.package
    eggs =
        Plone
        ${buildout:eggs}
    #    my.package
    
    # Activar la inicialización de zcml de los paquetes que lo requieran
    # e.g. zcml = my.package my.other.package
    zcml = 
    #    my.package
    
    # Directorios donde zope buscará productos
    products =
        ${buildout:directory}/products
        ${productdistros:location}
    
    # Interpreté de python generado con todos los paquetes activados en 
    # el path
    [zopepy]
    recipe = zc.recipe.egg
    eggs = ${instance:eggs}
    interpreter = zopepy
    extra-paths = ${zope2:location}/lib/python
    scripts = zopepy
    
    [versions]
    zope.testing = 3.8.7

En los comentarios en el código se explican las secciones del buildout.


Descarga código fuente
======================

Para descargar el código fuente de este ejemplo ejecute el siguiente comando:

.. code-block:: sh

  $ git clone https://github.com/plone-ve/buildout.plone3.git


Artículos relacionados
======================

.. seealso::

    Artículos sobre :ref:`replicación de proyectos Python <python_buildout>`.

    .. raw:: html

        <p>Vídeo tutorial llamado <b>Using buildout to install Zope and Plone</b> en Ingles</p>
        
        <div style="margin-top:10px;" align="center">
          <iframe width="560" height="315" src="http://www.youtube.com/embed/zZBE0uu5pGg" frameborder="0" allowfullscreen></iframe>
        </div>
        
        <p>creado por WebLion at Penn State, activistas de <a href="http://ploneedu.org" target="_target" title="PloneEdu"><b>PloneEdu.org</a></b></p>


Referencias
===========

-   `¿Qué es buildout?`_ desde la comunidad Plone México.
-   `Replicación de proyectos Python`_ desde la comunidad Plone Venezuela.

.. _¿Qué es buildout?: http://www.plone.mx/docs/buildout.html
.. _Replicación de proyectos Python: http://coactivate.org/projects/ploneve/replicacion-de-proyectos-python
