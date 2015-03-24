.. -*- coding: utf-8 -*-

.. _instancia_zope_debug:

==============================================
Creando instancia Zope adicional de depuración
==============================================

.. sidebar:: Sobre este artículo

    :Autor(es): Leonardo J. Caballero G.
    :Correo(s): leonardoc@plone.org
    :Compatible con: Plone 3.x, Plone 4.x
    :Fecha: 23 de Marzo de 2015

Es posible que desee mantener su :file:`buildout.cfg` para producción 
y sincronizar la configuración de desarrollo de forma automática 
como sea posible.

Además es de mucha utilidad para hacer analices entornos de producción,
acceder a la :ref:`interfaz administrativa de Zope <que_es_zmi>`, ver
registro de log detallados, entre otras labores administrativas de Zope.

Agregar configuración
=====================

Una buena idea es utilizar el mismo archivo :file:`buildout.cfg`, entonces
debe modificar este archivo con el siguiente comando:

.. code-block:: sh

  vim buildout.cfg

Si con cosas condicionales, como poner el modo de depuración activo, 
como es requerido, usted puede ampliar las secciones buildout, que a 
su vez crear **Instancias Zope adicionales** con la siguiente configuración:

.. code-block:: cfg

  parts =
      ...
      instance
  
  [instance]
  recipe = plone.recipe.zope2instance
  zope2-location = ${zope2:location}
  user = admin:admin
  http-address = 8080
  debug-mode = off
  verbose-security = off
  event-log-level = info

Y crea su nueva instancia ``debug`` Zope, seguidamente de la sección ``instance``
con la siguiente configuración:

.. code-block:: cfg

  parts =
      ...
      instance-debug

  # Crear un script lanzado el cual iniciará una 
  # instancia Zope en modo debug
  [instance-debug]
  # Extiende la instancia principal de producción
  <= instance

  # Aquí sobre escribes configuraciones especifica 
  # para hacer la instancia que se ejecute en modo debug
  http-address = 8008
  debug-mode = on
  verbose-security = on
  event-log-level = DEBUG

Guarde los cambios en el :file:`buildout.cfg`.

Construcción del proyecto
=========================

Para la construcción del proyecto Buildout, ejecute el siguiente comando:

.. code-block:: sh

  ./bin/buildout

Ejecutar servidor Zope2
=======================

Su instancia principal de Zope permanece en modo de producción ejecutándola
con el siguiente comando:

.. code-block:: sh

  ./bin/instance start

Y ahora usted puede iniciar si instancia de **desarrollo** Zope ejecutándola
con el siguiente comando:

.. code-block:: sh

  ./bin/instance-debug fg

.. note::

    Usando siempre el modo ``fg`` de Zope para el modo depuración, 
    pero no registra en el nivel de log.

Referencias
===========

- `Creating additional debug instances`_ from Zope Application Server by Plone Documentation.

.. _Creating additional debug instances: http://docs.plone.org/manage/deploying/zope.html#creating-additional-debug-instances
