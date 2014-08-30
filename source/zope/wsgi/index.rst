.. -*- coding: utf-8 -*-

.. _zope_como_wsgi:

=====================================
Configurar Zope como un servidor WSGI
=====================================

.. sidebar:: Sobre este artículo

    :Autor(es): Leonardo J. Caballero G.
    :Correo(s): leonardocaballero@gmail.com
    :Compatible con: Plone 3, Plone 4
    :Fecha: 30 de Agosto de 2014

Descripción general
===================

**WSGI**, significa en Ingles **Web Server Gateway Interface**, es decir, 
Interfaz de entrada de servidor Web. Esta una especificación para simple 
y universal de interfaz entre los servidores web y aplicaciones web o 
frameworks para el lenguaje de programación Python. EL WSGI sido adoptado 
como un estándar para el desarrollo de aplicaciones web de Python.

Zope tiene la posibilidad de ejecutarse con WSGI, usted solo necesita configurarlo.

El caso mas apropiado para desplegar Zope con WSGI es el siguiente:

* Una configuración ZEO con sus respectivos clientes ZEO.

* Gunicorn como servidor Web para aplicaciones WSGI.

* Supervisor para orquestar el arranque y supervisión de los procesos del despliegue.

Requerimientos
==============

Estos son los requerimientos mínimos de instalación: ::

  # aptitude install gcc g++ make tar unzip bzip2 libssl-dev libxml2-dev \
  libxslt1-dev zlib1g-dev libjpeg62-dev libreadline6-dev readline-common \
  wv xpdf-utils python2.7-dev python-pip git-core
  # pip install virtualenv==1.9.1 ; exit

Descargue configuración WSGI
============================

Para esta guía usaremos la configuración para Plone 4 desde el siguiente
repositorio: ::

  $ git clone https://github.com/Covantec/buildout.plone.wsgi.git

Crear entorno virtual
=====================

Para la inicialización del proyecto Buildout, ejecute el siguiente comando: ::

  $ cd ./buildout.plone.wsgi
  $ virtualenv --no-setuptools python2.7
  $ source ./python2.7/bin/activate

.. tip:: 

    * Si es una instalación de Plone 3.x o inferior debe crear el entorno virtual
      con la versión Python 2.4.x.

    * Si es una instalación de Plone entre las versiones 4.0 y 4.2 debe crear el
      entorno virtual con la versión Python 2.4.x.

Inicialización del proyecto
===========================

Para la inicialización del proyecto Buildout, ejecute el siguiente comando: ::

  (python2.7)$ python bootstrap.py

Construcción del proyecto
=========================

Para la construcción del proyecto Buildout, ejecute el siguiente comando: ::

  ./bin/buildout

Iniciar procesos
================

Para iniciar Zope con WSGI lo realiza mediante supervisor, ejecute el siguiente comando: ::

  ./bin/supervisord

Puede acceder a la interfaz administrativa de supervisor en la siguiente dirección http://127.0.0.1:9001/

Para iniciar la instancia Zope, ejecute el siguiente comando: ::

  ./bin/plone start

Puede acceder a la ZMI para crear su sitio Plone en la siguiente dirección http://127.0.0.1:8000/manage

Para detener algún proceso en supervisor, ejecute el siguiente comando: ::

  ./bin/supervisorctl -i
  gunicorn                         RUNNING    pid 28138, uptime 0:00:01
  zeo                              RUNNING    pid 28139, uptime 0:00:01
  supervisor>

Para detener todos los procesos, ejecute el siguiente comando: ::

  supervisor> stop all
  gunicorn: stopped
  zeo: stopped
  supervisor>

Para salir del shell interactivo de supervisor, ejecute el siguiente comando: ::

  supervisor> exit

Para detener la instancia Zope, ejecute el siguiente comando: ::

  ./bin/plone stop

Descarga código fuente
======================

Para descargar el código fuente de este ejemplo ejecute el siguiente comando:

.. code-block:: sh

  $ git clone https://github.com/Covantec/buildout.plone.wsgi.git

Referencias
===========

- `Authoring Content with WebDAV and FTP`_.

- `Managing Zope Objects Using External Tools`_.

.. _Authoring Content with WebDAV and FTP: http://www.zope.org/Documentation/Articles/WebDAV%20
.. _Managing Zope Objects Using External Tools: http://www.zope.org/Documentation/Books/ZopeBook/2_6Edition/ExternalTools.stx
