.. -*- coding: utf-8 -*-

.. _recipe_buildout:

================
Recipes Buildout
================

.. sidebar:: Sobre este artículo

    :Autor(es): Leonardo J. Caballero G.
    :Correo(s): leonardoc@plone.org
    :Compatible con: Python 2.4 o versiones superiores
    :Fecha: 21 de Marzo de 2015

.. _que_es_recipes:

¿Qué son los Recipes?
=====================

Los ``recipes`` son los mecanismos de plugin proveídos por Buildout para agregar
nuevas funcionalidades para construir su software. 

Una parte del Buildout es creado por una receta, esta es la receta responsable de la 
instalación / desinstalación de su software

Cada parte se crea bajo el directorio :file:`parts/` para el uso específico de la 
parcial receta de la construcción. 

.. tip:: Este directorio no está destinado a la modificación por parte del programador.

Cada sección definida en la declarativa ``parts =`` utiliza una receta para supervisar 
su instalación / desinstalación, el nombre de una parte es arbitraria. En algunos casos 
una receta creará archivos usando el prefijo del nombre de la receta. El resto de las 
líneas ``nombre = valor`` debajo de una sección parcial son simples argumentos que se 
pasan a la receta en tiempo de compilación para parametrizar los valores por defecto a 
sus necesidades.

Las recetas son escritos en Python, estos son distribuidos como :term:`Egg`. Son de mucha 
utilidad para trabajar con :term:`paquetes Egg` en desarrollo ya que esta lo soportan.

.. _recipes_instalar:

¿Cómo instalarlos?
==================

Las recetas son siempre instalado como un :term:`paquetes Egg` de Python. Ellos 
pueden ser descargados desde un servidor de paquetes, como el Python Package Index 
(:term:`PyPI`), otro ellos pueden ser desarrollados como parte de un proyecto usando 
un :term:`paquete Egg` de desarrollo. este es un tipo especial de :term:`paquete Egg` 
que se instala como un vínculo de huevo que contiene el nombre de un directorio de 
origen.

Los :term:`paquetes Egg` de desarrollo no tienen que ser empaquetados para
distribución para ser usados y se puede modificar en en sitio, lo cual es
especialmente útil cuando se están desarrollando.

A continuación se describen una serie de recetas útiles para diversos casos de usos la 
construcción de Python / Zope / Plone:

Control de versiones
--------------------

.. _mrdeveloper:

`mr.developer`_, es una extensión de :ref:`zc.buildout <python_buildout>` 
la cual hace fácil trabajar con buildout que contiene muchos paquetes que
contienen gran cantidad de paquetes de los cuales sólo desea desarrollar
algunos, a continuación un ejemplo de configuración: 

.. code-block:: cfg

  [buildout]
  # For options see http://pypi.python.org/pypi/mr.developer
  extensions = mr.developer
  
  auto-checkout =
      my.package
      some.other.package
      
  eggs =
      my.package
      some.other.package
        
  [sources]
  my.package = svn http://example.com/svn/my.package/trunk update=true
  some.other.package = git git://example.com/git/some.other.package.git

.. _infraesubversion:

`infrae.subversion`_, es una receta buildout para instalar productos Zope 
y productos Plone que están disponibles en sistemas de control de versiones SVN, 
a continuación un ejemplo de configuración: 

.. code-block:: cfg

  [buildout]
  parts =
      svnproducts
        
  # Get TickingMachine directly from SVN since it's not eggified
  # For options see http://pypi.python.org/pypi/infrae.subversion
  [svnproducts]
  recipe = infrae.subversion
  urls =
      http://tickingmachine.googlecode.com/svn/trunk TickingMachine

  # In the case you're installing an old product (not eggified) you will also need 
  # to register it in products value at the [instance] section so that they get added 
  # to your Python path:
  products =
      ${buildout:directory}/products
      ${productdistros:location}
      ${plone:products}
      ${svnproducts:location}

.. _plone_recipe_bundlecheckout:

`plone.recipe.bundlecheckout`_, es una receta buildout para instalar productos Zope 
y productos Plone que están disponibles en sistemas de control de versiones como CVS 
y SVN, a continuación un ejemplo de configuración: 

.. code-block:: cfg

  [buildout]
  parts =
      docfindertab
        
  # For options see http://pypi.python.org/pypi/plone.recipe.bundlecheckout
  [docfindertab]
  recipe = plone.recipe.bundlecheckout
  url = https://svn.plone.org/svn/collective/DocFinderTab/trunk
  subfolder = DocFinderTab

Ensamblaje de Plone
-------------------

.. _plone_recipe_distros:

`plone.recipe.distros`_, es una receta buildout para instalar disfribuciones de software 
bajo el concepto de paquete bundle, a continuación un ejemplo de configuración: 

.. code-block:: cfg

  [buildout]
  parts =
      productdistros
        
  # For options see http://pypi.python.org/pypi/plone.recipe.distros

  # Quills products:
  [productdistros]
  recipe = plone.recipe.distros
  urls =
      http://plone.org/products/quills/releases/1.6/quills-1-6-beta1.tgz

.. _collective_recipe_plonesite:

`collective.recipe.plonesite`_, es una receta buildout para crear
y actualizar un sitio Plone. Este receta le permite habilitar de crear y
actualizar un sitio Plone como parte de una ejecución buildout. 

Este receta sólo tiene por objeto ejecutar perfiles y productos en la herramienta
:ref:`portal_quickinstaller <zmi_portal_quickinstaller>`. Se supone que los métodos 
de instalación, ``setuphandlers``, pasos de actualización, y otras recetas 
se encargará del resto del trabajo, a continuación un ejemplo de configuración: 

.. code-block:: cfg

  [buildout]
  parts =
      plonesite
       
  # For options see http://pypi.python.org/pypi/collective.recipe.plonesite
  [plonesite]
  recipe = collective.recipe.plonesite
  site-id = Plone
  instance = instance
  profiles =
      collective.myapp:default

.. _collective_recipe_updateplone:

`collective.recipe.updateplone`_, es una receta buildout para actualizar sitios Plone, 
a continuación un ejemplo de configuración: 

.. code-block:: cfg

  [buildout]
  parts =
      update-site
        
  # For options see http://pypi.python.org/pypi/collective.recipe.updateplone
  [update-site]
  recipe = collective.recipe.updateplone
  plone-site = instance.Plone
  install = mypackage.policy
  run-once = False
  migrate-plone = True
  backup-db = True
  pack-db = True


Servicios y hosting
-------------------

.. _plone_recipe_command:

`plone.recipe.command`_, es una receta buildout para ejecutar
instrucciones desde linea de comando arbitrariamente desde buildout, 
a continuación un ejemplo de configuración: 

.. code-block:: cfg

  [buildout]
  parts =
      mkdir-config
        
  # For options see http://pypi.python.org/pypi/plone.recipe.command
  [mkdir-config]
  recipe = plone.recipe.command
  command =
    mkdir ${buildout:directory}/config
  update-command = ${mkdir-config:command}

.. _collective_recipe_backup:

`collective.recipe.backup`_, proporciona parámetros por defecto
para las tareas de respaldo de datos comunes. El script :command:`./bin/repozo` es
un script zope para hacer copias de seguridad de :file:`Data.fs`.

`plone.recipe.apache`_, es una receta buildout para compilar,
instalar un `servidor Web Apache`_ desde los archivos fuentes con la
configuración adecuada.

`zest.recipe.mysql`_, es una receta buildout para definir una base de datos `MySQL`_.

`z3c.recipe.ldap`_, es una receta buildout para desplegar una servidor `OpenLDAP`_.


Recetas disponibles
===================

Existe una lista de recetas buildout disponibles en los siguientes enlaces:

- `Lista de recetas Buildout`_.
- `Recetas Buidout disponibles en PYPI`_.


Artículos relacionados
======================

.. seealso:: Artículos sobre :ref:`replicación de proyectos Python <python_buildout>`.


Referencias
===========

- `Gestión de proyectos con Buildout`_ desde la comunidad Plone Venezuela.

.. _plone.recipe.command: http://pypi.python.org/pypi/plone.recipe.command
.. _plone.recipe.distros: http://pypi.python.org/pypi/plone.recipe.distros
.. _collective.recipe.plonesite: http://pypi.python.org/pypi/collective.recipe.plonesite
.. _collective.recipe.updateplone: http://pypi.python.org/pypi/collective.recipe.updateplone
.. _mr.developer: http://pypi.python.org/pypi/mr.developer
.. _infrae.subversion: http://pypi.python.org/pypi/infrae.subversion
.. _plone.recipe.bundlecheckout: http://pypi.python.org/pypi/plone.recipe.bundlecheckout
.. _collective.recipe.backup: http://pypi.python.org/pypi/collective.recipe.backup
.. _servidor Web Apache: http://httpd.apache.org/
.. _plone.recipe.apache: http://pypi.python.org/pypi/plone.recipe.apache
.. _MySQL: http://www.mysql.com/
.. _zest.recipe.mysql: http://pypi.python.org/pypi/zest.recipe.mysql
.. _OpenLDAP: http://es.wikipedia.org/wiki/OpenLDAP
.. _z3c.recipe.ldap: http://pypi.python.org/pypi/z3c.recipe.ldap
.. _Lista de recetas Buildout:  http://www.buildout.org/en/latest/docs/recipelist.html
.. _Recetas Buidout disponibles en PYPI: http://pypi.python.org/pypi?:action=search&term=recipe+buildout&submit=search
.. _Gestión de proyectos con Buildout: http://coactivate.org/projects/ploneve/gestion-de-proyectos-con-buildout