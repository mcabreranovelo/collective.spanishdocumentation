.. -*- coding: utf-8 -*-

.. _instalar_config_propio_mirror_pypi:

==================================================
Instalar y configurar repositorios espejos de PyPI
==================================================

.. sidebar:: Sobre este artículo

    :Autor(es): Leonardo J. Caballero G.
    :Correo(s): leonardocaballero@gmail.com
    :Fecha: 31 de Diciembre de 2013

Este manual intenta ayudar a como implementar un servidor espejo (mirror) 
de :term:`paquetes Egg` Python del servidor central :term:`PyPI` localmente 
en su organización.

.. toctree::
   :maxdepth: 1

.. _creando_propio_repositorio_pypi:

Repositorios de software
========================

Una de las características principales que ha popularizado a los sistemas 
operativos Linux, son los diversos esquemas de distribución de software 
implementados en la Web para compartir y distribuir software, todo esto 
gracias a la libertad 2 del software libre.

En la actualidad existen varios tipos de paquetes de software para Linux 
de los cuales dos son los principales formatos de paquetes los **.rpm** 
de Redhat Linux y los archivos **.deb** de Debian GNU/Linux, con estos 
formatos se pueden descargar, instalar, configurar y dejar listo un paquete 
de software para que usted solo lo ejecute y lo utilice.

Una parte importante que va de la mano del sistema de paquetes, es el 
repositorio de software y es, en pocas palabras, un sitio (lugares / 
servidores) en Internet donde se almacenan un espejo (lo mismo) que contiene 
el repositorio original del proveedor de software, el cual dicho espejo puede 
ayudar a que las personas que estén mas cerca (geográficamente hablando) del 
servidor espejo, para que al momento de descargar el software se más rápidamente.

Los repositorios de software de Linux se almacenan literalmente en cientos 
de servidores espejos "mirrors" distribuidos en muchos países, por ejemplo: 

La lista de mirrors de Debian GNU/Linux incluye cientos de servidores unos 
alojados por empresas, otros por universidades, gobiernos, etc.

-   http://www.debian.org/mirror/list

En el caso de Ubuntu Linux la lista también es larga y abarca países de la letra 
"A" a la letra "Z".

-   https://launchpad.net/ubuntu/+archivemirrors

Para gestionar los ``paquetes Deb`` es necesario usar las herramientas 
:command:`dpkg`, :command:`apt` / :command:`aptitude` las cuales usan estos repositorio 
para descargar dichos paquetes.

La lista pública de mirrors de Fedora Linux también es larga y abarca países.

-   http://mirrors.fedoraproject.org/publiclist

Para gestionar los ``paquetes rpm`` es necesario usar la herramienta 
:command:`yum` la cual usan estos repositorio para descargar dichos paquetes.

Repositorio de PyPI
===================

En el caso de Python existe el sistema de :term:`paquetes Egg` y estos se 
disponen para ser distribuidos como aplicaciones y librerías Python en un 
repositorio principal dispuesto por la fundación Python en la siguiente 
dirección:

-   http://pypi.python.org/simple/

Para gestionar los :term:`paquetes Egg` es necesario instalar las herramientas 
:ref:`easy_install <que_es_easyinstall>` / :ref:`pip <que_es_pip>` las cuales 
usan este repositorio para descargar los :term:`paquetes Egg`.

Este repositorio principal posee sus mirror o espejos como se listan a 
continuación:

-   http://b.pypi.python.org/simple/

-   http://c.pypi.python.org/simple/

-   http://d.pypi.python.org/simple/

-   http://e.pypi.python.org/simple/

-   http://f.pypi.python.org/simple/

-   http://g.pypi.python.org/simple/

.. tip::

     Para mas información sobre nuevo repositorios consulte la siguiente 
     dirección http://pypi.python.org/mirrors

Si desea saber el estatus actual de sincronización de los repositorios 
oficiales puede consultar la siguiente dirección:

-   http://www.pypi-mirrors.org/

.. _que_es_z3cpypimirror:

¿Qué es z3c.pypimirror?
=======================

`z3c.pypimirror`_, es un modulo para construir un mirror *parcial* o *completo* 
de :term:`PyPI`.

Esto le permite establecer el criterio de que paquete debe sincronizara en su 
repositorio espejo, esto es muy útil, cuando requiere hacer, trabajar solo con 
ciertos paquetes, por ejemplo: 

- Si esta trabajando con el framework de django, entonces puedes filtrar que 
  ``namespaces`` de paquetes **"django-*"**, **"Django-*"**, etc; va a sincronizar localmente.

- Si esta trabajando con el framework zope, entonces puedes filtrar que ``namespaces`` 
  de paquetes **"zope.*"**, **"z3c.*"**, **"zope*"**, etc;  va a sincronizar localmente.

Por defecto, la configuración que genera sincroniza todos los paquetes del repositorio.

Existen varios repositorios públicos generados con el paquete ``z3c.pypimirror`` 
disponibles a continuación:

-   http://pypi.it.uwosh.edu/

-   http://pypi.inqbus.de/

-   http://pypi.python.jp/

-   http://pypi.blitzen.unc.edu/

-   http://pypi.pbs.org/pypi/simple/

-   http://pypi.upc.edu/mirror/

-   http://pypi.affinitic.be/

-   http://kambing.ui.ac.id/pypi/

Ahora si usted desea tener su propio servidor espejo del servidor :term:`PyPI` 
por un tema de mayor eficiencia en los recursos de ancho de banda local de su 
organización, pues bien requiere tener servidor espejo de sus paquetes privados, 
entonces necesita instalar el paquete ``z3c.pypimirror``.

Requerimientos
==============

Para instalar el paquete :ref:`z3c.pypimirror <que_es_z3cpypimirror>`, su 
instalación es muy simple, por eso estoy partiendo del principio de que 
tenemos instalado en el sistema los siguientes requerimientos:

-   El interprete `Python`_ 2.4, 2.5, 2.6, 2.7 o superior.

-   Opcionalmente la herramienta :ref:`virtualenv <que_es_virtualenv>`, si 
    requiere hacer la instalación en un entorno virtual Python.

-   Los paquetes :ref:`distribute <que_es_distribute>` / :ref:`setuptools <que_es_setuptools>`.

-   Disponer al menos **13 GB de espacio libre** para los :term:`paquetes Egg`.

-   Disponer de un servidor Web como Apache2 o Nginx para hacer publico su 
    repositorio.

-   Habilidad de ejecutar un script vía tarea de :command:`crontab` en el servidor.
  
Dependencias
------------

Para los diversos casos de instalación es recomendable que instale ciertas 
dependencias en su sistema operativo como las que se muestran a continuación: 

.. code-block:: sh

  # aptitude install build-essential python-dev python-setuptools python-pip mercurial

Instalación
===========

Existen dos formas tradicionales de instalar el paquete:

.. _instalacion_asistida_buildout:

Asistida
--------

La instalación asistida, utiliza configuraciones :ref:`buildout <que_es_zcbuildout>`, 
para ayudarle en la instalación, la configuración de tu propio repositorio :term:`PyPI` 
de forma mas fácil y asistida debido a que automatiza las siguientes tareas por usted:
  
- Instalar el paquete :ref:`z3c.pypimirror <que_es_z3cpypimirror>` dentro de un 
  :ref:`virtualenv <que_es_virtualenv>`.
  
- Crear la estructura de directorio que contenga los paquetes a sincronizar.
  
- Definir las configuraciones del paquete por defecto.
  
- Genera un script para iniciar la sincronización de repositorio.
  
- Establecer una tarea programada que actualice el repositorio.

Para lograr esta instalación se debe ejecutar con los siguientes ­comando:

.. code-block:: sh

  $ git clone https://github.com/macagua/macagua.buildout.pypimirror.git
  $ virtualenv .
  $ source ./bin/activate
  $ python bootstrap.py
  $ ./bin/buildout -vvvN
  $ deactivate

Al finalizar estos comando debería tener los siguientes archivos:

:file:`buildout.cfg`
  Archivo de configuración :ref:`buildout <que_es_zcbuildout>` con todas las tareas 
  de construcción del repositorio espejo.

:file:`pypimirror.cfg`
  Archivo de configuraciones del paquete :ref:`z3c.pypimirror <que_es_z3cpypimirror>`.

:command:`bin/activate`
  Script de activación de la herramienta :ref:`virtualenv <que_es_virtualenv>`.

:command:`bin/buildout`
  Script :ref:`buildout <que_es_zcbuildout>`.

:command:`bin/pypimirror`
  Script de sincronización del paquete :ref:`z3c.pypimirror <que_es_z3cpypimirror>`.

:file:`packages`
  El directorio que contendrá los :term:`paquetes Egg` que sincronice en su repositorio espejo.

**Iniciar sincronización**

Lo primero que de hacer es iniciar la sincronización de su repositorio 
espejo, ejecutando el siguiente comando:

.. code-block:: sh

  $ ./bin/pypimirror --initial-fetch --follow-external-links --follow-external-index-pages --log-console ./pypimirror.cfg

Al finalizar estos comando debería tener los siguientes archivos:

:file:`pypimirror.log`
  Archivo log del paquete :ref:`z3c.pypimirror <que_es_z3cpypimirror>`.

:file:`packages/index.html`
  El índice de paquetes sincronizado generado dentro del directorio :file:`packages` 
  que a su ves contendrá todos los paquetes sincronizados en su repositorio espejo.

Luego de terminar la sincronización del repositorio, genera en el directorio 
:file:`packages` un archivo :file:`index.html` como índice del repositorio de software, 
puede consultarlo localmente en su navegador web de preferencia.

.. code-block:: sh

  $ firefox ./packages/index.html &

**Sincronizar repositorio**

Posteriormente una tarea programada con el programa :command:`crontab` realizara 
la sincronización del repositorio para mantener actualizado el repositorio con 
los nuevos paquetes disponibles, usted puede verificar la tarea definida, con 
el siguiente comando:

.. code-block:: sh

  $ crontab -l
  
.. _install_z3cpypimirror_egg:

Manual
------

Con la instalación manual del :ref:`paquete Egg <que_es_z3cpypimirror>`, usted 
requiere hacer manualmente las tareas descritas con la :ref:`configuración buildout <instalacion_asistida_buildout>`.
A continuación se muestra dos formas como puede instalar el paquete:

**Instalan con pip**

Puede instalar el :term:`paquetes Egg` de :ref:`z3c.pypimirror <que_es_z3cpypimirror>` 
con la herramienta :ref:`pip <que_es_pip>`, con el siguiente ­comando:

.. code-block:: sh

  # pip install z3c.pypimirror

**Instalando con easy_install**

Puede instalar el :term:`paquetes Egg` de :ref:`z3c.pypimirror <que_es_z3cpypimirror>` 
con la herramienta :ref:`easy_install <que_es_easyinstall>`, con el siguiente ­comando:

.. code-block:: sh

  # easy_install-2.4 z3c.pypimirror

**Configuración**

Después de ejecutar la instalación comando anterior, tenemos que configurar 
nuestro repositorio :term:`PyPI`, para eso hay crear un usuario en el sistema 
llamado ``pypimirror`` es un criterio, en el directorio **home** de usuario 
pypimirror, es en donde pretendo centralizar los paquetes, archivos de registros 
(.log) y entre otros... entonces cree una carpeta el nombre de paquetes con el 
siguiente comando:

.. code-block:: sh

  # mkdir -p /home/pypimirror/paquetes
  

Este será el directorio en donde iremos a mantener nuestros paquetes procedentes 
de :term:`PyPI`, los archivos de registros (\*.log) y temporales podemos mantenerlos 
en el directorio :file:`/home/pypimirror`, ahora tenemos que crear el fichero de 
configuración, lo llamé :file:`pypimirror.cfg`, tendrá la siguiente configuración:

.. code-block:: ini

  [DEFAULT]
  # the root folder of all mirrored packages.
  # if necessary it will be created for you
  mirror_file_path = /home/pypimirror/paquetes
  
  # where's your mirror on the net?
  base_url = http://pypi.sudominio.com
  
  # lock file to avoid duplicate runs of the mirror script
  lock_file_name = /home/pypimirror/pypi-poll-access.lock
  
  # Pattern for package files, only those matching will be mirrored
  filename_matches =
      *.zip
      *.tgz
      *.egg
      *.tar.gz
      *.tar.bz2
  
  # Pattern for package names; only packages having matching names will
  # be mirrored
  package_matches =
  #   zope.*
  #   plone.*
  #   Products.*
  #   collective.*
     *.*
  
  # remove packages not on pypi (or externals) anymore
  cleanup = True
  
  # create index.html files
  create_indexes = True
  
  # be more verbose
  verbose = True
  
  # resolve download_url links on pypi which point to files and download
  # the files from there (if they match filename_matches).
  # The filename and filesize (from the download header) are used
  # to find out if the file is already on the mirror. Not all servers
  # support the content-length header, so be prepared to download
  # a lot of data on each mirror update.
  # This is highly experimental and shouldn't be used right now.
  #
  # NOTE: This option should only be set to True if package_matches is not
  # set to '*' - otherwise you will mirror a huge amount of data. BE CAREFUL
  # using this option!!!
  external_links = False
  
  # similar to 'external_links' but also follows an index page if no
  # download links are available on the referenced download_url page
  # of a given package.
  #
  # NOTE: This option should only be set to True if package_matches is not
  # set to '*' - otherwise you will mirror a huge amount of data. BE CAREFUL
  # using this option!!!
  follow_external_index_pages = False
  
  # logfile
  log_filename = /home/pypimirror/pypimirror.log
  

Esta configuración, es una copia del archivo :file:`pypimirror.cfg.sample`
localizado por ejemplo en la ruta ``$PYTHON/site-packages/z3c.pypimirror-1.0.14-py2.4.egg/z3c/pypimirror``, 
un detalle importante durante la configuración es que en la variable
**package_matches**, se indique para descargar los espacios de nombre de
paquetes **zope**, **plone**, **Products** y **collective**, de siendo así
mismo el propio paquete :ref:`z3c.pypimirror <que_es_z3cpypimirror>` lo 
cual de esta forma estaría siendo descartado, a sí que para conseguir 
cualquier paquete desde :term:`PyPI`, usted puede comentar las lineas y 
decir como se muestra a continuación:

.. code-block:: cfg

    package_matches =
    #   zope.*
    #   plone.*
    #   Products.*
    #   collective.*
       *.*

**Iniciar sincronización**

Ahora que tenemos nuestro repositorio :term:`PyPI` debidamente configurado, para
iniciar la replicación del repositorio de :term:`PyPI`, ejecute el siguiente comando:

.. code-block:: sh

  $ /usr/bin/pypimirror --initial-fetch --follow-external-links --follow-external-index-pages /home/pypimirror/pypimirror.cfg

Puedes supervisar los avances analizando el logfile de :ref:`z3c.pypimirror <que_es_z3cpypimirror>`:

.. code-block:: sh

  $ tail -f /home/pypimirror/pypimirror.log

Cabe resaltar que **NO** es necesario preocuparse en crear la página índice
como el archivo :file:`index.html`, para el servidor Web, porque en el archivo de
configuración anterior, le estamos indicado que este será creado
automáticamente **(create_indexes = True)**.

**Sincronizar repositorio**

Usted automatizar la sincronización de los paquetes adicionando una tarea en
el :command:`crontab` del sistema con la siguiente linea:

.. code-block:: sh

  $ crontab -e

y entonces agregue la siguiente linea:

.. code-block:: cfg

  */6 * * * * pypimirror /usr/bin/pypimirror --update-fetch --follow-external-links --follow-external-index-pages /home/pypimirror/pypimirror.cfg

Publicar repositorio
====================

Luego de haber replicado localmente su repositorio :term:`PyPI` en su servidor, 
usted debe configurar un virtual host en un servidor Web para publicar 
su repositorio previamente replicado.

Nginx Web Server
----------------

Opcionalmente si usted utiliza un `Nginx Web Server`_ debe crear un sitio
disponible, con el siguiente comando:

.. code-block:: sh

  # vim /etc/nginx/sites-available/pypimirror

y entonces agrega la siguiente configuración:

.. code-block:: cfg

  server {
            listen IP-ADDRESS;
            server_name MIDOMINIO.TLD/pypi;
            location /pypi {
                root /home/pypimirror/paquetes;
            }
  }

Realice un enlace simbólico desde el directorio de Nginx :file:`sites-available/` 
al directorio :file:`sites-enabled/`, para que su configuración previa este disponible:

.. code-block:: sh

  # ln -s /etc/nginx/sites-available/pypimirror /etc/nginx/sites-enabled/pypimirror

Para finalizar debe carga de la nueva configuración, con el siguiente comando:

.. code-block:: sh

  # /etc/init.d/nginx reload

Apache Web Server
-----------------

Mientras se sincroniza el repositorio, usted puede configurar su servidor
Web, por ejemplo, `Apache Web Server`_ debe crear un sitio disponible con el
siguiente comando:

.. code-block:: sh

  # vim /etc/apache2/sites-available/pypimirror


Debe indicarle en su directiva ``DocumentRoot``, que apunte hacia el
directorio directorio, y entonces agrega la siguiente configuración:

.. code-block:: cfg

  <VirtualHost IP-ADDRESS:80>
      ServerName MIDOMINIO.TLD
      CustomLog /home/pypimirror/pypimirror.log combined
      DocumentRoot /home/pypimirror/paquetes
  </VirtualHost>


Realice un enlace simbólico desde el directorio de Apache2 :file:`sites-available/` 
al directorio :file:`sites-enabled/`, para que su configuración previa este disponible:

.. code-block:: sh

  # ln -s /etc/apache2/sites-available/pypimirror /etc/apache2/sites-enabled/pypimirror


Luego debe habilitar esta configuración del sitio llamado ``pypimirror``, con el siguiente comando:

.. code-block:: sh

  # a2ensite pypimirror

Y por ultimo recargamos la configuración en el servicio de :command:`apache2`, con el
siguiente comando:

.. code-block:: sh

  # /etc/init.d/apache2 reload

Usando repositorio
==================

Posterior a su instalación / configuración ya puede usar el repositorio previamente 
instalado, para esto existen varias formas de utilizarlo según sea su caso como se 
describen a continuación:

Usando pip
----------

Si usted necesita usar la herramienta :ref:`pip <que_es_pip>` es posible 
especificar el servidor de donde usted desea bajar el paquete, con lo 
muestra el siguiente comando:

.. code-block:: sh

  pip install -i http://sudominio.com/pypi Sphinx


Usando easy_install
-------------------

Opcionalmente con la herramienta :ref:`easy_install <que_es_easyinstall>` 
del SetupTools usted puede especificar el servidor de donde usted desea bajar 
el paquete, con lo muestra el siguiente comando:

.. code-block:: sh

  easy_install -i http://sudominio.com/pypi Sphinx


Usando buildout
---------------

Después de que todo este hecho, usted solo necesita decir en su archivo de
configuraciones locales buildout :file:`~/.buildout/default.cfg` (si no esta creado 
créalo o edite un archivo) cual es la dirección HTTP del repositorio por 
defecto (el que previamente configuro) de donde debería buscar y descargase
los paquetes y coloque lo siguiente:

.. code-block:: cfg

  [buildout]
  index =  http://sudominio.com/pypi


Guarde los cambios y ahora de esta forma cada ves que se ejecuta buildout
busca inicialmente este repositorio ;-)


Descargar código
================

Puede descargar el código fuente este ejemplo de configuración, ejecute 
el siguiente ­comando:

.. code-block:: sh

  $ git clone https://github.com/macagua/macagua.buildout.pypimirror.git

Ver también
===========

-   `Buildout de z3c.pypimirror`_.

-   `The PyPI Replication Project`_.

-   `What to do when PyPI goes down`_.

-   `Plone en la Plataforma de Desarrollo de Software Libre de CENDITEL`_.


Referencias
===========

-   El articulo `Instalar y configurar su propio repositorio de PyP­I­`_ desde 
    la comunidad Plone Venezuela.

-   `Criando seu próprio repositório do Pypi`_.

-   `Repositorios de software para Linux`_.


Reconocimientos
===============

Agradecimientos `Cleber J Santos`_ de la empresa `Simples Consultoria`_ por
escribir inicialmente este tutorial en Portugués, y a los compañeros `Dhionel Diaz`_ 
y `Leonardo J. Caballero G.`_ de la `fundación CENDITEL`_, por traducir al Español 
y poner en practica :ref:`z3c.pypimirror <que_es_z3cpypimirror>` con el cual
crearon esta completa receta :D

.. _z3c.pypimirror: http://pypi.python.org/pypi/z3c.pypimirror
.. _Python: http://www.python.org/
.. _Apache Web Server: http://httpd.apache.org/
.. _Nginx Web Server: http://wiki.nginx.org/Main
.. _Cleber J Santos: http://twitter.com/cleberjsantos
.. _Simples Consultoria: http://www.simplesconsultoria.com.br/
.. _Dhionel Diaz: mailto:ddiaz@cenditel.gob.ve
.. _Leonardo J. Caballero G.: http://wiki.cenditel.gob.ve/wiki/lcaballero
.. _fundación CENDITEL: http://www.cenditel.gob.ve/
.. _Buildout de z3c.pypimirror: http://bluedynamics.com/articles/jens/setup-z3c.pypimirror
.. _The PyPI Replication Project: http://www.coactivate.org/projects/pypi-mirroring/project-home
.. _Plone en la Plataforma de Desarrollo de Software Libre de CENDITEL: http://plataforma.cenditel.gob.ve/wiki/Plone
.. _Criando seu próprio repositório do Pypi: http://www.simplesconsultoria.com.br/blog/criando-seu-proprio-repositorio-do-pypi-1
.. _Instalar y configurar su propio repositorio de PyP­I­: http://www.coactivate.org/projects/ploneve/instalar-y-configurar-su-propio-repositorio-de-pypi
.. _What to do when PyPI goes down: http://jacobian.org/writing/when-pypi-goes-down/
.. _Repositorios de software para Linux: http://www.comoinstalarlinux.com/repositorios-de-software-para-llinux/