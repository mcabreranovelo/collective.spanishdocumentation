.. -*- coding: utf-8 -*-

.. highlight:: rest

.. _deliverance_instalacion:

===========
Instalación
===========

Para instalar Deliverance, usted podría instalar la distribución de `Deliverance`_ de :term:`PyPI`:.

.. note::

    El paquete Deliverance sólo se requiere para obtener el comando para manipular 
    el `servidor proxy`_ Deliverance.

Usted puede instalar la distribución de `Deliverance`_ usando :ref:`easy_install <que_es_easyinstall>`, 
:ref:`pip <que_es_pip>` o :ref:`zc.buildout <que_es_zcbuildout>`. Por ejemplo, usando ``easy_install`` 
(sería ideal si se ejecuta dentro de un :ref:`entorno virtual <creacion_entornos_virtuales>` Python):

.. code-block:: console

    $ easy_install -U Deliverance

Usted también puede instalar con la herramienta :command:`pip` si es su preferencia, 
puede realizarlo con el siguiente comando:

.. code-block:: console

    $ pip install Deliverance
    

.. _configuracion_paster:

Usando plantillas Paster
========================

Luego de tener instalado el software, necesita la configuración para ejecutarlo. 
Allí es cuando podemos usar el script :command:`bin/paster` el cual tiene disponible 
dos plantillas :ref:`PasteScript <que_es_pastescript>` para construir sitios con 
configuraciones Deliverance, para comprobar esto ejecute el siguiente 
comando:

.. code-block:: console

    $ ./bin/paster create --list-templates
    Available templates:
      basic_package:      A basic setuptools-enabled package
      paste_deploy:       A web application deployed through paste.deploy
      deliverance:        Basic template for a deliverance-proxy setup
      deliverance_plone:  Plone-specific template for deliverance-proxy


plantilla deliverance
---------------------

Debería tener disponible la plantilla Paster ``deliverance`` la cual le permite crear 
una configuración básica para la instalación del `servidor proxy`_ Deliverance.

A continuación se demostra cada creación de cada una de las plantillas Paster descritas 
anteriormente, con el siguiente comando:

.. code-block:: console

    $ ./bin/paster create -t deliverance deliverance.examples.basic
    Selected and implied templates:
      Deliverance#deliverance  Basic template for a deliverance-proxy setup
    
    Variables:
      egg:      deliverance.examples.basic
      package:  deliveranceexamplesbasic
      project:  deliverance.examples.basic
    Enter host (The host/port to serve on) ['localhost:8000']: localhost:5000
    Enter proxy_url (The main site to connect/proxy to) ['http://localhost:8080']: localhost:8000
    Enter proxy_rewrite_links (Rewrite links from sub_host?) ['n']: y
    Enter password (The password for the deliverance admin console) ['']: secret
    Enter theme_url (A URL to pull the initial theme from (optional)) ['']: 
    Creating template deliverance
    Creating directory ./deliverance.examples.basic
      Recursing into etc
        Creating ./deliverance.examples.basic/etc/
        Copying deliv-users.htpasswd_tmpl to ./deliverance.examples.basic/etc/deliv-users.htpasswd
        Copying deliverance.xml_tmpl to ./deliverance.examples.basic/etc/deliverance.xml
        Recursing into supervisor.d
          Creating ./deliverance.examples.basic/etc/supervisor.d/
          Copying deliverance.conf_tmpl to ./deliverance.examples.basic/etc/supervisor.d/deliverance.conf
        Copying supervisord.conf_tmpl to ./deliverance.examples.basic/etc/supervisord.conf
    Creating ./deliverance.examples.basic/theme
    Creating ./deliverance.examples.basic/theme/theme.html
    Creating ./deliverance.examples.basic/theme/style.css

Este le preguntara algunas preguntas:

``host``:
    El host que Deliverance servirá.  Nota ``localhost`` (o 127.0.0.1) significa que usted puede solamente 
    conectarse desde la maquina misma.  Si usted quiere que sea visible externamente use 0.0.0.0.

``proxy_host``:
    Esta es la ubicación donde todas las peticiones irán. ``http://localhost:8080`` es el mas común por defecto 
    para los servidores.  Usted puede también dar un host remoto y una ruta, como ``http://mysite.com/blog``.

``proxy_rewrite_links``:
    Si usted es el proxy a un sitio que en realidad no esperan que seas proxy a la misma ves, los enlaces 
    probablemente se romperá. Usted puede dar como respuesta Y aquí para activar la reescritura de enlace. 
    No es 100% perfecto (por ejemplo, los enlaces puestos en Javascript), pero puede ser bueno para la 
    experimentación.

``password``:
    La contraseña a acceder a la consola de logging.  El nombre de usuario es siempre ``admin``. Usted puede 
    agregar o actualizar los inicio de sesiones mas tarde.

``theme_url``:
    Si usted quiere basar su tema en una pagina existente, usted puede dar la dirección URL de la pagina aquí. 
    Se obtendrá la página y todo el CSS e imágenes de esta página, por lo que a nivel local se pueden editar. 
    De lo contrario un tema sumamente sencilla se otorgara al momento de la instalación.

Una ves que usted allá ingresado esos valores, instalara una básica estructura con un archivo 
:file:`etc/deliverance.xml` para la configuración, y el tema en el archivo :file:`theme/theme.html`.

Acceda al directorio creado, con el siguiente comando:

.. code-block:: console

    $ cd deliverance.examples.basic/

Luego usted descargue el archivo :file:`bootstrap.py`, con el siguiente comando:

.. code-block:: console

    $ wget http://svn.zope.org/*checkout*/zc.buildout/trunk/bootstrap/bootstrap.py

Cree un archivo llamado :file:`buildout.cfg` 

.. code-block:: console

    $ vim buildout.cfg

Y agregue la siguiente configuración:

.. code-block:: cfg

    [buildout]
    
    versions = versions
    
    parts =
        deliverance-server
        
    [versions]
    Deliverance = 0.6.1
    WebOb = 1.2.3
    PasteScript = 1.7.5
    PasteDeploy = 1.5.0
    
    [deliverance-server]
    recipe = zc.recipe.egg
    eggs =
        Deliverance
        PasteScript

Entonces usted tiene que iniciar su proyecto, con el siguiente comando:

.. code-block:: console

    $ python bootstrap.py

Usted debe iniciar su proyecto, con el siguiente comando:

.. code-block:: console

    $ ./bin/buildout -vN


Usted debería ver algo como esto:

.. code-block:: console
 
    Generated script '/home/user/deliverance.examples.basic/bin/paster'.
    Generated script '/home/user/deliverance.examples.basic/bin/deliverance-proxy'.

Una ves instalado, usted debería buscar el script :command:`deliverance-proxy` en el directorio 
:file:`bin` de su proyecto zc.buildout y ejecute el proxy deliverance, con el siguiente comando:

.. code-block:: console

    $ ./bin/deliverance-proxy ./etc/deliverance.xml 
    To see logging, visit http://localhost:5000/.deliverance/login
        after login go to http://localhost:5000/?deliv_log
    serving on http://127.0.0.1:5000

Las configuraciones de esta instalación pueden descargarse ejecutando 
el siguiente comando:

.. code-block:: console

    $ git clone https://github.com/deliverance/deliverance.examples.basic.git

plantilla deliverance_plone
---------------------------

Debería tener disponible la plantilla Paster ``deliverance_plone`` la cual le permite 
crear una configuración especifica de Plone con un ``servidor proxy`` Deliverance.

En el caso que requiera aplicar configuraciones Deliverance con sitios web Plone, 
para hacer esto ejecute el siguiente comando:

.. code-block:: console

    $ ./bin/paster create -t deliverance_plone deliverance.examples.plone
    Selected and implied templates:
      Deliverance#deliverance        Basic template for a deliverance-proxy setup
      Deliverance#deliverance_plone  Plone-specific template for deliverance-proxy
    
    Variables:
      egg:      deliverance.examples.plone
      package:  deliveranceexamplesplone
      project:  deliverance.examples.plone
    Enter site_name (The name of your Plone site (no /'s)) ['']: Plone
    Enter host (The host/port to serve on) ['localhost:8000']: localhost:5000
    Enter proxy_url (The main site to connect/proxy to) ['http://localhost:8080']: 
    Enter proxy_rewrite_links (Rewrite links from sub_host?) ['n']: y
    Enter password (The password for the deliverance admin console) ['']: secret
    Enter theme_url (A URL to pull the initial theme from (optional)) ['']: 
    Creating template deliverance
    Creating directory ./deliverance.examples.plone
      Recursing into etc
        Creating ./deliverance.examples.plone/etc/
        Copying deliv-users.htpasswd_tmpl to ./deliverance.examples.plone/etc/deliv-users.htpasswd
        Copying deliverance.xml_tmpl to ./deliverance.examples.plone/etc/deliverance.xml
        Recursing into supervisor.d
          Creating ./deliverance.examples.plone/etc/supervisor.d/
          Copying deliverance.conf_tmpl to ./deliverance.examples.plone/etc/supervisor.d/deliverance.conf
        Copying supervisord.conf_tmpl to ./deliverance.examples.plone/etc/supervisord.conf
    Creating ./deliverance.examples.plone/theme
    Creating ./deliverance.examples.plone/theme/theme.html
    Creating ./deliverance.examples.plone/theme/style.css
    Creating template deliverance_plone
      Recursing into etc
    Replace 1601 bytes with 2062 bytes (3/49 lines changed; 9 lines added)
        Copying deliverance.xml_tmpl to ./deliverance.examples.plone/etc/deliverance.xml

Acceda al directorio creado, con el siguiente comando:

.. code-block:: console

    $ cd deliverance.examples.plone/

Luego usted descargue el archivo :file:`bootstrap.py`, con el siguiente comando:

.. code-block:: console

    $ wget http://svn.zope.org/*checkout*/zc.buildout/trunk/bootstrap/bootstrap.py

Cree un archivo llamado :file:`buildout.cfg`

.. code-block:: console

    $ vim buildout.cfg

Y agregue la siguiente configuración:

.. code-block:: cfg

    [buildout]
    
    extends = https://raw.github.com/collective/buildout.plonetest/master/plone-4.2.x.cfg
    
    versions = versions
    
    parts +=
        deliverance-server
        
    [versions]
    Deliverance = 0.6.1
    WebOb = 1.2.3
    PasteScript = 1.7.5
    PasteDeploy = 1.5.0
    
    [deliverance-server]
    recipe = zc.recipe.egg
    eggs =
        Deliverance
        PasteScript

Entonces usted tiene que iniciar su proyecto, con el siguiente comando:

.. code-block:: console

    $ python bootstrap.py

Usted debe iniciar su proyecto, con el siguiente comando:

.. code-block:: console

    $ ./bin/buildout -vN


Usted debería ver algo como esto:

.. code-block:: console
 
    Generated script '/home/user/deliverance.examples.plone/bin/paster'.
    Generated script '/home/user/deliverance.examples.plone/bin/deliverance-proxy'.

Una ves instalado, usted debería buscar el script ``deliverance-proxy`` en el directorio 
:file:`bin` de su proyecto zc.buildout y ejecute el proxy deliverance, con el siguiente comando:

.. code-block:: console

    $ ./bin/deliverance-proxy ./etc/deliverance.xml 
    To see logging, visit http://localhost:5000/.deliverance/login
        after login go to http://localhost:5000/?deliv_log
    serving on http://127.0.0.1:5000

Usted debe iniciar la instancia Zope, con el siguiente comando:

.. code-block:: console

    $ ./bin/instance start

Y para finalizar, sin importar la plantilla usada para crear la configuración, 
igualmente debe ejecutar manualmente el ``servidor proxy`` Deliverance, puede 
hacerlo ejecutando el siguiente comando:

.. code-block:: console

    $ ./bin/deliverance-proxy ./etc/deliverance.xml
    To see logging, visit http://localhost:5000/.deliverance/login
        after login go to http://localhost:5000/?deliv_log
    serving on http://localhost:5000

Como puede ver le esta indicando que Deliverance esta siendo servido por la 
dirección URL http://localhost:5000/ aplicando su estilo y tema HTML al contenido 
como se define en la archivo :file:`deliverance.xml`.

Para acceder a la consola depuración de iniciar sesión por la dirección URL 
http://localhost:5000/.deliverance/login y luego acceder a la dirección URL 
http://localhost:5000/?deliv_log

Las configuraciones de esta instalación pueden descargarse ejecutando 
el siguiente comando:

.. code-block:: console

    $ git clone https://github.com/deliverance/deliverance.examples.plone.git

Modos de instalación
====================

Para este caso se instalara el ejemplo de instalación llamado `DeliveranceDemo`_

.. toctree::
   :maxdepth: 2

   instalacion_buildout
   instalacion_wsgi

.. _Deliverance: http://pypi.python.org/pypi/Deliverance
.. _servidor proxy: http://es.wikipedia.org/wiki/Servidor_proxy
.. _DeliveranceDemo: http://svn.plone.org/svn/collective/deliverancedemo/trunk/
.. _middleware WSGI: http://en.wikipedia.org/wiki/Python_Paste#WSGI_middleware