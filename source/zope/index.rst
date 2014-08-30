.. -*- coding: utf-8 -*-

.. _zope_index:

===============================
Z Object Publishing Environment
===============================

.. figure:: images/zope-logo.png
  :width: 180px
  :alt: Logotipo de Zope
  :align: center

  Logotipo de Zope

Plone esta basado en el :ref:`servidor de aplicaciones Zope <servidor_aplicaciones_web_oao>` 
y este requiere realizar tareas de hospedaje y administrativa para un servidor de aplicación 
Zope / sitio de Plone.

Primeros pasos en Zope
======================

.. list-table::
   :header-rows: 1
   :class: index-table

   * - Introducción
     - Base de datos
     - Administradores
     - Referencia

   * - :ref:`Z Object Publishing Environment <que_es_zope>`

       :ref:`Beneficios <beneficios_zope>`

       :ref:`Infraestructura de servicios <infraestructura_servicios_zope>`

       :ref:`¿Quien usa Zope? <software_basado_zope>`

       :ref:`Instalación del servidor Zope <instalacion_zope>`

     - :ref:`Zope Object Database - ZODB <que_es_zodb>`

       :ref:`Puntos de montajes para la ZODB <puntos_montaje_zodb>`

       :ref:`Importar y exportar data ZODB <importar_exportar_data>`

       :ref:`Compactar la ZODB <compactar_zodb>`

       :ref:`Backup de la ZODB <backup_zodb>`

       :ref:`Actualizar el ZCatalog <actualizar_zcatalog>`

       :ref:`Reparación de ZODB <reparacion_zodb>`

     - :ref:`Zope Management Interface - ZMI <zmi>`

       :ref:`Configurar como demonio / servicio <configurar_zope_como_demonio>`

       :ref:`Configurar como servidor FTP <zope_como_ftp>`

       :ref:`Configurar como servidor WebDAV <zope_como_webdav>`

       :ref:`Configurar como servidor WSGI <zope_como_wsgi>`

     - :ref:`Comando de control de Zope <linea_comando_zope>`

       :ref:`Configuraciones generales <configuraciones_generales>`

       :ref:`Instancia de depuración <instancia_zope_debug>`

       :ref:`Ejecutando detrás de Servidor Web <zope_plone_webserver>`

       :ref:`Ejecutando con Servidor Apache <zope_plone_webserver_apache>`

       :ref:`Ejecutando con Servidor Nginx <zope_plone_webserver_nginx>`

Programación en Zope
====================

.. list-table::
   :header-rows: 1
   :class: index-table

   * - Desarrollo
     - Base de datos ZODB
     - Base de datos SQL

   * - :ref:`Arquitectura de Componentes de Zope <zca-es>`

       :ref:`El motor de búsqueda de Zope <herramienta_zcatalog>`

       :ref:`Zope Page Templates <zpt_lenguage>`

       :ref:`Flujos de trabajo <flujo_trabajo>`

     - :ref:`Zope Object Database - ZODB <que_es_zodb>`

       `Programación con la ZODB <http://atmantree.com/go/2013/07/breve-introduccion-a-zodb/>`_

       `Vida y obra de objetos persistidos en ZODB <http://revista.python.org.ar/4/es/html/zodb.html>`_

       `Using the ZODB <http://www.fprimex.com/coding/zodb.html>`_

     - `Relational Database Connectivity <http://docs.zope.org/zope2/zope2book/RelationalDatabases.html>`_

       `Understanding Zope Database Adaptaters <http://www.makina-corpus.org/blog/understanding-zope-database-adaptaters>`_

       `Z SQL Methods User's Guide <http://doc.dvgu.ru/www/zope/zsql/ZSQL.html>`_

       `Connecting to MySQL and Zope ZMySQLDA <http://www.eng.ox.ac.uk/Plone/developing-for-plone/connecting-to-mysql>`_

.. 
  .. toctree::
      :maxdepth: 2
  
      z_object_publishing_environment
      instalacion
      zmi/index
      interaccion_linea_comando
      configuraciones_generales
      configurar_como_demonio
      instancia_debug
      web/zope_plone_detras_servidor_web
      web/servidor_apache
      web/servidor_nginx
      ftp/index
      webdav/index
      wsgi/index
      zodb/index
      zodb/puntos_montaje_db
      zodb/importar_exportar_data
      zodb/compactar
      zodb/respaldar
      zodb/compactar
      zodb/actualizar_catalog
      zodb/reparar
