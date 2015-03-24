.. -*- coding: utf-8 -*-

.. _repozo_py:

Programa repozo.py
==================

.. sidebar:: Sobre esta referencia

    :Traductor(es): Leonardo J. Caballero G.
    :Correo(s): leonardoc@plone.org
    :Compatible con: Plone 3.x, Plone 4.x
    :Fecha: 23 de Marzo de 2015

El programa ``repozo.py`` le permite realizar copias de seguridad incrementales
y completas de un archivo :file:`Data.fs` e índice de la ZODB.

Opciones básicas
----------------

A continuación se describe los diversos opciones de comando: 

Utilice: ./bin/repozo [options]

Donde:

    Exactamente uno de estas opciones ``-B`` o ``-R`` debe ser especificado:

    ``-B`` / ``--backup``
        Respaldar el actual archivo ZODB.

    ``-R`` / ``--recover``
        Restaurar un archivo ZODB desde un respaldo previo.

    ``-v`` / ``--verbose``
        Modo Verbose.

    ``-h`` / ``--help``
        Imprime este texto y sale.

    ``-r dir`` / ``--repository=dir``
        Directorio repositorio que contiene los archivos de respaldos. Este argumento
        es **requerido**. El directorio ya **debe existir**. Usted no debe editar los
        archivos en este directorio, o agregar sus propios archivos allí.

.. _repozo_backup:

Opciones para -B/--backup
-------------------------

Estas siguientes opciones son para realizar copias de seguridad

    ``-f file`` / ``--file=file``
        Archivo fuente Data.fs.  Este argumento es requerido.

    ``-F`` / ``--full``
        Forzar una copia de seguridad completa. Por defecto, una copia de
        seguridad incremental se hace si es posible (por ejemplo, si se ha
        producido una compactación desde la última copia de seguridad
        incremental, es necesaria una copia de seguridad completa).

    ``-Q`` / ``--quick``
        Verificar a través de la suma de comprobación ``md5`` sólo la última
        copia de seguridad incremental por escrito. Esto reduce significativamente
        el disco i/o en el (teórico) costo de la inconsistencia. Esta es una manera
        probabilística de determinar si es necesaria una copia de seguridad completa.

    ``-z`` / ``--gzip``
        Comprimir con ``gzip`` los archivos de copia de seguridad. Utiliza
        el nivel de compresión ``zlib`` defecto.  De forma predeterminada,
        no se utiliza la compresión ``gzip``.

    ``-k`` / ``--kill-old-on-full``
        Si se crea una copia de seguridad completa, eliminar todos los archivos
        de copia de seguridad completa o incremental anteriores (y archivos
        de metadatos asociados) desde el directorio del repositorio.

.. _repozo_recover:

Opciones para -R/--recover
--------------------------

Estas siguientes opciones son para restuarar copias de seguridad dentro de ZODB.

    ``-D str`` / ``--date=str``
        Recuperar el estado de una ZODB a partir de esta fecha. Especifique el
        tiempo en formato UTC (no formato local) ``yyyy-mm-dd[-hh[-mm[-ss]]]``.
        Por defecto, se utiliza la hora actual.

    ``-o filename`` / ``--output=filename``
        Escribir la ZODB recuperada al archivo indicado. Por defecto, el archivo
        se escribe en la salida estándar.

        .. note ::
            para el caso de la salida estándar, el archivo índice **no** se
            restaurará automáticamente.

.. seealso:: 
    Para ver mas información sobre las diversos opciones de comando
    :command:`./bin/repozo --help`.
