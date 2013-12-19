.. -*- coding: utf-8 -*-

.. _importar_exportar_data:

==========================================
Importar y exportar contenido desde el ZMI
==========================================

:Autor(es): Leonardo J. Caballero G.
:Correo(s): leonardocaballero@gmail.com
:Compatible con: Plone 3, Plone 4
:Fecha: 19 de Diciembre de 2013

El servidor de aplicaciones Zope ofrece copia las partes de la estructura 
de árbol a través de de importación / exportación. El archivo exportado es 
básicamente un `pickle Python`_ que contiene el nodo seleccionado y todos 
los nodos secundarios.

Los archivos ``.zexp`` importables debe ser colocado en el directorio 
:file:`/parts/instance/import` de su carpeta buildout en el servidor. 

Si está utilizando :ref:`ZEO Cluster <ser-zeo-o-no-ser-zeo>` definido, siempre 
se ejecutan las importaciones a través de un específico front-end de instancia, 
utilizando el acceso directo al puerto.

.. tip::

    Si realizo la exportación a través de la instancia llamada ``instance1`` 
    los archivos exportados deben estar en el directorio :file:`/parts/instance1/import`.

Tenga en cuenta que las estructura de carpetas en el directorio :file:`parts` 
se borra en cada ejecución buildout.

Cuando los archivos se colocan en el servidor en la carpeta correcta, 
la pestaña Import/Export :ref:`ZMI <que_es_zmi>` los recogerá en la 
selección de hacia abajo. No es necesario reiniciar Zope.

Más información
===============

-   `http://quintagroup.com/services/support/tutorials/import-export-plone/`_

.. _http://quintagroup.com/services/support/tutorials/import-export-plone/: http://quintagroup.com/services/support/tutorials/import-export-plone/
.. _pickle Python: http://mundogeek.net/archivos/2008/05/20/python-serializacion-de-objetos/