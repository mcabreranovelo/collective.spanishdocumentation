.. -*- coding: utf-8 -*-

.. _zope_plone_webserver:

=================================================
Ejecutando Zope y Plone detrás de un Servidor Web
=================================================

.. sidebar:: Sobre este artículo

    :Autor(es): Leonardo J. Caballero G.
    :Correo(s): leonardocaballero@gmail.com
    :Compatible con: Plone 3, Plone 4
    :Fecha: 30 de Agosto de 2014

Este documento busca explicar los conceptos intrínsecos para instalar y configurar 
un servidor Web en frente del servidor Zope/Plone.

¿Por que detrás de un Servidor Web?
===================================

Cuando se configura el servidor Zope y Plone detrás de un servidor Web generalmente 
se hace como **servidor proxy reverso** y existentes varias razones para este tipo 
de configuración:

* **Seguridad**: el servidor proxy es una capa adicional de defensa y por lo tanto 
  protege los servidores web. Para el servidor Zope permite enmascarar el puerto de 
  publicación del mismo, a través del patrón de diseño "Front-controler" que permite 
  aplicar nuevos direccionamientos a todas las peticiones del puerto 80 aplicando 
  reglas de reescritura de direcciones URLs.

* **Configurar un firewall en su servidor Web**, esta configuración tiene la finalidad 
  es reforzar la seguridad de aplicaciones Web.

* **Cifrado / Aceleración SSL**, cuando se crea un sitio web seguro, habitualmente el 
  cifrado SSL no lo hace el mismo servidor web, sino que es realizado por el "proxy reverso", 
  el cual está equipado con un hardware de aceleración SSL (Security Sockets Layer).

* **Distribución de Carga**, con el "proxy reverso" puede distribuir la carga entre 
  varios servidores web. En ese caso, el "proxy reverso" puede necesitar reescribir 
  las direcciones URLs de cada página web (traducción de la dirección URL externa a la 
  dirección URL interna correspondiente, según en qué servidor se encuentre la información 
  solicitada).

* **Caché de contenido estático**, con un "proxy reverso" puede descargar los servidores 
  web almacenando contenido estático como imágenes u otro contenido gráfico.


Servicio de Virtual hosting en Zope
===================================
El servidor Zope viene con un objeto llamado `Virtual Host Monster`_ que le ayuda a hacer 
configuraciones de hosting virtual. La técnica de hosting virtual es una forma de servir 
a muchos sitios web con un servidor Zope.

.. _zope_plone_webserver_terminologia_general:

Terminología general
--------------------

Hay que entender varios conceptos antes de continuar:

.. glossary::

  vhost
    Es una nomenclatura del Ingles "Hosting Virtual" que hace referencia del Hosting Virtual.

  Hosting Virtual
    Según la documentación sobre `Hosting Virtual`_ en Apache Versión 2.0 `'El término Hosting 
    Virtual se refiere a hacer funcionar más de un sitio web (tales como www.company1.com y 
    www.company2.com) en una sola máquina. Los sitios web virtuales pueden estar "basados en 
    direcciones IP", lo que significa que cada sitio web tiene una dirección IP diferente, o 
    "basados en nombres diferentes", lo que significa que con una sola dirección IP están 
    funcionando sitios web con diferentes nombres (de dominio). El hecho de que estén funcionando 
    en la misma máquina física pasa completamente desapercibido para el usuario que visita esos 
    sitios web'`.

  VHM
    Es una nomenclatura del Ingles `Virtual Host Monster`_ que hace referencia al objeto 
    encargado de Hosting Virtual del servidor Zope.

  Virtual Host Monster
    Según la documentación sobre `VirtualHostMonster`_ en la Wiki de Zope2 `'Es un objeto, 
    usualmente encontrado en la carpeta raíz de la instancia de Zope, el cual hace trabajar 
    a los hosts virtual'`.

  Proxy inverso
    Según la documentación sobre Proxy en su sección Reverse Proxy/`Proxy inverso`_ en 
    Wikipedia Español `'Un reverse proxy es un servidor proxy instalado en el domicilio 
    de uno o más servidores web. Todo el tráfico entrante de Internet y con el destino de 
    uno de esos servidores web pasa a través del servidor proxy'`.

  Reescritura de URL
    Según la documentación sobre `URL rewriting`_ (Rewrite engine) en Wikipedia Ingles 
    `'La reescritura de direcciones URL (a veces conocida como dirección URL de adornadas, 
    cortas o amigable a los motores de buscadores) le permite modificar la apariencia de 
    las dirección URL Web, para esto usa un motor de reescritura de URL, por lo generar 
    incorporado en un Servidor Web. Esta técnica es usada para proveer enlaces web cortos 
    y de mayor entendimiento y relevancia a páginas Web. La técnica añade un grado de 
    separación entre los archivos que se utilizan para generar una página web y la dirección 
    URL que se presenta al mundo.'`.

  Servidores Web
    Según la documentación sobre `Servidor web`_ en Wikipedia Español `'es un programa informático 
    que procesa una aplicación del lado del servidor realizando conexiones bidireccionales 
    y/o unidireccionales y síncronas o asíncronas con el cliente generando o cediendo una 
    respuesta en cualquier lenguaje o Aplicación del lado del cliente. El código recibido 
    por el cliente suele ser compilado y ejecutado por un navegador web. Para la transmisión 
    de todos estos datos suele utilizarse algún protocolo. Generalmente se utiliza el protocolo 
    HTTP para estas comunicaciones, perteneciente a la capa de aplicación del modelo OSI. 
    El término también se emplea para referirse al ordenador que ejecuta el programa.'`.


¿Como trabaja Virtual Host Monster?
-----------------------------------

EL objeto `Virtual Host Monster`_ enmascara la dirección URL devuelta por el servidor Zope como 
response la cual es publicada como **http://www.cliente1.com/** en lugar de **http://127.0.0.1:8080/**. 
Está instalado previamente en el servidor Zope (este objeto se llama ``virtual_hosting`` y se encuentra
en el directorio del raíz del servidor Zope y puede ser consultado desde la interfaz administrativa de 
Zope) y no necesita ninguna configuración en Zope. 

Su configuración sólo se produce a través de una regla de reescritura de la dirección URL, adicionalmente 
se debe configurar su servidor web como un proxy inverso hacia el servidor Zope. 

La regla de reescritura de la dirección URL de VHM luce algo así: ::

    ^/(.*) \ 
    http://127.0.0.1:8080/VirtualHostBase/http/intranet.cliente1.com:80/\
    cliente1_intranet/VirtualHostRoot/$1

Esta dirección URL de VHM previa tiene siete partes:

.. glossary::

  ^/(.*) \ 
    ¿Qué significa eso? Bueno, esto es una `expresión regular`_, que coincide con casi todo. Voy a explicarlo con calma:

    * El carácter ``^`` significa empezar por el principio, el principio es donde está justo después del nombre de dominio
      (por ejemplo, después de **http://www.cliente1.com**).

    * El carácter ``/`` significa que coincida con el primer ``/`` que venga (después del nombre de dominio, por ejemplo,
      **http://www.cliente1.com/**).

    * El carácter ``(`` significa recordar todo lo que allá coincidido entre este carácter y ``)`` y lo llaman como \$1

    * El carácter ``.`` significa que coincida con cualquier carácter simple que no sea un espacio en blanco (espacios o
      tabulaciones).

    * El carácter ``*`` significa en realidad el operador de la izquierda puede ser igualado a 0 o más veces - en otras
      palabras, coinciden con el texto continuo hasta llegar a una línea final o espacio en blanco.

    * El carácter ``\`` significa salto de linea en la configuración del servidor Web y se utiliza para hacer las configuraciones
      del servidor Web más legibles por humanos.

    En pocas palabras ``^/(.*)`` significa **Coincidir todo lo que empieza con un ``/`` y guardar todos los caracteres
    después del carácter ``/``,** esto luego es procesado por la variable \$1 que mas adelante se explica que función cumple.

  http://127.0.0.1:8080
    Esto es para el aplicar el proxy reverso en su servidor Web. Esto configura a cual servidor debería acceder, además incluir
    el protocolo, host y puerto. En este ejemplo el proxy reverso accede al servidor Zope en el puerto 8080 en el mismo host
    usando el protocolo http. En Apache 2.2 se hace con el módulo `mod_proxy`_ y Nginx con su configuración **por defecto**.

  VirtualHostBase
    Esta es la palabra clave mágica para iniciar el hosting virtual. ¡Usted no debe agregar un objeto llamado ``VirtualHostBase``
    en el directorio raíz de su Zope!

  http
    Es el primer segmento de ruta después del ``VirtualHostBase`` define el protocolo del la dirección URL del vhost.

  intranet.cliente1.com:80
    Es el segundo elemento después del ``VirtualHostBase`` y define el servidor y el puerto. Junto con el protocolo es la parte base
    de la dirección URL, en este ejemplo **http://intranet.cliente1.com:80**. Como el ``VirtualHostBase`` el protocolo y servidor no
    son objetos reales. Ellos son solo colocados dentro de la dirección URL para propósitos de configuración y estos son despojados
    de la dirección URL después de la configuración del host virtual para cada solicitud.

  cliente1_intranet
    Ahora el verdadero recorrido a través de servidor Zope es que inicia. Después de configurar la parte de protocolo y el servidor
    de la nueva dirección URL que esta atravesando a través de Zope a la nueva raíz virtual para el host virtual. Usted puede agregar
    cero o más objetos aquí.

  VirtualHostRoot
    Finalmente la palabra clave mágica con la que se ha llegado al nuevo raíz virtual para el vhost. Cada cosa después del
    ``VirtualHostRoot`` es visible en el navegador Web.

  Caso especial _vh_documentos
    Imagine que usted quiere tener **http://intranet.cliente1.com/documentos/** como la dirección URL de su dirección URL virtual.
    Entonces usted puede obtener el efecto usando la declaración especial ``_vh_``. Cualquier segmento de ruta iniciando con ``_vh_``
    es despojado de la dirección URL para ser recorrido a través de Zope y volver a ser agregado sin ``_vh_`` después de recorrido.

    Un ejemplo: ::

      ^/documentos/(.*) \
      http://127.0.0.1:8080/VirtualHostBase/http/intranet.cliente1.com:80/\
      cliente1_intranet/VirtualHostRoot/_vh_documentos/$1

  \$1
    Así mismo como el ``^/(.*)`` y el ``\$1`` ambos son tipos de `expresión regular`_ hacia alguna sección especifica de su sitio,
    un ejemplo, puede ser una sección llamada **documentos**. Entonces el valor obtenido de la expresión ``^/(.*)`` se almacena en
    la variable \$1".


.. note::

  Usted no puede crear un objeto llamado ``VirtualHostBase`` o ``VirtualHostRoot``
  en su Zope ni debe agregar un objeto con el mismo ID de su VHM. Es posible que
  funcione, pero también puede dañar el sitio.


Suprimiendo Virtual Host Monster
================================

En el caso de que usted ha establecido reglas de virtual hosting de modo 
que ya no se Zope le permiten acceder a la interfaz de gestión, puede agregar
``_SUPPRESS_ACCESSRULE"`` a la dirección URL para desactivar ``VirtualHostMonster``.


.. seealso:: 
  
  - `Zope Virtual Hosting Services`_.

  - `Mapping the Virtual Host`_.

  - :ref:`Ejecutando Zope y Plone con Servidor Web Apache <zope_plone_webserver_apache>`.

  - :ref:`Ejecutando Zope y Plone con Servidor Web Nginx <zope_plone_webserver_nginx>`.


Referencias
===========

- `Definir Virtual Host y Reescritura de Servidor Web`_.

- `How VHM works`_.

.. _Hosting Virtual: http://httpd.apache.org/docs/2.0/es/vhosts/
.. _VirtualHostMonster: http://wiki.zope.org/zope2/VirtualHostMonster
.. _Nginx: http://wiki.nginx.org/NginxEs
.. _Apache 2: http://httpd.apache.org/
.. _mod_rewrite: http://httpd.apache.org/docs/2.2/mod/mod_rewrite.html
.. _mod_proxy: http://httpd.apache.org/docs/2.2/mod/mod_proxy.html
.. _Proxy inverso: http://es.wikipedia.org/wiki/Proxy#Reverse_Proxy_.2F_Proxy_inverso
.. _URL rewriting: http://en.wikipedia.org/wiki/URL_rewriting
.. _Servidor web: http://es.wikipedia.org/wiki/Servidor_web
.. _Virtual Host Monster: https://weblion.psu.edu/trac/weblion/wiki/VirtualHostMonster
.. _Zope Virtual Hosting Services: http://docs.zope.org/zope2/zope2book/VirtualHosting.html
.. _Mapping the Virtual Host: http://www.insmallsteps.com/lessons/lesson-hosting-install/mapping-the-virtual-host
.. _Definir Virtual Host y Reescritura de Servidor Web: http://wiki.canaima.softwarelibre.gob.ve/wiki/Definir_Virtual_Host_y_Reescritura_de_Servidor_Web
.. _How VHM works: http://plone.org/documentation/kb/plone-apache/vhm
.. _expresión regular: http://es.wikipedia.org/wiki/Expresión_regular
.. _https://plone.dcri.duke.edu/info/faq/vhm: https://plone.dcri.duke.edu/info/faq/vhm