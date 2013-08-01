.. -*- coding: utf-8 -*-

.. _distribute_pip:

================
Distribute y pip
================

:Autor(es): Leonardo J. Caballero G.
:Correo(s): leonardocaballero@gmail.com
:Compatible con: Python 2.4 o versiones superiores
:Fecha: 20 de Marzo de 2013

Este articulo explica como instalar paquetes Python con ``Distribute`` y ``pip``.

.. _que_es_distribute:

¿Qué es Distribute?
===================

`Distribute`_ es un conjunto de mejoras en el módulo de la biblioteca
estándar de Python: `distutils`_ (para Python 2.3.5 y hasta en la mayoría de
las plataformas, plataformas de 64 bits requieren como mínimo de Python 2.4)
que le permite crear con más facilidad la distribución de paquetes de Python,
en especial los que tienen las dependencias de otros paquetes.

``Distribute`` se creó porque el :ref:`paquete Setuptools <que_es_setuptools>` 
actualmente ya no se mantiene. Los paquetes de terceros, es probable que requieran 
``setuptools``, que es proporcionado por el paquete ``Distribute``. Por lo tanto, 
en cualquier momento si los paquetes dependen del :ref:`paquete Setuptools <que_es_setuptools>`, 
``Distribute`` intervendrá para decir que ya ofrece el módulo de ``setuptools``.

.. image:: ./pip_distribute.png
  :align: center
  :alt: Move from Setuptools to Distribute

Estado actual del Empaquetamiento en Python
-------------------------------------------

El módulo ``distutils`` es parte de la `librería estándar`_ de Python y aun
lo será hasta la versión Python 3.3. 

.. note::
    El módulo ``distutils`` será descontinuado en Python 3.3. 

El módulo ``distutils2`` (note el número **dos**) tendrá compatibilidad hacia
atrás hasta Python 2.4 en adelante; y será parte de la `librería estándar`_ 
en Python 3.3.

El módulo ``distutils`` provee las bases para empaquetar aplicaciones Python.
Desafortunadamente, el módulo ``distutils`` está plagado de problemas, razón
por la cual un pequeño grupo de programadores de Python están trabajando en
``distutils2``. Sin embargo, hasta que ``distutils2`` este completado, se
recomienda que en el desarrollador pueda usar tanto el paquete ``distutils`` o 
el paquete ``Distribute`` para empaquetar software Python.

Al mismo tiempo, si un paquete requiere el :ref:`paquete Setuptools <que_es_setuptools>`, 
la recomendación es que instale el paquete ``Distribute``, el cual provee una versión más 
actualizada del :ref:`paquete Setuptools <que_es_setuptools>` que el `paquete original de Setuptools`_.

En el `futuro`_ ``distutils2`` remplazará a ``setuptools`` y ``distutils``,
le cual también removerá la necesidad de ``Distribute``. El como del estado
anterior ``distutils`` será removido de la `librería estándar`_. Para más
información, por favor, consulte el `Futuro del Empaquetado`_.


.. image:: ./state_of_packaging.jpg
  :alt: El estado actual de Empaquetado en Python
  :align: center

.. note::

  Ver el vídeo de la `PyCon 2011 - Packaging, from Distutils to Distutils2`_,
  Packaging or installing a Python application can be extremely painful por
  `Tarek Ziadé`_ esta charla le sumergiera dentro de las nuevas características
  de Distutils2 y explica como usted puede usarlo en su proyecto *hoy* para
  hacer más fácil la vida para todo el mundo (usuarios, administradores de
  paquetes de Sistemas operativos, programadores, etc.).

  Para descargar el vídeo `haga clic aquí`_ (**Tamaño 294 mb**) y para ver por
  vídeo Stream haga `clic aquí`_.

.. _que_es_pip:

¿Qué es pip?
============

`pip`_ es una herramienta para instalar y administrar :term:`Paquetes Python`, 
como los que puede encontrar en el Índice de Paquetes de Python - :term:`PyPI`. 

.. tip::
    Esta herramienta es el remplazo para la famosa herramienta 
    :ref:`easy_install <que_es_easyinstall>`. 

En su mayoría, ``pip`` utiliza las mismas técnicas para encontrar los paquetes, 
por lo que los paquetes que se instalaban usando la herramienta ``easy_install`` 
también deben ser instalables con la herramienta ``pip``. 

Esto significa que usted puede utilizar con el siguiente comando: 

.. code-block:: sh

    $ pip install AlgunPaquete 

En lugar del tradicional comando usado con la herramienta ``easy_install`` como 
se describe a continuación:

.. code-block:: sh

    $ easy_install AlgunPaquete


pip comparado con easy_install
------------------------------

``pip`` ofrece mejoras a la herramienta ``easy_install``. Algunas de las mejoras son:

-   Todos los paquetes se descargan antes de iniciar la instalación. Una
    instalación parcialmente completada no se produce como resultado.
    
-   Tiene cuidado de presentar una salida útil en la consola.
    
-   Las razones de las acciones de instalación se le aplica un seguimiento. 
    Por ejemplo, si un paquete se está instalando, ``pip`` sigue la pista de 
    por qué ese paquete era necesario.
    
-   Los mensajes de error debe ser útiles.
    
-   El código fuente es relativamente conciso y coherente, por lo que es
    más fácil de usar mediante programación.
    
-   Ofrece soporte nativo para otros sistemas de control de versiones
    (Git, Mercurial y Bazaar)
    
-   Tiene un mecanismo de desinstalación de paquetes.
    
-   Fácil de definir conjuntos de requerimientos y reproducir de forma
    fiable un conjunto de paquetes.
    
-   Los paquetes no tienen que ser instalados como :term:`paquetes Egg`, que
    pueden ser instalados en forma plana (mientras cuida la *metadata* de
    :term:`paquetes Egg`).


pip no hace todo lo que se easy_install. En concreto:
-----------------------------------------------------

-   No se puede instalar a partir de :term:`paquetes Egg`. Sólo se instala desde el
    código fuente. (En el futuro será bueno si se pudiera instalar los
    binarios de Windows EXE o MSI -.. pero instalar paquetes binarios para
    otras plataformas no es una prioridad).
    
-   No entiende la sección *SetupTools Extras* (como package[test]). Esto
    podría ser agregado eventualmente.
    
-   Es incompatible con algunos paquetes que tienen muchas personalizaciones
    ``distutils`` o ``setuptools`` en sus archivos :file:`setup.py`.

.. _instalacion_pip:

Instrucciones de Instalación
============================

Siempre existen más de dos formas de instalar paquetes Python con ``Distribute`` 
y ``pip`` ;)

Requerimientos previos
----------------------
Es necesario que instale ciertas dependencias en su sistema operativo como las que 
se muestran a continuación: 

.. code-block:: sh

  # aptitude install build-essential python-dev python-setuptools

Instalación con Paquetes Egg
----------------------------

Para instalar ``Distribute`` ejecute el siguiente comando: 

.. code-block:: sh

  # easy_install -U distribute

También para instalar ``pip`` ejecute el siguiente comando: 

.. code-block:: sh

  # easy_install -U pip

.. _uso_pip:

Instalación en sistemas Debian
------------------------------

La instalación en sistemas Debian es recomendable que instale ciertas dependencias 
en su sistema operativo como las que se muestran a continuación: 

.. code-block:: sh

  # aptitude install build-essential python-dev python-pip


Ejemplos de uso de pip
======================

La herramienta ``pip`` ofrece varias formas de uso, para instalar los paquetes de
diversas fuentes:

.. tip::
    
    Para poder utilizar el ``pip``, primero debe instalar ``setuptools`` o ``distribute``. 
    Si utiliza :ref:`virtualenv <que_es_virtualenv>`, una copia del ``pip`` será automáticamente 
    instalados en cada entorno virtual que usted crea. 
    
    ``pip`` se puede complementar con ``virtualenv``, y se recomienda que lo utilice para 
    :ref:`aislar a la instalación <creacion_entornos_virtuales>` de los :term:`paquetes Egg`.

**Ejemplo 1.** Instalar un paquete su nombre en su versión más reciente, buscando en :term:`PyPI`: 

.. code-block:: sh

    $ pip install SQLObject

**Ejemplo 2.** Instalar o actualizar un paquete por nombre y versión utilizando una dirección URL donde encontradas en una "página de descargas": 

.. code-block:: sh

    $ pip install -f http://dist.plone.org/packages/ 'Pillow==1.7.3'

**Ejemplo 3.** Instalar o actualizar un paquete desde su propio :ref:`replica del repositorio PyPI <creando_propio_repositorio_pypi>` o su repositorio de :term:`paquetes Egg` privados: 

.. code-block:: sh

    $ pip install -i http://pypi.ejemplo.com/simple SQLObject

**Ejemplo 4.** Descargar e instalar una distribución de código fuente: 

.. code-block:: sh

    $ pip install http://ejemplo.com/ruta/a/MiPaquete-1.2.3.tgz

**Ejemplo 5.** Instalar un paquete con una versión especifica: 

.. code-block:: sh

    $ pip install 'ZopeSkel==2.21.2'

**Ejemplo 6.** Instalar todas las dependencias de su proyecto Python usando un archivo de dependencias requeridas para instalar: 

.. code-block:: sh

    $ pip install -r ./requirements.txt

Un ejemplo del archivo :file:`requirements.txt` puede ser el siguiente: ::

    python-ldap
    django
    buildbot
    buildbot-slave
    PyYAML
    south

**Ejemplo 7.** Actualizar un paquete ya instalado con la versión más reciente de :term:`PyPI`: 

.. code-block:: sh

    $ pip install --upgrade PyProtocols

**Ejemplo 8.** Para usar realizar búsquedas de paquetes disponibles para instalar desde los repositorios por definidos: 

.. code-block:: sh

    $ pip search plonetheme-*

**Ejemplo 9.** Para remover un :term:`paquete Egg` 

.. code-block:: sh

    $ pip uninstall SQLObject


Para más información consulte la ayuda disponible por que paquete ``pip``
ejecutando el siguiente comando: 

.. code-block:: sh

    $ pip help


.. _distribute_buildout:

Distribute en zc.buildout
=========================

Puede usar Distribute en :ref:`zc.buildout <que_es_zcbuildout>`, habilitando 
el uso de este por medio de un parámetro adicional en su archivo ``bootstrap.py`` 
de la siguiente manera: 

.. code-block:: sh

    $ python bootstrap.py --distribute


.. _pip_buildout:

pip en zc.buildout
==================

Existen varias estrategias para integrar ``pip`` en :ref:`zc.buildout <que_es_zcbuildout>`, 
a continuación se describen algunas formas:

`gp.recipe.pip`_, ese paquete es un recipe de ``zc.buildout`` el cual permite
instalar :term:`Paquete Python` usando ``pip``. A continuación se explica un ejemplo de
configuración ``zc.buildout`` con este récipe se puede usar:

1.  El récipe agrega un :ref:`virtualenv <que_es_virtualenv>` en el directorio 
    ``parts/`` de su instalación buildout, entonces genera este binario para 
    generar un scripts  ejecutable Python. Así que tienes un área de pruebas 
    **limpia** de instalaciones previas.
    
2.  El récipe esta basado en `zc.recipe.egg#scripts`_ para que pueda
    compartir sus :term:`paquetes Egg` entre buildouts como de costumbre.
    
3.  Por supuesto, usted puede instalar algunos archivos **.pybundle**.

4.  Usted puede construir paquetes desde un repositorio SVN con la opción
    ``editables``.
    
5.  Cada linea encontrada en la opción ``install`` es la última parte de un
    comando de ``pip``. Esta le permitirá a usted construir :term:`paquetes Egg` 
    con sus dependencias. Por ejemplo, instalar la librería `lxml`_ en un 
    área de prueba pura, sin tener instalado ``libxml2`` y ``libxslt``, 
    usted necesita tener instalado ``Cython`` y con esta línea de comando 
    ``python setup.py install --static-deps`` para instalar para instalar el 
    paquete `lxml`_.

A continuación un ejemplo de configuración :ref:`zc.buildout <que_es_zcbuildout>`:

.. code-block:: cfg

    [buildout]
    # the cache dir is used by buildout & pip
    download-cache = download
    parts = eggs
      
    [eggs]
    recipe = gp.recipe.pip
   
    # eggs installed by pip (also add the Deliverance bundle)
    install =
        Cython
        --install-option=--static-deps lxml==2.2alpha1
        http://deliverance.openplans.org/dist/Deliverance-snapshot-
        latest.pybundle
      
    # eggs installed by zc.recipe.egg
    eggs =
        Paste
        pyquery
    

Otra forma de usar ``pip`` es a través de una extensión :ref:`zc.buildout <que_es_zcbuildout>` 
llamada `gp.vcsdevelop`_, para hacer checkout de :term:`paquetes Egg` desde 
varios `sistemas de control de versiones`_. A continuación se muestra un 
ejemplo de configuración ``zc.buildout`` con esta extensión:

.. code-block:: cfg

    [buildout]
    ...
    extensions = gp.vcsdevelop
    develop-dir = ./requirements
    requirements = requirements.txt
    parts = eggs
    ...
    [eggs]
    recipe = zc.recipe.egg
    eggs = ${buildout:requirements-eggs}
    interpreter = python
    ...

Un ejemplo del archivo :file:`requirements.txt` puede ser el siguiente: ::

    ConfigObject>=1.0
    -e git+git://github.com/bearstech/PloneTerminal.git#egg=PloneTerminal


Referencias
===========

-   El articulo `Distribute y pip`_ desde la comunidad Plone Venezuela.
-   `Installing the Package Tools`_.
-   `pip v1.0.2 documentation`_.
-   `Combine zc.buildout and pip benefits`_.

.. _Distribute: http://packages.python.org/distribute
.. _distutils: http://docs.python.org/3/library/distutils.html
.. _librería estándar: http://guide.python-distribute.org/glossary.html#term-standard-library
.. _paquete original de Setuptools: http://pypi.python.org/pypi/setuptools/
.. _futuro: http://guide.python-distribute.org/future.html
.. _Futuro del Empaquetado: http://guide.python-distribute.org/future.html
.. _PyCon 2011 - Packaging, from Distutils to Distutils2: http://us.pycon.org/2011/schedule/presentations/81/
.. _Tarek Ziadé: http://tarekziade.wordpress.com/
.. _haga clic aquí: http://blip.tv/file/get/Pycon-PyCon2011PackagingFromDistutilsToDistutils2191.mp4
.. _clic aquí: http://pycon.blip.tv/file/4880990
.. _pip: http://pypi.python.org/pypi/pip
.. _gp.recipe.pip: http://pypi.python.org/pypi/gp.recipe.pip
.. _zc.recipe.egg#scripts: http://pypi.python.org/pypi/zc.recipe.egg#id23
.. _lxml: http://codespeak.net/lxml/
.. _gp.vcsdevelop: http://pypi.python.org/pypi/gp.vcsdevelop/
.. _sistemas de control de versiones: http://es.wikipedia.org/wiki/Control_de_versiones
.. _Installing the Package Tools: http://guide.python-distribute.org/installation.html
.. _pip v1.0.2 documentation: http://www.pip-installer.org/en/latest/index.html
.. _Combine zc.buildout and pip benefits: http://www.gawel.org/weblog/en/2008/12/combine-zc.buildout-an-pip-benefits
.. _Distribute y pip: http://www.coactivate.org/projects/ploneve/distribute-y-pip
