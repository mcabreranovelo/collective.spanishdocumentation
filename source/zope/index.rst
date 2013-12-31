.. -*- coding: utf-8 -*-

.. _zope_index:

===============================
Z Object Publishing Environment
===============================

Plone esta basado en el :ref:`servidor de aplicaciones Zope <servidor_aplicaciones_web_oao>` 
y este requiere realizar tareas de hospedaje y administrativa para un servidor de aplicación 
Zope / sitio de Plone.

.. figure:: images/zope-logo.png
  :width: 180px
  :alt: Logotipo de Zope
  :align: center

  Logotipo de Zope

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

     - :ref:`Zope Object Database - ZODB <que_es_zodb>`

       :ref:`Puntos de montajes para la ZODB <puntos_montaje_zodb>`

       :ref:`Compactar la ZODB <compactar_zodb>`

       :ref:`Importar y exportar data ZODB <importar_exportar_data>`

     - :ref:`Zope Management Interface - ZMI <zmi>`

       :ref:`Configurar como demonio / servicio <configurar_zope_como_demonio>`

       :ref:`Configurar como servidor FTP <zope_como_ftp>`

       :ref:`Configurar como servidor WebDAV <zope_como_webdav>`

       :ref:`Ejecutando detrás de Servidor Web <zope_plone_webserver>`

     - :ref:`Comando de control de Zope <linea_comando_zope>`

       :ref:`Configuraciones generales <configuraciones_generales>`

       :ref:`Ejecutando con Servidor Apache <zope_plone_webserver_apache>`

       :ref:`Ejecutando con Servidor Nginx <zope_plone_webserver_nginx>`

       :ref:`Instancia de depuración <instancia_zope_debug>`

.. 
  .. toctree::
      :maxdepth: 2
  
      z_object_publishing_environment
      zmi/index
      interaccion_linea_comando
      configuraciones_generales
      configurar_como_demonio
      ftp/index
      webdav/index
      instancia_debug
      web/zope_plone_detras_servidor_web
      web/servidor_apache
      web/servidor_nginx
      zodb/index
      zodb/compactar
      zodb/puntos_montaje_db
      zodb/importar_exportar_data