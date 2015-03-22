.. -*- coding: utf-8 -*-

.. _desarrollar_productos:

========================================
Desarrollar diversos productos con Plone
========================================

.. sidebar:: Sobre este artículo

    :Autor(es): Carlos de la Guardia, Leonardo J. Caballero G.
    :Correo(s): carlos.delaguardia@gmail.com, leonardoc@plone.org
    :Compatible con: Plone 3.x, Plone 4.x
    :Fecha: 21 de Marzo de 2015

En esta articulo busca explicar los tipos desarrollos de productos / módulos
disponibles para Plone.

Introducción
============

Un sitio basado en :ref:`Plone <que_es_plone>` es muy complejo y se compone de
una colección de elementos como contenido, configuración y recursos de presentación.
La tendencia desde Plone 3 hasta la actualidad en Plone 4 y Plone 5 es separar lo más
posible todas estas áreas, para permitir un desarrollo organizado y estructurado.

En la base de datos :ref:`ZODB <que_es_zodb>`, debe en lo posible almacenar
únicamente el contenido generado por los usuarios. Todo el código y configuración
del sitio deben estar en el :term:`filesystem`, de manera que puedan editarse y
generar versiones con las herramientas comunes de desarrollo y no queden encerrados
en la :ref:`ZODB <que_es_zodb>`. Esto también permite una distribución e instalación
más sencillas.

.. todo::
    Por explicar los posibles formas de hacer paquetes Plone.

.. _desarrollar_productos_tipos:

Tipos de productos
==================

La estructura del código que se recomienda incluye las siguientes partes:

.. _productos_plone_theme:

Producto de tema
----------------

Conocido en Ingles como **plone theme product**, este producto incluye uno o más
productos que definan un "skin" de Plone que especifique la presentación visual
del sitio. Cada uno puede incluir:

* Estilos de CSS.

* Archivos de Javascript.

* Archivos de Imágenes.

* Plantillas de Plone modificados.

* Plantillas originales del tema.

* Vistas y viewlets especiales.
      
.. seealso:: Para crear este producto consulte el articulo :ref:`Creación de un paquete de tema <producto_tema>`.

.. _productos_content_types:

Productos de contenido
----------------------

Conocido en Ingles como **content types product**, este es uno o varios productos que
definen los tipos de contenido que representan la base del sitio web.

* Definición de tipos y campos.

* Flujo de trabajos específicos para un tipo de contenido.

* Vistas y viewlets especiales para un tipo de contenido.

* Imágenes y estilos propios del contenido.

* Portlets propios del contenido.

* Índices y metadatos del catálogo para cada tipo utilizado.

.. todo::
    Escribir un articulo sobre este punto

.. _productos_policy_plone:

Producto de configuración
-------------------------

Conocido en Ingles como **policy product**, este producto incluye toda la configuración
general del sitio. Representa las reglas generales de manejo de sitios Plone de una
organización y puede incluir:

* Configuraciones del sitio y propiedades de navegación.

* Productos propios y de terceros que deben instalarse automáticamente con el sitio.

* Configuraciones de viewlets.

* Estructura inicial de contenido del sitio.

* Pasos adicionales a la instalación del producto, como creación de cuentas de usuarios 
  y contenido personalizado.

* Portlets utilizados en el sitio.

* Flujo de trabajos generales de la organización.
      
.. seealso:: Para crear este producto consulte el articulo :ref:`Creación de un producto
    de configuración <producto_policy>`.

.. _productos_utils_portal:

Productos de apoyo
------------------

Uno o varios productos que realicen funciones no específicamente asociadas al contenido.

* Utilerías (herramientas tipo *portal_xxx*).

* Portlets generales.

* Vistas y viewlets especiales.

* Funcionalidades que extiendan Plone.

.. todo::
    Escribir un articulo sobre este punto

Referencia
==========

- `Desarrollo avanzado de sitios con Plone 3`_ desde la comunidad Plone México.

.. _Desarrollo avanzado de sitios con Plone 3: http://www.plone.mx/docs/productos.html
