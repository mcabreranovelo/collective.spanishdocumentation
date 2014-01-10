.. -*- coding: utf-8 -*-

.. _producto_tema:

==============================
Creación de un paquete de tema
==============================

.. sidebar:: Sobre este artículo

    :Autor(es): Carlos de la Guardia, Leonardo J. Caballero G.
    :Correo(s): carlos.delaguardia@gmail.com, leonardocaballero@gmail.com
    :Compatible con: Plone 3, Plone 4
    :Fecha: 05 de Enero de 2014

.. _producto_tema_intro:

Introducción
============

Un tema de Plone es un conjunto de :ref:`templates <zpt_lenguage>`, imágenes, 
estilos y código Python que dan la apariencia visual al sitio de Plone. 
Usualmente se le da también el nombre de `skin`.

Plone utiliza dos mecanismos generales para definir los elementos de un tema:
skins de CMF y vistas de Python. 

Skins de CMF
============

El Content Management Framework (CMF) es un producto de Zope que forma parte
de las dependencias básicas de Plone. Un skin de CMF consiste en uno o mas
directorios que contienen los templates, scripts y recursos del sitio Plone.
El conjunto de directorios del skin esta ordenado por prioridad, del mas alto
al mas bajo. Para mostrar un recurso determinado del sitio, por ejemplo el
logotipo, Plone busca por nombre en todos los directorios del skin comenzando
con el de prioridad mas alta, hasta encontrar el primero que contenga el
nombre buscado.

Es posible incluir capas para el skin del sitio en un producto de Plone y
definir su prioridad como máxima, de tal manera que cualquier elemento de
Plone que se incluya en el producto tendrá precedencia sobre los de Plone o
cualquier otro producto que se encuentre mas abajo en la lista de capas.

Vistas y viewlets en Python
===========================

En los skins de CMF es posible colocar scripts de Python, pero estos están
restringidos en cuanto a utilización de librerías y acceso al sistema en
general. Es por eso que cuando se requiere un procesamiento mas complejo de
datos es mejor utilizar Python directamente y no a través del skin. Plone
tiene un mecanismo para generar paginas utilizando Python y opcionalmente un
template de :ref:`ZPT <zpt_lenguage>`, mediante vistas y viewlets.

Una vista es una clase de Python que usualmente se asocia con un template
para producir una pagina web. Un viewlet es un fragmento de HTML generado por
una clase de Python y un template, de manera similar a las vistas. La
diferencia es que los viewlets se integran en una estructura de pagina
definida por una serie de contenedores conocidos como `viewlet managers`,
mientras que las vistas son totalmente independientes.

.. _producto_tema_generar:

Generación con paster
=====================

Un tema es un conjunto de ``skins``, vistas y ``viewlets`` definidos dentro de un
:term:`Producto Plone`. La manera mas fácil de crear uno es utilizar los templates
para :command:`paster` del paquete ZopeSkel:

.. tip::
    Debe tener instalado el paquete :ref:`ZopeSkel <skel_plone>` para poder 
    usar el comando :command:`paster`.

.. note:: 
    Debe estar dentro el directorio :file:`src/` de su instalación el cual 
    fungirá como directorio que contendrá los paquetes en desarrollo.

Lo primero que hace es mandar llamar el template ``plone3_theme``, pasándole el
nombre del paquete que creara. El template utiliza una estructura de directorios 
de dos niveles, por lo que hay que usar un nombre compuesto. Por lo general, 
la primera parte del nombre define la `marca` o la categoría general del paquete 
y la segunda parte el nombre "verdadero" del mismo. En este ejemplo el nombre es 
`plonetheme.cliente1`:

.. code-block:: sh

    $ paster create -t plone3_theme plonetheme.cliente1
    Selected and implied templates:
      ZopeSkel#basic_namespace  A basic Python project with a namespace package
      ZopeSkel#plone            A project for Plone products
      ZopeSkel#plone3_theme     A theme for Plone 3

    Variables:
      egg:      plonetheme.cliente1
      package:  plonethemecliente1
      project:  plonetheme.cliente1

A continuación, :command:`paster` realiza algunas preguntas para personalizar 
la generación del paquete. La primera es si desea contestar todas las preguntas 
(``all``) o solo algunas (``easy``). Usted debe contestar ``all``.

.. code-block:: sh

    Expert Mode? (What question mode would you like? (easy/expert/all)?) ['easy']: all

Después le pregunta los nombres del paquete ``Namespace`` (primera parte del 
nombre pasado al template) y el nombre del paquete (segunda parte). Como los
valores por omisión son los mismos que le paso como parámetros en el comando 
anterior, basta presiona la tecla ``Enter`` en las siguientes dos preguntas.

.. code-block:: sh

    Namespace Package Name (Name of outer namespace package) ['plonetheme']: 
    Package Name (Name of the inner namespace package) ['cliente1']: 

A continuación necesita dar el nombre del skin que se mostrara en los
paneles de control de Plone para referirse a nuestro paquete

.. code-block:: sh

    Skin Name (Name of the theme (human facing, added to portal_skins)) ['']: Tema de cliente1

La siguiente pregunta permite definir el skin base para el nuestro, desde
donde se copiaran todas las capas registradas, de manera que no sea necesario
para usted definir toda la lista. Usualmente usará el skin de Plone

.. code-block:: sh

    Skin Base (Name of the theme from which this is copied) ['Plone Default']: 

Si requiere cambiar la apariencia visual del sitio totalmente, tal vez sea
aconsejable comenzar con hojas de estilos vacías. Si no lo hace así, las 
hojas de estilos del sitio de Plone estarán activas y todas sus definiciones
afectaran la vista final del sitio. En este caso basta utilizar las de Plone,
por lo que se deja vacía la respuesta

.. code-block:: sh

    Empty Styles? (Override default public stylesheets with empty ones?) [False]: 

El template puede incluir directamente en el código algunos comentarios
descriptivos sobre las operaciones que realiza, para ayudar al programador a
comprender lo que esta sucediendo. Por defecto se incluirán dichos
comentarios

.. code-block:: sh

    Include Documentation? (Include in-line documentation in generated code?) [True]: 


La versión del paquete que se utiliza en Plone 4 en la sección  
:menuselection:`Configuración del sitio --> Complementos` o en Plone 3 en la sección 
:menuselection:`Configuración del sitio --> Productos Adicionales` para mostrar 
al usuario la versión instalada del producto: 

.. code-block:: sh

    Version (Version number for project) ['1.0']: 0.1

Después, se pide una corta descripción del tema

.. code-block:: sh

    Description (One-line description of the project) ['An installable theme for Plone 3']: Tema de cliente1

Algunos temas requieren además de la apariencia visual modificar la
configuración del sitio de Plone, para lo que es necesario incluir un perfil
de :ref:`generic setup <perfiles_genericsetup>`:

.. code-block:: sh

    Register Profile (Should this package register a GS Profile) [True]: 

Las siguientes preguntas son para definir un perfil de registro para subir
el paquete a un repositorio como el :term:`Python Package Index`

.. code-block:: sh

    Long Description (Multi-line description (in ReST)) ['']: Tema basado en Skin Plone 3 para cliente1 el cual personaliza el sitio Plone a la imagen corporativas.
    Author (Name of author for project) ['']: Leonardo J. Caballero G.
    Author Email (Email of author for project) ['']: leonardocaballero@gmail.com
    Keywords (List of keywords, space-separated) ['web zope plone theme']: web zope plone theme cliente1
    Project URL (URL of the homepage for this project) ['http://svn.plone.org/svn/collective/']: https://github.com/collective/plonetheme.cliente1
    Project License (Name of license for the project) ['GPL']: 

Finalmente, las ultimas dos preguntas siempre ocuparan los valores por defecto

.. code-block:: sh

    Zip-Safe? (Can this project be used as a zipped egg? (true/false)) [False]: 
    Zope2 Product? (Are you creating a product for Zope2/Plone or an Archetypes Product?) [True]:
    Creating template basic_namespace
    Creating directory ./plonetheme.cliente1
    ...
    ------------------------------------------------------------------------------
    The project you just created has local commands. These can be used from within
    the product.
    
    usage: paster COMMAND
    
    Commands:
      addcontent  Adds plone content types to your project
    
    For more information: paster help COMMAND
    ------------------------------------------------------------------------------
    Running python setup.py egg_info

Luego de responder a estas preguntas el programa :command:`paster` creará la 
estructura inicial del paquete del tema de Plone llamado :file:`plonetheme.cliente1` 
en el directorio :file:`src/` de su instalación el cual fungirá como directorio que 
contendrá los paquetes en desarrollo.

::

    plonetheme.cliente1/
    |-- docs
    |   |-- HISTORY.txt
    |   |-- INSTALL.txt
    |   |-- LICENSE.GPL
    |   `-- LICENSE.txt
    |-- MANIFEST.in
    |-- plonetheme
    |   |-- cliente1
    |   |   |-- browser
    |   |   |   |-- configure.zcml
    |   |   |   |-- images
    |   |   |   |   `-- README.txt
    |   |   |   |-- __init__.py
    |   |   |   |-- interfaces.py
    |   |   |   |-- stylesheets
    |   |   |   |   |-- main.css
    |   |   |   |   `-- README.txt
    |   |   |   |-- viewlet.pt
    |   |   |   `-- viewlets.py
    |   |   |-- configure.zcml
    |   |   |-- __init__.py
    |   |   |-- locales
    |   |   |   `-- README.txt
    |   |   |-- profiles
    |   |   |   `-- default
    |   |   |       |-- cssregistry.xml
    |   |   |       |-- jsregistry.xml
    |   |   |       |-- metadata.xml
    |   |   |       |-- plonetheme.cliente1_various.txt
    |   |   |       |-- skins.xml
    |   |   |       `-- viewlets.xml
    |   |   |-- profiles.zcml
    |   |   |-- setuphandlers.py
    |   |   |-- skins
    |   |   |   |-- plonetheme_cliente1_custom_images
    |   |   |   |   `-- CONTENT.txt
    |   |   |   |-- plonetheme_cliente1_custom_templates
    |   |   |   |   `-- CONTENT.txt
    |   |   |   `-- plonetheme_cliente1_styles
    |   |   |       |-- base_properties.props
    |   |   |       `-- CONTENT.txt
    |   |   |-- skins.zcml
    |   |   |-- tests.py
    |   |   `-- version.txt
    |   `-- __init__.py
    |-- plonetheme.cliente1-configure.zcml
    |-- plonetheme.cliente1.egg-info
    |   |-- dependency_links.txt
    |   |-- entry_points.txt
    |   |-- namespace_packages.txt
    |   |-- not-zip-safe
    |   |-- paster_plugins.txt
    |   |-- PKG-INFO
    |   |-- requires.txt
    |   |-- SOURCES.txt
    |   `-- top_level.txt
    |-- README.txt
    |-- setup.cfg
    `-- setup.py


.. _producto_tema_instalar:

¿Cómo instalarlo?
=================

Luego de generar el tema debe agregar este a la configuración buildout para completar 
la instalación de este producto. Esto se realiza usando la herramienta :ref:`zc.buildout <que_es_zcbuildout>` 
para esto usted tiene que agregar el producto a las sección ``eggs`` del archivo :file:`buildout.cfg` 
como se muestra a continuación:

.. code-block:: cfg

  eggs =
      plonetheme.cliente1
      
.. note::
    Debe tener habilitado la extensión :ref:`mr.developer <mrdeveloper>` para gestionar localmente
    el producto en desarrollo, y posterior publicación en un sistema de control de versiones.

Quizás dependiendo su configuración en la variable declarativa de ``auto-checkout`` de 
:ref:`mr.developer <mrdeveloper>` tiene que agregar la siguiente linea:

.. code-block:: cfg

  auto-checkout =
      plonetheme.cliente1

.. tip:: Usted puede usar el comodín ``*`` en ves de cada linea con los paquetes en desarrollo, 
    lo cual le indicara a la extensión :ref:`mr.developer <mrdeveloper>` que compruebe local desde 
    el :term:`filesystem` o remotamente desde un :ref:`control de versiones <rcs_index>` todos los 
    paquetes de descritos en la sección ``sources``.

En la su sección declarativa ``sources`` del archivo :file:`buildout.cfg` tiene que agregar 
la siguiente linea:

.. code-block:: cfg

  [sources]
  plonetheme.cliente1 = fs plonetheme.cliente1

.. tip:: la opción ``fs`` le indica a la extensión :ref:`mr.developer <mrdeveloper>` que 
    gestione el paquete localmente desde el :term:`filesystem` o sistema de archivo.

Luego ejecute el script :command:`buildout`, de la siguiente forma:

.. code-block:: sh

  $ ./bin/buildout -vN

Con este comando busca el paquete o sus dependencias en el repositorio :term:`PyPI`, 
descarga e instala el producto en su instancia Zope para sus sitios Plone allí hospedados.

.. note:: Hasta este punto usted **NO** ha publicado *producto de tema* en en el repositorio 
    :term:`PyPI`, mas si este tiene dependencias de instalación se descargaran e instalaran 
    por usted.

Entonces inicie la :term:`Instancia de Zope`, de la siguiente forma:

.. code-block:: sh

  $ ./bin/instance fg 

Luego de esto ya tiene disponible el producto para ser habilitado en cada sitio 
Plone dentro de su :term:`Instancia de Zope`.

.. _producto_tema_habilitar:

Habilitarlo en Plone
====================

Para instalar de este producto en cada sitio Plone usted debe **Habilitarlo** o 
**Instalarlo**, este proceso se hace manualmente como se describe a continuación:

En **Plone 4** acceda a la :menuselection:`Configuración del sitio --> Complementos` 
y marque la casilla llamada **Tema de cliente1** y luego presione el botón **Habilitar**.

.. todo::
    Agregar capturas de pantallas para este procedimiento

En **Plone 3** (versiones anteriores) acceda a la 
:menuselection:`Configuración del sitio --> Productos Adicionales` y marque la casilla 
llamada **Tema de cliente1** y luego presione el botón **Instalar**.

De esta forma ya tiene disponible su :term:`Producto Plone` de temas para ser usado en su 
sitio Plone.

Comando locales de temas
========================

.. todo::
    Escribir sobre este punto

Resumen
=======

En este artículo has aprendido a:

- Entender el :ref:`funcionamiento <producto_tema_intro>` del producto.

- ¿:ref:`Cómo generar <producto_tema_generar>` el producto?.

- ¿Cómo :ref:`instalar <producto_tema_instalar>` y :ref:`habilitar <producto_tema_habilitar>` 
  el producto creado en un sitio Plone.

Descarga código fuente
======================

Usted puede descargar el código fuente de este ejemplo, para esto ejecute el siguiente comando:

.. code-block:: sh

  $ git clone https://github.com/plone-ve/plonetheme.cliente1.git plonetheme.cliente1

.. seealso:: 
  
  -   :ref:`Referencias de Temas en Plone <referencias_temas_plone>`.

  -   Sistema de plantillas con :ref:`Deliverance <apariencias_deliverance>`.

Referencia
==========

- `Creación de un paquete de tema`_ desde la comunidad Plone México.

.. _Creación de un paquete de tema: http://www.plone.mx/docs/tema.html