.. -*- coding: utf-8 -*-

.. _reparacion_zodb:

Reparación de ZODB
==================

.. sidebar:: Sobre este artículo

    :Traductor(es): Leonardo J. Caballero G.
    :Correo(s): leonardocaballero@gmail.com
    :Compatible con: Plone 3, Plone 4
    :Fecha: 30 de Agosto de 2014

.. note::
    En esta es una traducción del articulo llamado `ZODB reparieren`_ donde 
    se ofrece la información de como reparar una ZODB.

En una base de datos Zope puede estar dañada, por ejemplo, por
una caída del sistema o fallo del disco duro. Esto se vuelve
más notable por un *POSKeyError* o *CorruptedError* y entonces
ya no tenemos objetos editables.

.. _reparar_corruptederror:

CorruptedError
~~~~~~~~~~~~~~

Este error puede tener varias causas, por ejemplo, longitudes incorrectas o
tiempos de las transacciones.

:program:`fsrecover.py` es un script que verifica la integridad de las transacciones 
y la distancia con los datos corruptos. Por lo tanto, no es para *POSKeyErrors*
adecuado sino más bien recomendado para *CorruptedErrors*. Además, también puede
conducir a más *POSKeyErrors* cuando se retira una mala operación, dejando de ese 
modo la referencia a un objeto ya no existente:

::

    $ ./bin/zopepy eggs/ZODB3-3.10.2-py2.6-linux-x86_64.egg/ZODB/fsrecover.py \
    -P 0 var/filestorage/Data.fs var/filestorage/Data.fs.recovered &> logrecover.txt

A continuación en el archivo :file:`logrecover.txt`, puede comprobar cuántos datos se
han perdido, incluyendo:

::

    Recovering var/filestorage/Data.fs into var/filestorage/Data.fs.recovered
    . 1 . 2 . 3 . 4 . 5 . 6 . 7 . 8 . 9 . 0
    0 bytes removed during recovery
    Packing ...

.. _reparar_poskeyerror:

POSKeyError
~~~~~~~~~~~

Para entender este error, es importante saber que cada objeto de la base de datos tiene
un identificador único (``OID``) que se le ha asignado. Este ``OID`` es un número binario, como ``0x40A90L`` que hace referencia a un objeto serializado. En un *POSKeyError* ahora se puede encontrar por un ``OID`` no objeto adecuado. Así, por ejemplo, almacene una carpeta que se deriva de ``OFS.ObjectManager``, los objetos como valores de atributos ``_objects``. El listado resultante se compilará cuando se guarda en una lista de OID. Ahora se puede cargar el método ``objectValues()`` de un OID ya no puede asignar a un objeto serializado, entonces se emite un *POSKeyError*.


#. Con el paquete `zc.zodbdgc <http://pypi.python.org/pypi/zc.zodbdgc>`_ 
   viene con el script :program:`multi-zodb-check-refs` que permite la verificación 
   de varias ZODB. Está atravesara desde la raíz a través de toda la base de
   datos. Esto es para asegurar que todos los objetos son accesibles y cada
   objeto no alcanzable se pueden registrar. Por otra parte, se comprueba
   el Blobstorage y si si sus archivos se pueden cargar.

#. Para instalar el paquete ``zc.zodbdgc`` en un entorno
   virtual con ``virtualenv`` debe ejecutar los siguientes comandos:

   ::

       $ easy_install-2.6 virtualenv
       $ virtualenv --no-site-packages zeo_check


#. Entonces una ves creado en este entorno instale ``zc.zodbdgc``:

   ::

       $ cd zeo_check
       $ ./bin/easy_install zc.zodbdgc


#. Compacte su ZODB y luego copiarlos en el entorno ``virtuelenv``.

#. Crear un archivo de configuración :file:`storages.cfg` con el siguiente 
   contenido:

   ::

       <zodb>
         <filestorage my>
            path var/filestorage/my.fs
            blob-dir var/blobstorage-my
         </filestorage>
       </zodb>

#. A continuación, el script :program:`multi-zodb-check-refs` puede ser 
   ejecutado con el siguiente comando:

   ::

       $ ./bin/multi-zodb-check-refs storages.cfg

   ¿Son todas las referencias a su base de datos es válida?, recibirá 
   ninguna salida. En POSKeyErrors la salida se ve como el siguiente ejemplo:

   ::

       !!! main 26798 ?
       POSKeyError: 0x68ae

Examen periódico y notificación por correo electrónico
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Este script debe ejecutarse regularmente como un tarea de :program:`cron`:

::

    # Check ZEO Storages
    0 6 * * * cd /home/veit/zeo_check; ./bin/multi-zodb-check-refs \
    | mailx -s "Check Storages" -c admin@veit-schiele.de

Restaurar
~~~~~~~~~

#. Tal vez los objetos que faltan se pueden restaurar desde
   la copia de seguridad.

#. Con la opción ``-r`` obtendrá una base de datos con referencias
   opuestas, lo que puede descubrir en su caso, qué objetos faltan:

   ::

       $ ./bin/multi-zodb-check-refs -r var/filestorage/refdb.fs storages.cfg
       !!! main 26798 main 16717
       POSKeyError: 0x68ae

#. Ahora escribe un archivo :file:`refdb.cfg` con el siguiente contenido:

   ::

       <zodb main>
           <filestorage 1>
                 path /home/veit/zeo_check/var/filestorage/refdb.fs
           </filestorage>
       </zodb>

#. A continuación, puede abrir la base de datos:

   ::

       $ ../myproject/bin/zopepy
       >>> import ZODB.config
       >>> db = ZODB.config.databaseFromFile(open('./refdb.cfg'))
       >>> conn = db.open()
       >>> refs = conn.root()['references']

   Ahora debería obtener un mensaje de error como este:

   ::

       !!! main 13184375 ?
       POSKeyError: 0xc92d77

#. Ahora usted puede averiguar el OID del objeto referenciado por el de:

   ::

       >>> parent = list(refs['main'][13184375])
       >>> parent
       [13178389]

#. Ahora bien, si se carga este objeto, usted debe obtener un POSKeyError:

   ::

       >>> app._p_jar.get('13178389')
       2010-07-16 15:30:18 ERROR ZODB.Connection Couldn't load state for 0xc91615
       Traceback (most recent call last):
       …
       ZODB.POSException.POSKeyError: 0xc92d77

#. Podemos, sin embargo, los datos reales de la carga objeto padre para
   obtener una idea acerca de este objeto:

   ::

       >>> app._p_jar.db()._storage.load('\x00\x00\x00\x00\x00\xc9\x16\x15', '')
       ('cBTrees.IOBTree
       IOBucket
       q\x01.((J$KT\x02ccopy_reg
       _reconstructor
       q\x02(cfive.intid.keyreference
       KeyReferenceToPersistent
       …

#. Ahora vamos a crear un objeto falso que tiene el mismo OID (``13184375``) como
   el objeto que falta por medio de:

   ::

       $ ./bin/instance-debug debug
       Starting debugger (the name "app" is bound to the top-level Zope object)
       …
       >>> import transaction
       >>> transaction.begin()
       >>> from ZODB.utils import p64
       >>> p64(26798)
       '\x00\x00\x00\x00\x00\x00h\xae'
       >>> from persistent import Persistent
       >>> a = Persistent()
       >>> a._p_oid = '\x00\x00\x00\x00\x00\x00h\xae'
       >>> a._p_jar = app._p_jar
       >>> app._p_jar._register(a)
       >>> app._p_jar._added[a._p_oid] = a
       >>> transaction.commit()

#. Ahora debería de nuevo puede llamar al objeto en sí mismo, así como
   el objeto principal:

   ::

       >>> app._p_jar.get('\x00\x00\x00\x00\x00\x00h\xae')
       <persistent.Persistent object at 0xab7f9cc>
       >>> app._p_jar.get('\x00\x00\x00\x00\x00\xc9\x16\x15')
       BTrees.IOBTree.IOBucket([(39078692, <five.intid.keyreference…

#. Por último, aún debe cerrar la conexión con la base de datos:

   ::

       >>> conn.close()
       >>> db.close()

Faltan archivos BLOB
^^^^^^^^^^^^^^^^^^^^

Si recibe el mensaje de error ``POSKeyError: 'No blob file'``, 
Mikko Ohtamaa escribió un script `fixblobs.py`_, con el puede
eliminar el contenido de la ZODB, para el contenido que no está
más disponible como BLOB. Consulte el articulo `Fixing POSKeyError: ‘No blob file’ content in Plone <http://opensourcehacker.com/2012/01/05/fixing-poskeyerror-no-blob-file-content-in-plone/>`_.

Otras herramientas útiles
~~~~~~~~~~~~~~~~~~~~~~~~~


:program:`analyze.py`
    Muestra información como OID, tamaño, etc, de los objetos
    en la base de datos.

:program:`fstest.py`
    Comprueba las transacciones corruptas de la base de datos.

:program:`fsrecover.py`
    reparar error de transacción en la base de datos.
    error de transacción reparado en la base de datos.

Más información
~~~~~~~~~~~~~~~

-  `Recovering from BTree corruption <http://www.mail-archive.com/zodb-dev@zope.org/msg02535.html>`_

-  `Inspecting a ZODB to find the causes of bloat <http://www.zopelabs.com/cookbook/1114086617>`_

-  `Introduction to the Zope Object Database <http://www.python.org/workshops/2000-01/proceedings/papers/fulton/zodb3.html>`_

-  `Finding the last changed object in a ZODB <http://blogs.nuxeo.com/sections/blogs/lennart_regebro/2006_06_28_finding-last-changed-object-in-zodb>`_

- `Fixing a zope database with fsrecover.py`_.

- `Recovering Corrupted Data.fs ZODB files`_.

- `Packing and copying Data.fs from production server for local development`_.

- `ZODB repair PosKeyErrors in Plone and Zope`_.

.. _ZODB reparieren: http://www.plone-entwicklerhandbuch.de/plone-entwicklerhandbuch/produktivserver/zodb-reparieren
.. _Fixing a zope database with fsrecover.py : http://play.pixelblaster.ro/zope-plone-tips/fixing-a-zope-database-with-fsrecover.py
.. _Recovering Corrupted Data.fs ZODB files: http://old.zope.org/Members/itamar/CorruptedZODB
.. _Packing and copying Data.fs from production server for local development: http://opensourcehacker.com/2009/09/01/packing-and-copying-data-fs-from-production-server-for-local-development/
.. _ZODB repair PosKeyErrors in Plone and Zope: http://www.derstappen-it.de/tech-blog/zodb-repair
.. _fixblobs.py: https://gist.github.com/macagua/4fa954022a0145da9afd
