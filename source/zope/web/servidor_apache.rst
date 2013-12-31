.. -*- coding: utf-8 -*-

.. _zope_plone_webserver_apache:

Ejecutando Zope y Plone con Servidor Web Apache
===============================================

.. sidebar:: Sobre este artículo

    :Autor(es): Leonardo J. Caballero G.
    :Correo(s): leonardocaballero@gmail.com
    :Compatible con: Plone 3, Plone 4
    :Fecha: 31 de Diciembre de 2013

Este documento busca explicar los conceptos intrínsecos para instalar y configurar 
un servidor Web `Apache 2`_ en frente del servidor Zope/Plone, a través de técnicas de 
**reescritura URL**.

Acerca de Servidor HTTP Apache
------------------------------
Según la documentación sobre `Servidor HTTP Apache`_ en Wikipedia Español `'es un servidor 
web HTTP de código abierto, para plataformas Unix (BSD, GNU/Linux, etc.), Microsoft Windows, 
Macintosh y otras, que implementa el protocolo HTTP/1.1 y la noción de sitio virtual'`.


Terminología en Apache
----------------------

Hay que entender varios conceptos sobre el servidor Web Apache antes de continuar:

.. glossary::

  Módulos Apache 2
    Una lista de todos los módulos de Apache 2.2 con sus opciones.

    .. tip:: Más información consulte la referencia de `módulos Apache 2`_.

  Como reescribir dirección URL
    Un buen sobre la técnica de reescritura de direcciones URL con las reglas de reescritura.

    .. tip:: Más información consulte la referencia de `rewrite`_.

  Referencias de módulo mod_proxy
    La referencias oficial desde la documentación de Apache 2.2.

    .. tip:: Más información consulte la referencia de `mod_proxy`_.

  Referencias de módulo mod_ssl
    Cifrado SSL con apache 2.

    .. tip:: Más información consulte la referencia de `mod_ssl`_.


Instalar y configurar Servidor Web Apache
-----------------------------------------

Para instalar debe iniciar sesión como usuario "root" ejecute el siguiente
comando: 

.. code-block:: sh

  # aptitude install apache2


Habilitar módulos de mod_rewrite y mod_proxy
--------------------------------------------

Próximo paso es habilitar ``mod_proxy`` y ``mod_rewrite``.

- Módulo `mod_rewrite`_: es usado como un motor de reescritura
  basado en reglas para reescribir direcciones URL solicitadas en tiempo de
  ejecución, es decir le permite a usted apuntar a una dirección URL en
  otra dirección URL. Para habilitar ese módulo debe ejecutar el siguiente comando:

  .. code-block:: sh

    # a2enmod proxy
    Enabling module proxy.
    Run '/etc/init.d/apache2 restart' to activate new configuration!

- Módulo `mod_proxy`_: es un `Proxy inverso`_ que le permite apuntar
  a una dirección URL en otro servidor en otro puerto. Este sirve como un
  traductor, para que el usuario nunca se comunique con cualquier otro
  servicio que use otro puerto que no sea el 80, es decir es un
  intermediario transparente hacia otro sitio. Con este módulo los usuarios
  pueden ir de Plone hacia una aplicación PHP, y luego a una aplicación
  Java y nunca saberlo. Para habilitar ese módulo debe ejecutar el siguiente comando: 

  .. code-block:: sh

    # a2enmod rewrite
    Enabling module rewrite.
    Run '/etc/init.d/apache2 restart' to activate new configuration!

Luego puede editar la configuración del módulo ``mod_proxy``, con el
siguiente comando: 

.. code-block:: sh

  # vim /etc/apache2/mods-enabled/proxy.conf


Ahora, encontramos los siguientes ajustes y coinciden con lo que tengo aquí.
Siga exactamente esto, o usted podría terminar con teniendo un proxy abierto
que permite a otros rebote a través de su máquina para llegar a cualquier
lugar que desee de forma anónima, enviar spam, etc. Hagas lo que hagas, nunca
active su ``ProxyRequests On``. 

.. code-block:: cfg

    ProxyRequests Off
    ProxyPreserveHost On
    <Proxy *>
         Order deny,allow
         #Deny from all
         Allow from all
    </Proxy>

Regla de Re-escritura de Zope
-----------------------------

Y defina la política de virtual host del sitio, con el siguiente comando: 

.. code-block:: sh

  # vim /etc/apache2/sites-available/cliente1-intranet

Agregue la siguiente configuración: 

.. code-block:: cfg

    <VirtualHost *:80>
      ServerName    www.cliente1.com
      ServerAlias   intranet.cliente1.com
      ServerAdmin   webmaster@intranet.cliente1.com
      ServerSignature On

      CustomLog     /var/log/apache2/cliente1-intranet-access.log combined
      ErrorLog      /var/log/apache2/cliente1-intranet-error.log
      LogLevel warn

      # registro del rebajar la tasa de compresión a un archivo
      #CustomLog /var/log/apache2/deflate_log deflate

      <IfModule mod_rewrite.c>
        RewriteEngine On

        # uso RewriteLog para la depuración de problemas con sus reglas de reescritura 
        # debe desactivar después de encontrar el error, ya que el disco duro se llenaría *muy rápido*
        # RewriteLog "/var/log/apache2/rewrite_log"
        # RewriteLogLevel 2

        # sirviendo los iconos desde el servidor Apache 2
        RewriteRule ^/icons/ - [L]

        # reescribir cualquier acceso al ZMI en un servidor seguro
        # RewriteRule ^/(.*)/manage(.*) \
        # https://secure.cliente1.com/Zope/cliente1_instance/cliente1_com/$1/manage$2 [NC,R=301,L]
        # RewriteRule ^/manage(.*) \
        # https://secure.cliente1.com/Zope/cliente1_instance/cliente1_com/manage$1  [NC,R=301,L]


       # reescribir cualquier otro acceso al servidor Zope usando un proxy [P] 
       # y añadir las palabras claves mágicas del VMH. 
       # usar la variable de servidor %{SERVER_NAME} en lugar de cliente1.com 
       # para evitar que se desborde la directiva ServerAlias​​, 
       # usar la variable de servidor %{HTTP_HOST} no es recomendable ya que puede contener el puerto

       RewriteRule ^/manage/(.*) \
           http://127.0.0.1:8080/VirtualHostBase/http/%{SERVER_NAME}:80/manage_main/VirtualHostRoot/$1 [L,P]

       RewriteRule ^/(.*) \
           http://127.0.0.1:8080/VirtualHostBase/http/%{SERVER_NAME}:80/cliente1_intranet/VirtualHostRoot/$1 [L,P]

      </IfModule>

      <IfModule mod_proxy.c>
        ProxyVia On

        # evitar que el servidor web sea utilizado como proxy
        <LocationMatch "^[^/]">
          Deny from all
        </LocationMatch>
      </IfModule>

      # almacenamiento en caché (inhabilitado)
      # esto cacheará todos los archivos con la información correcta de caché a partir /
      <IfModule mod_mem_cache.c>
      # CacheEnable mem /
      </IfModule>

      # compresión (inhabilitado)
      <IfModule mod_deflate.c>
       SetOutputFilter DEFLATE
      </IfModule>
    </VirtualHost>


Realice un enlace simbólico desde el directorio de Apache 2.2 :file:`sites-available/` 
al directorio :file:`sites-enabled/`, para que su configuración previa este disponible 

.. code-block:: sh

  # ln -s /etc/apache2/sites-available/cliente1-intranet /etc/apache2/sites-enabled/cliente1-intranet


Reinicie el servidor
--------------------

Luego reinicie su servidor Apache con el siguiente comando: 

.. code-block:: sh

  # /etc/init.d/apache2 reload


Otras configuraciones
---------------------

A continuación, algunas configuraciones muy características:


Plone como un domino completo
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Tener un nombre de host completo (es decir, todo bajo "/") que es servido por
un único sitio Plone, añade esto a su configuración de VirtualHost de Apache
la siguiente configuración: 

.. code-block:: sh

  RewriteEngine On
  RewriteRule ^/(.*)$
    http://127.0.0.1:8080/VirtualHostBase/http/%{SERVER_NAME}:80/cliente1_intranet/VirtualHostRoot/$1 [L,P]

Plone como una porción de su sitio
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Alternativamente, usted podría mapear su sitio Plone dentro de un sub-
directorio de un sitio existente sin subsumirlo como todo el sitio. ¿Para
hacer esto hay es usar una regla de reescritura ligeramente diferente?. En
primer lugar, lo mejor es crear un sitio Plone con un ID que coincida con el
nombre de directorio en el que desea que el sitio este publicado. Por
ejemplo, si desea que la dirección URL de su sitio Plone sea así: ::

  http://cliente1.com/cliente1_intranet

Entonces debería crear su sitio Plone con el identificador **cliente1_intranet**. 
Para aparejar eso a este sitio que se muestra cuando usted navega a la dirección 
`http://cliente1.com/cliente1_intranet`_, debe especificar la reescritura de 
la siguiente forma: 

.. code-block:: sh

  RewriteEngine On
  RewriteRule ^/cliente1_intranet($|/.*) http://127.0.0.1:8080/VirtualHostBase/http/%{SERVER_NAME}:80/VirtualHostRoot/cliente1_intranet$1 [L,P]

Soporte HTTPS
~~~~~~~~~~~~~

Si usted quiere soportar acceso seguro HTTPS a su sitio Plone, es algo
parecida la regla de reescritura anterior para su VirtualHost. Cambie ``http``
a ``https`` y cambiar los números de puerto de "80" a "443", de esta forma: 

.. code-block:: sh

  RewriteRule ^/(.*)$ \
   http://127.0.0.1:8080/VirtualHostBase/https/%{SERVER_NAME}:443/VirtualHostRoot/$1 [L,P]

.. tip:: Más información http://plone.org/documentation/kb/apache-ssl

Reglas más elegantes
~~~~~~~~~~~~~~~~~~~~

Si usted tiene necesidades mas exóticas, tome un tiempo y lea la página de
`Virtual Host Monster`_, y considere tener a la mano el `RewriteRule Witch`_,
el cual es un generador de directivas RewriteRule de Apache para Virtual Host
en Zope.

Recomendaciones
~~~~~~~~~~~~~~~

- Si tienes problemas raros con sus reglas, es recomendado activar el
  `RewriteLog`_ y alzar el `RewriteLogLevel`_ a tu conveniencia, consulte
  la documentación de `Mod_rewrite`_.


Suprimiendo virtual host monster
================================

En el caso de que usted ha establecido reglas de virtual hosting de modo 
que ya no se Zope le permiten acceder a la interfaz de gestión, puede agregar
``_SUPPRESS_ACCESSRULE"`` a la dirección URL para desactivar `VirtualHostMonster`_.

.. seealso:: 
  
  -   :ref:`Ejecutando Zope y Plone detrás de un Servidor Web <zope_plone_webserver>`.
  -   `Running Plone and Zope behind an Apache 2 web server`_.
  -   `Mapping the Virtual Host`_.

Referencias
===========

-   `Definir Virtual Host y Reescritura de Servidor Web`_. 

-   `Proxy Apache a Zope`_.

-   `How VHM works`_.

.. _Apache 2: http://httpd.apache.org/
.. _módulos Apache 2: http://httpd.apache.org/docs/2.2/es/mod/
.. _mod_rewrite: http://httpd.apache.org/docs/2.2/mod/mod_rewrite.html
.. _rewrite: http://httpd.apache.org/docs-2.0/misc/rewriteguide.html
.. _mod_proxy: http://httpd.apache.org/docs/2.2/mod/mod_proxy.html
.. _mod_ssl: http://httpd.apache.org/docs/2.2/mod/mod_ssl.html
.. _Proxy inverso: http://es.wikipedia.org/wiki/Proxy#Reverse_Proxy_.2F_Proxy_inverso
.. _Servidor HTTP Apache: http://es.wikipedia.org/wiki/Servidor_HTTP_Apache
.. _http://cliente1.com/cliente1_intranet: http://cliente1.com/cliente1_intranet
.. _Virtual Host Monster: https://weblion.psu.edu/trac/weblion/wiki/VirtualHostMonster
.. _VirtualHostMonster: https://weblion.psu.edu/trac/weblion/wiki/VirtualHostMonster
.. _RewriteRule Witch: http://betabug.ch/zope/witch
.. _RewriteLog: http://httpd.apache.org/docs/2.2/mod/mod_rewrite.html#rewritelog
.. _RewriteLogLevel: http://httpd.apache.org/docs/2.2/mod/mod_rewrite.html#rewriteloglevel
.. _Running Plone and Zope behind an Apache 2 web server: http://plone.org/documentation/kb/plone-apache/tutorial-all-pages
.. _Mapping the Virtual Host: http://www.insmallsteps.com/lessons/lesson-hosting-install/mapping-the-virtual-host
.. _Definir Virtual Host y Reescritura de Servidor Web: http://wiki.canaima.softwarelibre.gob.ve/wiki/Definir_Virtual_Host_y_Reescritura_de_Servidor_Web
.. _Proxy Apache a Zope: https://weblion.psu.edu/trac/weblion/wiki/ProxyApacheToZope
.. _How VHM works: http://plone.org/documentation/kb/plone-apache/vhm
.. _https://plone.dcri.duke.edu/info/faq/vhm: https://plone.dcri.duke.edu/info/faq/vhm