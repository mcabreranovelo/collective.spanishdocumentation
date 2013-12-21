.. -*- coding: utf-8 -*-

.. _zope_plone_webserver_nginx:

Ejecutando Zope y Plone con Servidor Web Nginx
==============================================

:Autor(es): Leonardo J. Caballero G.
:Correo(s): leonardocaballero@gmail.com
:Compatible con: Plone 3, Plone 4
:Fecha: 21 de Diciembre de 2013

Este documento busca explicar los conceptos intrínsecos para instalar y configurar 
un servidor Web `Nginx`_ en frente del servidor Zope/Plone, a través de técnicas de 
**reescritura URL**.

Acerca de Nginx
---------------

Según la documentación sobre `Nginx en Wikipedia Español`_ `'es un servidor web/proxy inverso 
ligero de alto rendimiento y un proxy para protocolos de correo electrónico (IMAP/POP3).'`.

Instalar y configurar Servidor Web Nginx
----------------------------------------

Para instalar debe iniciar sesión como usuario "root" ejecute el siguiente
comando:  

.. code-block:: sh

  # aptitude install nginx

Luego se debe agregar la configuración respectiva en Nginx con el siguiente
comando: 

.. code-block:: sh

  # vim /etc/nginx/nginx.conf

Y agregue la siguiente configuración: 

.. code-block:: cfg

    user www-data;
    worker_processes  1;

    error_log  /var/log/nginx/error.log;
    pid        /var/run/nginx.pid;

    events {
        worker_connections  1024;
    }

    http {
        include       /etc/nginx/mime.types;
        default_type  application/octet-stream;

        access_log      /var/log/nginx/access.log;

        sendfile        on;
        #tcp_nopush     on;

        #keepalive_timeout  0;
        keepalive_timeout  65;
        tcp_nodelay        on;

        #gzip  on;

        server_names_hash_bucket_size 64;

        server_name_in_redirect off;
        server_tokens           off;

        include /etc/nginx/conf.d/*.conf;
        include /etc/nginx/sites-enabled/*;
    }


Regla de Reescritura de URL para Zope
-------------------------------------

Y defina la política de virtual host del sitio, con el siguiente comando: 

.. code-block:: sh

  # vim /etc/nginx/sites-available/cliente1-intranet

Agregue la siguiente configuración: 

.. code-block:: cfg

    server {
        # DNS/IP y Puerto en que escucha la aplicación
        listen   *:80;

        # Nombre del servidor
        server_name  intranet.cliente1.com;

        # Tamaño máximo de subida de archivos
        client_max_body_size 24M;

        # Tamaño máximo de buffer de archivos
        client_body_buffer_size 128K;

        # Archivo de registro de acceso del sitio web
        access_log  /var/log/nginx/cliente1-intranet.access.log;

        # Archivo de registro de error del sitio web
        error_log  /var/log/nginx/cliente1-intranet.error.log error;

        # Interfaz Administrativa de Zope
        location /manage {
                proxy_pass       http://127.0.0.1:8080/VirtualHostBase/http/intranet.cliente1.com:80/manage_main/VirtualHostRoot/;
                proxy_set_header Host $host;
            }

        # Intranet del cliente1
        location / {
                proxy_pass       http://127.0.0.1:8080/VirtualHostBase/http/intranet.cliente1.com:80/cliente1_intranet/VirtualHostRoot/;
                proxy_set_header Host $host;
        }

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
                root   /var/www/nginx-default;
        }

    }


Realice un enlace simbólico desde el directorio de Nginx :file:`sites-available/`
al directorio :file:`sites-enabled/`, para que su configuración previa este
disponible: 

.. code-block:: sh

  # ln -s /etc/nginx/sites-available/cliente1-intranet /etc/nginx/sites-enabled/cliente1-intranet


Reinicie el servidor Web
------------------------

Luego reinicie su servidor Nginx con el siguiente comando: 

.. code-block:: sh

  # /etc/init.d/nginx reload

.. seealso:: Los artículos sobre :ref:`Ejecutando Zope y Plone detrás de un Servidor Web <zope_plone_webserver>` y `Mapping the Virtual Host`_.

Referencias
===========

-   `Integración de Plone con el Servidor Web Nginx de la fundación CENDITEL`_.

-   `Definir Virtual Host y Reescritura de Servidor Web`_. 

.. _Nginx: http://wiki.nginx.org/NginxEs
.. _Nginx en Wikipedia Español: http://es.wikipedia.org/wiki/Nginx
.. _Mapping the Virtual Host: http://www.insmallsteps.com/lessons/lesson-hosting-install/mapping-the-virtual-host
.. _Integración de Plone con el Servidor Web Nginx de la fundación CENDITEL: http://plataforma.cenditel.gob.ve/wiki/Plone%3APloneVHostWebServer
.. _Definir Virtual Host y Reescritura de Servidor Web: http://wiki.canaima.softwarelibre.gob.ve/wiki/Definir_Virtual_Host_y_Reescritura_de_Servidor_Web