.. -*- coding: utf-8 -*-

.. _actualizar_zcatalog:

Actualizar el ZCatalog
======================

.. sidebar:: Sobre este artículo

    :Autor(es): Leonardo J. Caballero G.
    :Correo(s): leonardocaballero@gmail.com
    :Compatible con: Plone 3, Plone 4
    :Fecha: 26 de Agosto de 2014

El ZCatalog
-----------

Es el motor de búsqueda incorporado en Zope. Le permite clasificar
y buscar todo tipo de objetos Zope. También puede utilizarlo para
buscar datos externos como datos relacionales, archivos y páginas
web remotos. Además de la búsqueda se puede utilizar el *ZCatalog*
para organizar colecciones de objetos.

Soporta una rica interfaz de consulta llamada :ref:`portal_catalog <zmi_portal_catalog>`.
En esta puede realizar búsquedas de texto completo, puede buscar
varios índices a la vez, e incluso puede especificar un peso para
los diferentes campos en los resultados. Además, el *ZCatalog* realiza
un seguimiento de meta-datos sobre los objetos indexados.

.. tip::
    El *ZCatalog* se distribuye en el producto Zope llamado `Products.ZCatalog`_.

.. _zmi_portal_catalog:

Herramienta portal_catalog
--------------------------

Provee un mecanismo poderoso de indexación y búsqueda en la :ref:`ZODB <que_es_zodb>` 
denominado :term:`Zcatalog`. Es una clase envoltorio (wrapper) de paquete `ZCatalog`_
que provee índices adicionales, metadatos y políticas específicas para las operaciones
de un sitio Plone.

Permite:

- Seleccionar vocabulario: (inglés, japonés, etc).

- Seleccionar metadata: Los valores de los atributos que coinciden con el nombre 
  en esta lista son los catalogados.

- Seleccionar índices: Los valores de cualquier atributo y método que coincide con 
  un índice en esta lista son los indexados.

- Localizar y agregar objetos al catálogo.

- Actualizar manualmente objetos en el catálogo.

- Remover objetos del catálogo.

Esta herramienta le permite a usted indexar y hacer búsquedas para objetos Zope, mas 
el ``ZCatalog`` no es simplemente un sistema administración de datos que le permite 
buscar a través de contenido. Usted tiene la opción de almacenar las propiedades en 
el Catálogo y cuales atributos se utilizan para la búsqueda.

Una vez que se introduce un conjunto de objetos en el catálogo, usted será capaz de 
actualizar el inventario objeto agregando, actualización de los objetos, o borrar estos.

Para mas detalle consulte la herramienta en 
:menuselection:`Configuración del Sitio --> Interfaz de Administración de Zope --> portal_catalog`.

.. image:: ./zmi_portal_catalog.png
  :alt: portal_catalog - ZMI
  :align: center
  :width: 742px
  :height: 288px
  :target: ../../_images/zmi_portal_catalog.png

.. _actualizar_indice:

Actualizar el índice de objetos de la ZODB con ZCatalog
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

La herramienta :ref:`portal_catalog <zmi_portal_catalog>` ofrece mecanismos
avanzado para actualizar el índice de objetos de la ZODB, acceda a la ZMI de tu sitio Plone 
:menuselection:`Configuración del Sitio --> Interfaz de Administración de Zope --> portal_catalog --> Advanced`,
allí encontrara las siguientes opciones:

.. image:: ./zmi_portal_catalog_Advanced.png
  :alt: portal_catalog - Advanced - ZMI
  :align: center
  :width: 742px
  :height: 288px
  :target: ../../_images/zmi_portal_catalog_Advanced.png

.. warning::

    Por precaución haga un respaldo de tu :ref:`ZODB <que_es_zodb>` en ubicada por defecto 
    en el directorio :file:`var/filestorage/Data.*`

**Catalog Maintenance:** con esta tarea realizas la actualización del catálogo, 
el cual actualizará todos los registros del catálogo y eliminar registros no 
válidos. Para ello, en la limpieza de todos los índices y volver a catalogar 
todos los objetos actualmente indexados. 

.. warning:: 
   
   La eliminación del catálogo eliminará todas las entradas. Si desea realizar esta 
   tarea presione el botón **Clear Catalog**.
   
   El registro de los progresos por cada N objetos re-indexado al registro Zope (esta 
   definido en 0 para deshabilitar el registro). Para activar esta funcionalidad debe 
   cambiar el valor a 1 y presione el botón **Change**.

**Clear and Rebuild:** con esta tarea se se eliminarán todas las entradas del catálogo, 
y luego caminar todo el portal en busca de objetos de contenido que deben ser indexados 
en el catálogo y el índice de ellos. Haciendo esto eliminará las entradas inapropiados 
del catálogo de portal (scripts, plantillas) y conservar todo el contenido indexado. 
Esto puede tomar mucho tiempo, pero es la forma correcta de reconstruir un catálogo que 
ha tenido indebidamente objetos añadidos o eliminados.

La actualización del índice de objetos del *ZCatalog* se podría realizar por las siguientes
razones:

* Actualizar referencia a contenido no existente en su Plone.

* La reconstrucción después de la migración masiva de contenido.

* Creación de catálogo después de la creación de objetos en las pruebas unitarias.

Referencias
-----------

-   `Using the Zope Management Interface`_.

-   `Searching and Categorizing Content`_.

.. _ZMI (Zope Management Interface): http://wiki.zope.org/zope2/ZMIZopeManagementInterface
.. _Zope Management Interface: https://weblion.psu.edu/trac/weblion/wiki/ZopeManagementInterface
.. _Using the Zope Management Interface: http://docs.zope.org/zope2/zope2book/UsingZope.html
.. _Zope Management Interface know-how for better Plone development: http://stackoverflow.com/questions/5098499/zope-management-interface-know-how-for-better-plone-development
.. _Products.ZCatalog: https://pypi.python.org/pypi/Products.ZCatalog/
.. _ZCatalog: https://pypi.python.org/pypi/Products.ZCatalog/
.. _Searching and Categorizing Content: http://docs.zope.org/zope2/zope2book/SearchingZCatalog.html
