.. -*- coding: utf-8 -*-

.. _backup_zodb:

Backup de la ZODB
=================

.. sidebar:: Sobre este artículo

    :Traductor(es): Leonardo J. Caballero G.
    :Correo(s): leonardocaballero@gmail.com
    :Compatible con: Plone 3, Plone 4
    :Fecha: 25 de Agosto de 2014

.. note::
    En esta es una traducción del articulo llamado `Backup der ZODB`_ donde 
    se ofrece la información de como reparar una ZODB.

Zope viene con :program:`repozo.py` con un script que le permite realizar 
copias de seguridad de la ZODB durante la operación. 

Es como ya se tiene :program:`zeopack.py` en ``parts/zope2/utilities/ZODBTools/``. 
Además, se puede personalizar con :program:`repozo.py` para crear copias de seguridad
incrementales. 

La receta ``plone.recipe.zope2instance`` es creado como una envoltura a :program:`bin/repozo`.

Para generar una copia de seguridad incremental, primero que debe crear el 
directorio :file:`backups`, que corresponden antes de que el script :program:`repozo` 
con los siguientes parámetros:

::

    $ mkdir backups
    $ ./bin/repozo -BvzQ -r backups -f var/filestorage/Data.fs

Si se restaura una copia de seguridad una vez más, se debe detener la instancia
Zope en primer lugar, se crea una copia de los posibles ``Data.fs`` corruptos 
y sólo entonces ejecute ``repozo`` con el siguiente comando:

::

    $ ./bin/repozo -Rv -r backups -o Data.fs

.. note::
    Ejecutar :program:`repozo` después de cada :ref:`compactación de ZODB <compactar_zodb>`, 
    sólo se puede realizar una copia de seguridad completa de nuevo, la compactación se recomienda
    significativamente con menos frecuencia que la copia de seguridad. 

Este listado también se puede crear de forma automática con la receta ``z3c.recipe.usercrontab``. 
Para este propósito, inscrita en el archivo :file:`deploy.cfg` siguiente:

::

    [buildout]
    parts =
        ...
        backup-crontab
    ...
    [backup-crontab]
    recipe = z3c.recipe.usercrontab
    times = 15 0 * * *
    command =
        ${buildout:bin-directory}/repozo  -BvzQ -r ${buildout:directory}/backups \
        -f ${buildout:directory}/var/filestorage/Data.fs

Copia de seguridad de múltiples de ZODBs en una instancia
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Con la receta `collective.recipe.backup <http://pypi.python.org/pypi/collective.recipe.backup>`_
puede crear un script que puede crear copias de seguridad de múltiples ZODBs, por ejemplo, 
Además del `catálogo en su catálogo en su propia ZODB <http://www.plone-entwicklerhandbuch.de/plone-entwicklerhandbuch/produktivserver/performance/zcatalog/katalog-in-eigener-zodb>`_

::

    [buildout]
    parts =
        ...
        backup
    ...
    [backup]
    recipe = collective.recipe.backup
    additional_filestorages =
        Extra
        Super

Para aplicar múltiples puntos de montaje se utilizó la receta
``collective.recipe.filestorage``, en la sección ``[backup]`` 
también se puede simplificar:

::

    [backup]
    recipe = collective.recipe.backup
    additional_filestorages = ${filestorage:parts}

Las siguientes opciones adicionales proporciona la receta ``collective.recipe.backup``:

``location``
    Lugar donde se almacenan las copias de seguridad.

    El valor por defecto es :file:`var/backups` dentro del 
    directorio Buildout.

    El uso explícito de ``location`` es importante tener en cuenta que 
    la última parte de la especificación se usa como prefijo. La declaración:

    ::

        location = ${buildout:directory}/backups

    hay en la carpeta de proyectos buildout las subcarpetas generadas
    ``backups_Catalog`` y ``backups_Extra``. Este contendrá la copia de 
    seguridad de cada base de datos.

``keep``
    Número de copias de seguridad completas que se conservan.

    El valor por defecto es ``2``. 

    Todas las copias de seguridad anteriores, incluyendo sus copias de 
    seguridad incrementales se eliminan automáticamente. 

    Si el valor se establece en ``0``, todas las copias de seguridad se
    mantienen.

``datafs``
    Si los :file:`Data.fs` no está en el almacenamiento de carpetas por defecto
    :file:`var/filestorage/Data.fs`, la ruta se puede sobrescribir con esta opción.

``full``
    Por lo general, se crean copias de seguridad incrementales. Si el valor 
    aquí definido es ``true``, cada copia de seguridad full sera creada.

``debug``
    En casos raros, si en el archivo de log esta en el nivel ``debug``
    ser escrito. Entonces usted debe aquí debe hacer énfasis en establecer
    ``True``.

``snapshotlocation``
    Lugar donde se guardan los respaldos de datos snapshot. 

    El valor por defecto es :file:`var/snapshotbackups` dentro del 
    directorio Buildout. En definición explícita se aplicarán respecto 
    la ruta de las mismas reglas para el prefijo de carpeta, como en 
    ``location``.

``gzip``
    El valor por defecto es ``true``. 

    El final está comprimido las ZODB en formato ``*.fsz`` y no ``*.fs.gz``.

``additional_filestorages``
    Aquí usted puede proporcionar información adicional, por ejemplo, si ha
    externalizado su catálogo separado en una ZODB o participado más puntos 
    de montajes de ZODBs.

Al usar la receta ``collective.recipe.backup`` este patrón cambia 
en la directiva ``command`` bajo la sección ``[backup-crontab]``:

::

    [backup-crontab]
    ...
    command = ${buildout:bin-directory}/backup -q

Eliminación de copias de seguridad antiguas
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Las copias de seguridad antiguas se deben eliminar después de un cierto tiempo. 
En nuestro ejemplo, las siguientes copias de seguridad incrementales después de dos 
semanas y copias de seguridad completas después de cinco semanas se eliminan:

::

    [buildout]
    parts =
        ...
        remove-incremental-backups
        remove-full-backups
    ...
    [remove-incremental-backups]
    recipe = z3c.recipe.usercrontab
    times = 8 0 * * *
    command = find ${buildout:directory}/backups -name \*deltafs -ctime +14 -delete

    [remove-full-backups]
    recipe = z3c.recipe.usercrontab
    times = 8 0 * * *
    command = find ${buildout:directory}/backups -name \*dat -ctime +35 -delete

.. _blob_storage:

Blob-Storages
~~~~~~~~~~~~~

Con la receta ``collective.recipe.backup`` partir de la versión 2.0
también puede ser crear copias de seguridad del almacenamiento
Blob. Desde la versión 4.0 en Plone normalmente todas las imágenes
y los archivos (*Binary large objects - Blob*) se almacenan en el
sistema de archivos. Por lo tanto también necesita copias de seguridad
de este almacenamiento blob. Si no se especifica la ubicación del
almacenamiento de blob en la receta ``plone.recipe.zope2instance`` también
puede hacerlo con ``blob_storage`` especificar explícitamente la ruta:

::

    [buildout]
    parts =
        instance
        backup

    [instance]
    recipe = plone.recipe.zope2instance
    user = admin:admin
    blob-storage = ${buildout:directory}/var/blobstorage

    [backup]
    recipe = collective.recipe.backup

Si es necesario, buildout puede crear varios scripts para crear los archivos de
copia de seguridad para los ZODBs y los almacenamientos blob:

::

    [buildout]
    parts =
        ...
        filebackup
        blobbackup

    [filebackup]
    recipe = collective.recipe.backup
    backup_blobs = false

    [blobbackup]
    recipe = collective.recipe.backup
    blob_storage = ${buildout:directory}/var/blobstorage
    only_blobs = true

Los siguientes atributos se añadieron nuevos:

``blob-storage``
    Directorio donde se guardan los blob-storage.

    Esta opción se ignora si ``backup_blobs = false``. 

    Si nada es especificado para ``blob-storage``, se intenta 
    para determinar un valor de una sección que utilice en las 
    siguientes recetas:

    -  ``plone.recipe.zeoserver``
    -  ``plone.recipe.zope2instance``
    -  ``plone.recipe.zope2zeoserver``

``blob_storage``
    Notación alternativa para ``blob_storage`` desde la receta
    ``plone.recipe.zope2instance`` también se utiliza esta variable, 
    en pero ``collective.recipe.backup`` sin embargo, se utilizan 
    guiones bajos.


``backup_blobs``
    Si se especifica o determina un valor para ``blob-storage`` 
    por lo general las copias de seguridad de los blobstorage serán
    creado. Puede esto prevenirse usando ``backup_blobs = false``.

``blobbackuplocation``
    Directorio donde se almacenan los archivos de copia de seguridad. 

    El valor por defecto es :file:`var/blobstoragebackups` dentro del 
    directorio Buildout.

``blobsnapshotlocation``
    Directorio donde se crean las copias de seguridad snapshots.

    El valor por defecto es :file:`var/blobstoragesnapshots` en 
    Directorio Buildout.

``only_blobs``
    Esto sólo creara una copia de seguridad de los Blob-Storages, no 
    los ZODBs.

    El valor por defecto es ``false``.

``use_rsync``
    Use el programa :program:`rsync` con *Hard Links* para crear las 
    copias de seguridad de blob.

    El valor por defecto es ``true``.

    Si el programa :program:`rsync` no está instalado, o debido a que los *Hard Links* 
    no funcionan (*Windows*), en este caso el atributo debe establecerse 
    en ``false``. Entonces se crea una copia simple con ``shutil.copytree``
    de Python.

Varios Blob-Storages
~~~~~~~~~~~~~~~~~~~~

Actualmente los tipos soportados por la receta ``collective.recipe.backup`` 
no Blob-Storages adicionales. Para esto posiblemente tendría que ser creado
su propia sección Buildout, lo que crea un segundo conjunto de scripts de
copia de seguridad, por ejemplo:


::

    [extrablobbackup]
    recipe = collective.recipe.backup
    blob_storage = ${buildout:directory}/var/extrablobstorage
    only_blobs = true

rsync
~~~~~

De uso común es la receta ``collective.recipe.backup`` y la herramienta :program:`rsync`
para crear la copia de seguridad. Aquí se conocen. Los *hard links* creados para
ahorrar espacio en disco y crear copias de seguridad incrementales. Sin embargo,
para esto se requiere de Linux / Unix o Mac OS X.

Con el programa :program:`rsync` ahora también puede ser usado para crear copias
de seguridad en servidores remotos: usando el script `rsync-backup.sh`_

Para el sistema operativo Windows, debería ejecutarse usando el programa `Cygwin`_. 
Si no, puede establecerse esto ``use_rsync = false`` y el directorio de almacenamiento 
de blob se copia a continuación de la copia de seguridad.

collective.recipe.rsync
^^^^^^^^^^^^^^^^^^^^^^^

Alternativamente, se utiliza la receta `collective.recipe.rsync <http://pypi.python.org/pypi/collective.recipe.rsync>`_. Para este propósito, 
por ejemplo, cree el archivo :file:`rsync.cfg` con la siguiente contenido:

::

    [rsync-file]
    recipe = collective.recipe.rsync
    source = veit-schiele.de:/srv/www.veit-schiele.de/var/filestorage/Data.fs
    target = var/filestorage/Data.fs
    script = true

    [rsync-blob]
    recipe = collective.recipe.rsync
    source = veit-schiele.de:/srv/www.veit-schiele.de/var/blobstorage/
    target = var/blobstorage/
    script = true

``script``
    Por lo general, ``collective.recipe.rsync`` llama a :program:`rsync` durante
    la instalación de la receta. Si un script adecuado (con el nombre de 
    la sección) se crea, este mismo más adelante a de ser llamado como una
    tarea de :program:`cron` para ejecutar el programa :program:`rsync`. Esto es sólo para
    asegurarse de que el script ``rsync-file`` este ejecutado antes de ejecutar
    el script ``rsync-blob``.

``port``
    Opcionalmente, puede especificar un puerto alternativo para :program:`rsync`.

.. tip::
    Para obtener más información sobre el comando :program:`rsync` consulte el el artículo 
    de Mike Rubel: `Easy Automated Snapshot-Style Backups with Linux and Rsync`_.

Referencias
~~~~~~~~~~~

- `Backup der ZODB`_.

.. _Backup der ZODB: http://www.plone-entwicklerhandbuch.de/plone-entwicklerhandbuch/produktivserver/backup-der-zodb
.. _rsync-backup.sh: https://gist.github.com/macagua/a20c3fd337c33395b507
.. _Easy Automated Snapshot-Style Backups with Linux and Rsync: http://www.mikerubel.org/computers/rsync_snapshots/
.. _Cygwin: https://www.cygwin.com/
