.. -*- coding: utf-8 -*-

.. highlight:: rest

.. _que_es_zodb:

===========================
Zope Object Database - ZODB
===========================

:Autor(es): Leonardo J. Caballero G.
:Correo(s): leonardocaballero@gmail.com
:Compatible con: Plone 3, Plone 4
:Fecha: 19 de Diciembre de 2013

La Zope Object Database (ZODB) es una base de datos orientada a objetos 
para almacenar de forma transparente y persistente objetos en el lenguaje 
de programación Python. Se incluye como parte de Zope, un Servidor de 
aplicaciones Web, pero también puede ser utilizado independientemente de Zope.

Características
===============

Las características de la ZODB se incluyen: 

- Transacciones.

- Historial / deshacer.

- Almacenamiento conectable de forma transparente.

- Almacenamiento en caché.

- Control de concurrencia multiversión (multiversion concurrency control - MVCC).

- Escalabilidad a través de una red (usando :ref:`ZEO <que_es_zeo>`).

Historia
========

-  Creado por `Jim Fulton <http://www.zope.com/about_us/management/james_fulton.html>`_ de 
   `Zope Corporation <http://es.wikipedia.org/wiki/Zope#Zope_Corporation>`_ a finales de los años 90.

-  Inicio como un simple sistema de `persistencia de
   Objetos <https://es.wikipedia.org/wiki/Persistencia_de_objetos>`_ (Persistent Object System -
   POS) durante el desarrollo de Principia (el cual posteriormente sería
   Zope).

-  ZODB 3 fue renombrada cuando un cambio significante de la
   arquitectura fue publicado.

-  ZODB 4 fue un proyecto de corta duración para volver a poner
   re-implementar todo el paquete de ZODB 3 usando 100% Python.

.. _que_es_zeo:

ZEO
===

ZEO *(Zope Enterprise Objects)*, es una implementación de almacenamiento de 
ZODB que permite varios procesos de clientes a la `persistencia de
objetos <https://es.wikipedia.org/wiki/Persistencia_de_objetos>`_ en un único servidor ZEO. Esto
permite la escalabilidad transparente, pero el servidor ZEO es todavía
un punto único de fallo.

Almacenes de datos basado en conectores
=======================================

-  `FileStorage <http://docs.zope.org/zope2/zdgbook/ZODBPersistentComponents.html>`_
   - Permite que un único proceso de Python para hablar con un archivo
   en el disco.
   
-  `BlobStorage <https://pypi.python.org/pypi/plone.app.blob>`_ -
   Permite a los grandes datos binarios ser gestionado por la ZODB, pero
   separado de su habitual base de datos *FileStorage*, es decir
   :file:`Data.fs`. Esto tiene varias ventajas, la más importante un archivo
   :file:`Data.fs` mucho más pequeños y un mejor rendimiento tanto en CPU,
   así como de la memoria.

-  `RelStorage <https://pypi.python.org/pypi/RelStorage>`_ - Permite el
   almacenamiento de respaldo persistencia para ser un
   `RDBMS <https://es.wikipedia.org/wiki/RDBMS>`_.

-  :ref:`NetworkStorage <que_es_zeo>` (también conocido como
   :ref:`ZEO <que_es_zeo>`) - Permite cargar varios procesos de Python y
   almacenar instancias persistentes al mismo tiempo.

-  `DirectoryStorage <http://dirstorage.sourceforge.net/>`_ - Cada dato
   persistente se almacena como un archivo separado en el sistema de
   archivos. Al igual que en FSFS en `Subversion <https://es.wikipedia.org/wiki/Subversion>`_.

-  `DemoStorage <http://docs.zope.org/zope3/Code/ZODB/DemoStorage/index.html>`_
   - Un fondo en memoria para el almacenamiento persistente. Proporcione
   un ejemplo de implementación de un almacenamiento completo sin
   distraer información acerca del almacenamiento, este tipo de
   almacenamiento es volátil lo cual es útil para dar demostraciones.

-  BDBStorage - que utiliza `Berkeley DB <https://es.wikipedia.org/wiki/Berkeley_DB>`_ back-end.
   Ahora abandonada.

Tecnologías de conmutación por error
====================================

-  `Servicios de replicación de Zope (ZRS) <https://pypi.python.org/pypi/zc.zrs>`_ 
   Es un producto que elimina el punto único de fallo, proporcionando copia de seguridad 
   en caliente de las escrituras y lecturas de balanceo de carga.

-  `ZEORaid <https://pypi.python.org/pypi/gocept.zeoraid>`_, es una
   solución de código abierto que proporciona un servidor proxy de red
   que distribuye el almacenamiento de objetos y la recuperación a
   través de una serie de servidores de red.

-  `RelStorage <https://pypi.python.org/pypi/RelStorage>`_, usa las
   tecnologías de `RDBMS <https://es.wikipedia.org/wiki/RDBMS>`_ así de esta 
   forma se evitas la necesidad de servidor :ref:`ZEO <que_es_zeo>`.

-  NEO - Distribuido (tolerancia a fallos, equilibrio de carga) la
   aplicación de almacenamiento. No está listo para su uso en producción
   todavía (a partir de 01/2011).

.. _directorios_zodb:

Directorios de ZODB
===================

En el directorio :file:`var/filestorage/` se encuentran los siguiente archivos:

- :file:`Data.fs` es la base de datos como tal.

- :file:`Data.fs.lock` es para señalar que :file:`Data.fs` esta en uso.

- :file:`Data.fs.index` guarda una copia del indice.

- :file:`Data.fs.tmp` se usa para operaciones como pack.
