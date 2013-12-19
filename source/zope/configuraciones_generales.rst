.. -*- coding: utf-8 -*-

.. _configuraciones_generales:

=========================
Configuraciones generales
=========================

:Autor(es): Leonardo J. Caballero G.
:Correo(s): leonardocaballero@gmail.com
:Compatible con: Plone 3, Plone 4
:Fecha: 19 de Diciembre de 2013


Algunos de los comportamientos de las instancias de Zope / Plone son controladas con 
variables de entorno del sistema operativo. Usted puede configurar los que están aquí 
en un formato de ``clave / valor``. 

Algunas de las siguientes son configuraciones adicionales al servidor Zope que son de 
gran utilidad:

Zona horaria
============

``TZ`` le permite a usted definir la zona horaria para sistemas donde no esta disponible 
automáticamente. Para esto debe agregar en la sección **[instance]** en su archivo de 
configuración de :file:`buildout.cfg`: 

.. code-block:: cfg

  environment-vars =
      TZ America/Caracas


Habilitar los idiomas necesarios en Plone
=========================================

Si solo necesita ofrecer soporte a i18n para N número de idiomas en específicos usted puede 
configurar esto agregando en la sección **[instance]** en su archivo de configuración del 
archivo :file:`buildout.cfg`:

.. code-block:: cfg

  environment-vars =
      PTS_LANGUAGES en, es, pt

De esta forma se esta habilitando el soporte a los idiomas Ingles, Español y Portugués, 
estoy puede ser muy conveniente por que ahorra recursos computo al momento de iniciar 
su instancias Zope.

``zope_i18n_compile_mo_files``, le permite la compilación automática de los archivos 
de las traducciones perdidas (tal ves haga el arranque de la instancia mas lento).

``zope_i18n_allowed_languages``, le permite limitar las traducciones disponibles.

speed up startup - only refresh translation catalog for those languages
see http://maurits.vanrees.org/weblog/archive/2010/10/i18n-plone-4

.. code-block:: cfg

  environment-vars =
      zope_i18n_compile_mo_files true
      zope_i18n_allowed_languages en es pt

Permission denied: ... .python-eggs
===================================

Error en la instalación del Producto debido a fallar en la creación de paquete Egg 
caché Algunas bibliotecas de Python, en particular, la biblioteca de ``Python-MySQL``, 
se distribuyen en los Paquetes Egg Python comprimido que necesitan ser descomprimidos 
en un directorio de caché.

A menos que especifique un directorio de destino para este caché, Python intentará 
crear en el directorio :file:`$HOME/.python-eggs`. Si ejecuta Zope bajo un identificador 
de usuario especial y con permisos mínimos (como debería ser), Python no puede ser 
capaz de crear el directorio de caché.

``PYTHON_EGG_CACHE``, determinas donde los paquetes Egg python comprimidos son 
desempacadas para su uso. Sin esta configuración no podemos ejecutar la instancia 
Zope como root con ``effictive-user`` de Zope y desde zope no puede escribir en 
:file:`/root/.python-eggs`.

.. code-block:: cfg

  environment-vars =
      PYTHON_EGG_CACHE ${buildout:directory}/var/.python-eggs

.. tip::

    Para mayor información consulte http://plone.org/documentation/error/permission-denied-python-eggs

PYTHONHASHSEED
==============

``PYTHONHASHSEED``, determina la preselección inicial para los hashes. "random" provoca 
un valor pseudo-aleatoria se utiliza para preseleccionar los objetos de hashes de str, 
bytes y datetime.

.. code-block:: cfg

  environment-vars =
      PYTHONHASHSEED random

.. tip::

    Para mayor información consulte:
    
    - http://docs.python.org/2.7/using/cmdline.html#envvar-PYTHONHASHSEED
    - http://www.marshut.com/phqqz/random-setup-profiles-missing-on-plone-4-3-installs.html
    - https://dev.plone.org/ticket/12850
