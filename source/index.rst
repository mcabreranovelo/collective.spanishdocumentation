.. -*- coding: utf-8 -*-

=========================================
Documentación oficial de Plone en Español
=========================================

Esta sección intenta recoger todo la documentación que hasta el momento 
esta traducida al Español, como resultado de la iniciativa llamada 
*traducciones plone* creada en 2008 en el sitio CoActivate.org por miembros 
de la comunidad Plone Conosur. A continuación se listan los documentos 
traducidos hasta el momento:


Instalación de Plone
====================

Este sección se dedica a recopilar las diversas formas de instalación de Plone 
en diversos Sistemas operativos como Windows, OS X, Linux, BSD (distribución de 
software Berkeley) y prácticamente cualquier otra plataforma.

.. toctree::
   :maxdepth: 1

   instalacion/requerimientos_sistema_plone
   instalacion/instalando_plone


Uso de Plone
============

Plone es un Sistema de gestión de contenidos muy completo y útil,
por lo que es muy importante conocerlo para poder tomar máxima ventaja de
estos CMS.  

En esta sección tenemos el tutorial traducción oficial a los manuales de usuario 
y administración de elementos de Plone.

.. toctree::
   :maxdepth: 1


   Manual de Usuario de Plone 3 <manuales/usando_plone3/index>
..
   Manual de Usuario de Plone 2.5 (En proceso) 
   Manual de Usuario de Plone 4 (En proceso) 


Desarrollo en Zope/Plone
========================

Plone es un Sistema de gestión de contenidos muy completo y útil,
por lo que es muy importante conocer las técnicas y tecnologías que 
agilicen nuestro desarrollo.

.. toctree::
   :maxdepth: 1

   apariencias/index
   Realizando pruebas en Plone 3 <programacion/haciendo_pruebas/index>

----

==========================
Mejores Practicas de Plone
==========================

Esta sección intenta recoger todo la documentación disponible en en Español, 
sobre las *Mejores Practicas de Plone*, esta es resultado de la iniciativa de 
*Carlos de la Guardia* que publica esta documentación en busca de promover la 
documentación en Español, desde entonces esta documentación es mantenida por 
miembros de la comunidad Plone Conosur. A continuación se listan los documentos 
traducidos hasta el momento:

Introducción
============

Desarrollar un sitio con Plone requiere de la combinación de una serie de
tecnologías y conocimientos, desde HTML hasta desarrollo avanzado con Python.
A lo largo del tiempo, la comunidad de Plone ha ido experimentando y
adoptando diversas formas de trabajar un proyecto, las cuales hoy en día
pueden considerarse como las mejores practicas de desarrollo con Plone.

Algunas de estas practicas se refieren por supuesto a la programación con
Python y a la construcción de aplicaciones administración de contenido con
Plone, pero hay algunas otras que rebasan el ámbito de Plone y son útiles
para cualquier ambiente de desarrollo.

En este texto vamos a abordar una por una diversas practicas que consideramos
invaluables para el trabajo profesional con Plone. La intención es demostrar
la manera en que se integra un ambiente de desarrollo ideal para desarrollar
con Plone.

Además de las mejores practicas, conoceremos en detalle algunas de las
principales tecnologías de Zope y Plone.

En particular, conoceremos:


.. hlist::
   :columns: 2

   * :ref:`Tutoriales de control de versiones <rcs_index>`.

   * :ref:`Tutoriales de Python <python_index>`.

----

Buildout y sus complementos
===========================

Buildout es un sistema que permite definir ambientes de desarrollo
que pueden ser replicados, incluyendo dependencias y configuración. Buildout 
se apoya fuertemente en setuptools, que permite instalar paquetes de Python 
a través de Internet. Es recomendable utilizar buildout para cualquier proyecto 
de Plone que se quiera emprender.

.. hlist::
   :columns: 2

   * :ref:`Replicación de proyectos Python <python_buildout>`.

   * :ref:`Hola mundo en zc.buildout <buildout_holamundo>`.
   
   * :ref:`Recipes Buildout <recipe_buildout>`.
   
   * :ref:`Programar tareas con crontab <buildout_crontab>`.
   
   * :ref:`Rotar archivos .log de Zope <buildout_logrotate>`.
   
   * :ref:`Buildout para instalar de todas las partes de un sitio <plone_esquema_alta_disponibilidad>`.
   
   * :ref:`Buildout y Plone 3 <buildout_plone3>`.
   

Administración de Zope
======================

Plone esta basado en el servidor de aplicaciones Zope y este requiere realizar 
tareas de hospedaje y administrativa para un servidor de aplicación Zope / 
sitio de Plone.

.. hlist::
   :columns: 3

   * :ref:`Zope Management Interface - ZMI <zmi>`.
   
   * :ref:`Comando de control de Zope <linea_comando_zope>`.
   
   * :ref:`Configuraciones generales <configuraciones_generales>`.
   
   * :ref:`Configurar Zope y Plone como un demonio / servicio <configurar_zope_como_demonio>`.
   
   * :ref:`Configurar Zope como un servidor FTP <zope_como_ftp>`.
   
   * :ref:`Configurar Zope como un servidor WebDAV <zope_como_webdav>`.
   
   * :ref:`Zope Object Database - ZODB <que_es_zodb>`.
   
   * :ref:`Configurar puntos de montajes para Data.fs separadas <puntos_montaje_zodb>`.
   
   * :ref:`¿Cómo compactar la ZODB de sitio Plone? <compactar_zodb>`.
   
   * :ref:`Importar y exportar contenido desde el ZMI <importar_exportar_data>`.
   
   * :ref:`Creando instancia Zope adicional de depuración <instancia_zope_debug>`.
   
   * :ref:`Ejecutando Zope y Plone detrás de un Servidor Web <zope_plone_webserver>`.

Administración de Plone
=======================

Desde el CMS Plone puede realizar labores administrativas propias del sitio web, 
este apartado busca aglomerar una serie de artículos útiles sobre estas labores.

.. toctree::
   :maxdepth: 1

   instalacion/productos/index

Desarrollo en Plone
===================

Existen muchos temas importantes para el desarrollo con Plone, en esta
sección tocaremos algunos de ellos.

.. toctree::
   :maxdepth: 1

   programacion/tipos_productos
   programacion/crear_producto_policy
   programacion/crear_producto_tema

Tecnologías de Zope
-------------------

Plone esta basado en el servidor de aplicaciones Zope y en un ``toolkit`` de
desarrollo de portales llamado CMF. Para trabajar con Plone es necesario
conocer diversas tecnologías provenientes de estos sistemas.

.. toctree::
   :maxdepth: 1

   programacion/zca/zca-es
   programacion/zope_page_templates
   programacion/herramienta_zcatalog
   programacion/flujo_de_trabajo
   programacion/perfiles_genericsetup

Diversos tutoriales en Plone
============================

En esta sección agrupamos una serie de mini tutoriales acerca de algunas de
las demostraciones más solicitadas por participantes en cursos de Plone.
Muchas demuestran el poder de Python o de APIs de Javascript más que el
manejo de Plone, pero por lo menos permiten conocer como enfocar situaciones
comunes en aplicaciones web con Plone.

.. toctree::
   :maxdepth: 2
   
   tutoriales/index


Otros recursos
==============

.. toctree::
   :maxdepth: 1

   glosario
   enlaces
   presentaciones/index


============================
Acerca de esta documentación
============================

Guía de instrucciones y estilos para el 
mantenimiento de esta documentación.

.. toctree::
   :maxdepth: 1

   escribiendo/index