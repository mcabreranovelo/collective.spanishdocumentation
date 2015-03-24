.. -*- coding: utf-8 -*-

.. _backup_zodb:

Respaldo de la ZODB
===================

.. sidebar:: Sobre este artículo

    :Traductor(es): Leonardo J. Caballero G.
    :Correo(s): leonardoc@plone.org
    :Compatible con: Plone 3.x, Plone 4.x
    :Fecha: 23 de Marzo de 2015

.. note::
    En esta es una traducción del articulo llamado `Backup der ZODB`_
    donde se ofrece la información de como reparar una ZODB.

Archivos de base de datos
-------------------------

Usualmente la base de datos de Plone esta configurado en el archivo
:file:`var/filestorage/Data.fs` y los archivos cargados desde la
interfaz de Plone pueden encontrarse como BLOBs in :file:`var/blobstorage`.

.. tip:: 
    Para mas detalle sobre estos archivos y directorios consulte
    :ref:`Directorios de ZODB <directorios_zodb>`.

.. _backup:

Generando copias de seguridad
-----------------------------

Zope provee un script :program:`repozo.py` que le permite realizar
copias de seguridad de la ZODB durante su funcionamiento.

Para instalaciones Plone 4.3 usando configuraciones buildout bajo Linux
se encuentra en el directorio:

- :file:`eggs/ZODB3-3.10.5-py2.7-linux-i686.egg/ZODB/scripts/repozo.py`.

.. note::
    Esto puede variar entre versiones de Plone y Zope.

.. warning::
    Ejecutar :program:`repozo` sólo se puede realizar una copia de seguridad
    completa de nuevo después de cada :ref:`compactación de ZODB <compactar_zodb>`.
    El procedimiento de compactación se recomienda realizar con significativamente menos
    frecuencia que la copia de seguridad.

.. _backup_quick:

Copias de seguridad incremental
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Para generar una copia de seguridad incremental, primero que debe crear el
directorio :file:`backups`, el cual se usara con el programa :program:`repozo`
con los siguientes comando: ::

    $ mkdir backups
    $ ./bin/repozo -BvzQ -r backups -f var/filestorage/Data.fs

.. _backup_full:

Copias de seguridad completa
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Para generar una copia de seguridad completa, se debe realizar los
siguientes pasos:

#. En primer lugar, debe crear el directorio :file:`backups`
   con el comando :command:`mkdir backups`.

#. Entonces ejecute el programa :program:`repozo`, con el siguiente comando:

.. code-block:: sh

    $ ./bin/repozo -BvzF -r backups -f var/filestorage/Data.fs

.. _restore:

Restaurar copias de seguridad
-----------------------------

Zope provee un script :program:`repozo.py` que le permite no solo realizar
copias de seguridad de la ZODB sino también restaurarlas.

.. _restore_full:

Restaurar copias de seguridad completa
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Para restaurar una copia de seguridad completa, se debe realizar los
siguientes pasos:

#. En primer lugar **detener** el servivio del servidor Zope (*Zeo* y sus clientes o
   la instancia Zope *standalone*).

#. Localiza la ruta donde se hicieron las copias de seguridad incrementales.
   Para en este articulo usamos :file:`backups`.

#. Compruebe que los archivos de copia de seguridad incrementales se encuentran
   dentro de este directorio. Las secuencias de comandos de copia de seguridad
   escriben de forma automática la base de datos en el directorio de copia de seguridad
   en uno de los dos formatos, una copia incremental y una copia de seguridad completa.
   Puede detectar la diferencia al ver las extensiones de archivo: 

   - El archivo con extensión ``.fs``, es una copia de seguridad completa.

   - El archivo con extensión ``.deltafs``, es una copia de seguridad incremental.

   .. tip::
       Cree una copia del archivo :file:`Data.fs` con los posibles objetos corruptos,
       por previsión.

#. Entonces ejecute el programa :program:`repozo` con el siguiente comando:

    .. code-block:: sh

           $ ./bin/repozo -Rv -r backups -o var/filestorage/Data.fs

   El resultado de la ejecución de comando debería ser algo así:

    .. code-block:: sh

           looking for files between last full backup and 2006-06-23-19-39-20...
           files needed to recover state as of 2006-06-23-19-39-20:
                  /srv/plone/instance/backups/2006-06-23-18-49-47.fs
                  /srv/plone/instance/backups/2006-06-23-18-55-56.deltafs
           Recovering file to /srv/plone/instance/var/filestorage/Data.fs
           Recovered 6435866 bytes, md5: 4470d48dfeae1f6201cc594142408bfe

   Esto comando examina las copias de seguridad disponibles, busca el mas reciente y
   mezcla cualquier copia de seguridad incremental (si esta presente). Ademas este
   creará un archivo :file:`Data.fs` en la ubicación especificada con el parámetro
   ``-o`` en base a las copias de seguridad realizadas por :program:`repozo`
   del repositorio llamado :file:`backups` especificado con el parámetro ``-r``.

#. Por ultimo, asegúrese de **iniciar** el servidor Zope (*Zeo* y al menos un cliente o
   la instancia Zope *standalone*.

.. _restore_date:

Restaurar copias de seguridad a partir de una fecha determinada
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A veces, es necesario retroceder en el tiempo y recuperar datos perdidos,
o crear una base de datos de pruebas de las copias de seguridad de los
datos de producción.

Para recrear el archivo de datos para una fecha en particular utilice
el programa :program:`repozo`, primero que debe tener acceso al repositorio
de copias de seguridad (en este articulo usamos :file:`backups`), el cual
se usara con el programa :program:`repozo` con el siguiente comando: ::

    $ ./bin/repozo -R --r backups --date='2014-07-02' -o var/filestorage/Data.fs

Esto comando creará un archivo :file:`Data.fs` en la ubicación especificada con
el parámetro ``-o`` en base a las copias de seguridad realizadas por :program:`repozo`
del repositorio llamado :file:`backups` especificado con el parámetro ``-r`` y con la
fecha especifica *2014-07-02* usando el parámetro ``--date``.

.. tip::
    Yo siempre uso la fecha de mañana para --date='yyyy-mm-dd' fin de obtener
    todos los cambios del día de hoy.

.. note::
    El detalle del parámetro ``--date`` se puede consultar en la referencia
    de recuperar de copia de seguridad de :ref:`repozo <repozo_recover>`.

.. _repozo_buildout:

repozo usando buildout
----------------------

Además, se puede personalizar con programa :program:`repozo.py` para
crear copias de seguridad incrementales y completas, usando la receta
`plone.recipe.zope2instance`_ crea una envoltura del script
:program:`repozo.py` que genera con el nombre :program:`repozo` en el
directorio :file:`bin`.

También se puede crear de forma automática una tarea de este comando
de respaldo de datos con la receta `z3c.recipe.usercrontab`_. Para
este propósito, inscrita en el archivo :file:`buildout.cfg` la siguiente
configuración:

.. code-block:: cfg

    [buildout]
    parts =
        ...
        backup-crontab
    
    [backup-crontab]
    recipe = z3c.recipe.usercrontab
    times = 15 0 * * *
    command =
        ${buildout:bin-directory}/repozo -BvzQ -r ${buildout:directory}/backups \
        -f ${buildout:directory}/var/filestorage/Data.fs

Copia de seguridad de múltiples de ZODBs en una instancia
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Con la receta `collective.recipe.backup`_ puede crear un script que puede crear copias
de seguridad de múltiples ZODBs. Además crear `catálogo separado para su propia ZODB`_.

.. code-block:: cfg

    [buildout]
    parts =
        ...
        backup
    
    [backup]
    recipe = collective.recipe.backup
    additional_filestorages =
        Extra
        Super

Para realizar copias de seguridad a múltiples puntos de montaje se utiliza la receta 
:ref:`collective.recipe.filestorage <puntos_montaje_zodb>`, en la sección ``[backup]`` 
también se puede simplificar:

.. code-block:: cfg

    [backup]
    recipe = collective.recipe.backup
    additional_filestorages = ${mountpoints:parts}

Las siguientes opciones adicionales proporciona la receta ``collective.recipe.backup``:

``location``
    Lugar donde se almacenan las copias de seguridad.

    El valor por defecto es :file:`var/backups` dentro del 
    directorio Buildout.

    El uso explícito de ``location`` es importante tener en cuenta que 
    la última parte de la especificación se usa como prefijo. La declaración:

    ::

        location = ${buildout:directory}/backups

    Allí en la carpeta de proyectos buildout las sub-carpetas generadas
    :file:`backups_Catalog` y :file:`backups_Extra`. Este contendrá la copia de 
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
    En casos raros, si en el archivo de log esta en el nivel ``debug`` ser escrito.
    Entonces usted debe aquí debe hacer énfasis en establecer ``True``.

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

Al usar la receta ``collective.recipe.backup`` este patrón cambia en la directiva
``command`` bajo la sección ``[backup-crontab]`` como se muestra a continuación:

.. code-block:: cfg

    [backup-crontab]
    
    command = ${buildout:bin-directory}/backup -q

Eliminación de copias de seguridad antiguas
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Las copias de seguridad antiguas se deben eliminar después de un cierto tiempo.
En este ejemplo, las siguientes copias de seguridad incrementales después de dos
semanas y copias de seguridad completas después de cinco semanas se eliminan:

.. code-block:: cfg

    [buildout]
    parts =
        ...
        remove-incremental-backups
        remove-full-backups
    
    [remove-incremental-backups]
    recipe = z3c.recipe.usercrontab
    times = 8 0 * * *
    command = find ${buildout:directory}/backups -name \*deltafs -ctime +14 -delete

    [remove-full-backups]
    recipe = z3c.recipe.usercrontab
    times = 8 0 * * *
    command = find ${buildout:directory}/backups -name \*dat -ctime +35 -delete

Puede comprobar la definición de las tareas crontab ejecutando el siguiente comando:

.. code-block:: sh

    $ crontab -l

.. _blob_storage:

Blob Storages
-------------

Nosotros podemos realizar copias de seguridad de blob storage. Desde la versión 4.0
en Plone normalmente todas las imágenes y los archivos (*Binary large objects - Blob*)
se almacenan en el sistema de archivos. En Plone 3 es opcional. Por lo tanto también
necesita copias de seguridad de este almacenamiento ``blob``. 

Con la receta ``collective.recipe.backup`` partir de la versión 2.0 también puede ser
crear copias de seguridad del almacenamiento Blob. 

Si no se especifica el directorio donde Plone (o Zope) almacena sus ``blobs`` en la receta
``plone.recipe.zope2instance`` también puede especificar explícitamente la ruta del directorio
con la declarativa ``blob_storage`` de la receta ``collective.recipe.backup``:

.. code-block:: cfg

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

.. code-block:: cfg

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
    Directorio donde se guardan los ``blob-storage``.

    Esta opción se ignora si ``backup_blobs = false``.

    Si nada es especificado para ``blob-storage``, se intenta
    para determinar un valor de una sección que utilice en las
    siguientes recetas:

    - `plone.recipe.zeoserver`_.
    
    - `plone.recipe.zope2instance`_.
    
    - `plone.recipe.zope2zeoserver`_.

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

    Si el programa :program:`rsync` no está instalado, o debido a que los
    *Hard Links* no funcionan (*Windows*), en este caso el atributo debe
    establecerse en ``false``. Entonces se crea una copia simple con
    ``shutil.copytree`` de Python.

Varios Blob-Storages
~~~~~~~~~~~~~~~~~~~~

Actualmente los tipos soportados por la receta ``collective.recipe.backup``
no Blob-Storages adicionales. Para esto posiblemente tendría que ser creado
su propia sección Buildout, lo que crea un segundo conjunto de scripts de
copia de seguridad, por ejemplo:

.. code-block:: cfg

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
de seguridad en servidores remotos: usando el script `rsync-backup.sh`_.

Para el sistema operativo Windows, debería ejecutarse usando el programa `Cygwin`_.
Si no, puede establecerse esto ``use_rsync = false`` y el directorio de almacenamiento 
de blob se copia a continuación de la copia de seguridad.

collective.recipe.rsync
^^^^^^^^^^^^^^^^^^^^^^^

Alternativamente, se utiliza la receta `collective.recipe.rsync`_. Para este propósito, 
por ejemplo, cree el archivo :file:`rsync.cfg` con la siguiente contenido:

.. code-block:: cfg

    [rsync-file]
    recipe = collective.recipe.rsync
    source = TUSITIO.COM:/srv/www.TUSITIO.COM/var/filestorage/Data.fs
    target = var/filestorage/Data.fs
    script = true

    [rsync-blob]
    recipe = collective.recipe.rsync
    source = TUSITIO.COM:/srv/www.TUSITIO.COM/var/blobstorage/
    target = var/blobstorage/
    script = true

``script``
    Por lo general, ``collective.recipe.rsync`` llama a :program:`rsync`
    durante la instalación de la receta. Si un script adecuado (con el
    nombre de la sección) se crea, este mismo más adelante a de ser llamado
    como una tarea de :program:`cron` para ejecutar el programa :program:`rsync`.
    Esto es sólo para asegurarse de que el script ``rsync-file`` este ejecutado
    antes de ejecutar el script ``rsync-blob``.

``port``
    Opcionalmente, puede especificar un puerto alternativo para :program:`rsync`.

.. tip::
    Para obtener más información sobre el comando :program:`rsync` consulte el artículo
    de Mike Rubel: `Easy Automated Snapshot-Style Backups with Linux and Rsync`_.

Referencias
~~~~~~~~~~~

- `ZODB Database`_.

- `Backup der ZODB`_.

- `Recovering a ZODB Data.fs file using repozo`_.

- `Restoring Backups`_.

.. _ZODB Database: http://docs.plone.org/develop/plone/persistency/database.html
.. _Backup der ZODB: http://www.plone-entwicklerhandbuch.de/plone-entwicklerhandbuch/produktivserver/backup-der-zodb
.. _Recovering a ZODB Data.fs file using repozo: http://www.coactivate.org/projects/opencore/recovering-the-production-database
.. _Restoring Backups: http://www.enfoldsystems.com/software/server/docs/4.0/restoring.html
.. _rsync-backup.sh: https://gist.github.com/macagua/a20c3fd337c33395b507
.. _Easy Automated Snapshot-Style Backups with Linux and Rsync: http://www.mikerubel.org/computers/rsync_snapshots/
.. _Cygwin: https://www.cygwin.com/
.. _catálogo separado para su propia ZODB: http://www.plone-entwicklerhandbuch.de/plone-entwicklerhandbuch/produktivserver/performance/zcatalog/katalog-in-eigener-zodb
.. _collective.recipe.backup: http://pypi.python.org/pypi/collective.recipe.backup
.. _collective.recipe.rsync: http://pypi.python.org/pypi/collective.recipe.rsync
.. _z3c.recipe.usercrontab: http://pypi.python.org/pypi/z3c.recipe.usercrontab
.. _plone.recipe.zope2instance: http://pypi.python.org/pypi/plone.recipe.zope2instance
.. _plone.recipe.zeoserver: http://pypi.python.org/pypi/plone.recipe.zeoserver
.. _plone.recipe.zope2zeoserver: http://pypi.python.org/pypi/plone.recipe.zope2zeoserver
