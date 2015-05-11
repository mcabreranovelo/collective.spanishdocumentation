.. -*- coding: utf-8 -*-

.. _blogs:

=================
Blogs / Bitácoras
=================

.. sidebar:: Sobre este artículo

   :Autor(es): Leonardo J. Caballero G.
   :Correo(s): leonardoc@plone.org
   :Compatible con: Plone 4 o versiones superiores
   :Fecha: 10 de Mayo de 2015

Existe varios productos para Bitácoras / Blogs entre ellos los mas destacados están:

.. _blogstar_quees:

Producto blog.star
==================

El producto `blog.star`_, es una suite de Blog para Plone.

¿Qué hace?
----------

Este :term:`Producto Plone` es una suite de Blogging para Plone.

.. figure:: blog_star.png
  :align: center
  :alt: El producto blog.star, para Bitácoras/Blogs.

  El producto **blog.star**, para Bitácoras/Blogs.

.. _blogstar_info:

.. sidebar:: Ficha técnica del producto

   :Pagina del proyecto: http://plone.org/products/collective.blog.star
   :Repositorio de código: https://github.com/collective/collective.blog.star
   :Programador del producto: Jarn AS.

.. _blogstar_instalar:

¿Cómo instalarlo?
-----------------

La instalación de este producto se realiza usando la herramienta 
:ref:`zc.buildout <que_es_zcbuildout>` para esto usted tiene que agregar 
el producto a las sección ``eggs`` del archivo :file:`buildout.cfg` como 
se muestra a continuación:

.. code-block:: cfg

  eggs =
      ...
      collective.blog.star

Luego ejecute el script :command:`buildout`, de la siguiente forma:

.. code-block:: sh

  $ ./bin/buildout -vN

Con este comando busca el paquete en el repositorio :term:`PyPI`, descarga e 
instala el producto en su instancia Zope para sus sitios Plone allí hospedados.

Entonces inicie la :term:`Instancia de Zope`, de la siguiente forma:

.. code-block:: sh

  $ ./bin/instance fg
  
Luego de esto ya tiene disponible el servidor Zope, el producto puede ser activado 
en cada sitio Plone dentro de su :term:`Instancia de Zope` como se describe a 
continuación:

Activarlo en Plone
------------------

Para activar este producto en un sitio Web Plone 4 usted debe acceder a la sección 
:menuselection:`Configuración del sitio --> Complementos`, ubicada en la esquina 
superior derecha en el nombre del usuario, como se muestra a continuación:

.. figure:: ../productos/productos_complementos_1.png
  :align: center
  :alt: Acceder a la Configuración del sitio

  Acceder a la Configuración del sitio

Después haga clic en panel de control **Complementos**, como se muestra a continuación:

.. figure:: ../productos/productos_complementos_2.png
  :align: center
  :alt: Acceder al panel de control Complementos

  Acceder al panel de control Complementos

Entonces marque la casilla llamada **blog.star** y luego presione el botón 
**Activar**.

.. _blogstar_usar:

Usar el producto blog.star
--------------------------

Para usar este producto usted puede crear tipo de contenido **Carpeta** 
y cambiar su vista desde el menú :menuselection:`Mostrar --> Blog view` 
convirtiendo esa carpeta en un blog. Usted puede agregar de entradas a 
blog con el tipo de contenidos **Pagina** y podrá crear entradas de podcast 
con el tipo de contenidos **Archivo** gracias al producto `collective.flowplayer`_.

Usted también puede definir un conjunto de portlets disponibles, como 
Archivo Mensual, Ultimas entradas al Blog y un portlet de Nubes de Etiquetas 
con el producto `qi.portlet.TagClouds`_, Comentarios en su cuenta Twitter con 
el producto `collective.twitterportlet`_.

Si usted necesita comentarios para las entradas en tu blog, por defecto Plone 
incorpora un sistema de comentarios y discusiones, este se configura en 
:menuselection:`Configuración del sitio --> Discusión`. Si usted requiere otro 
tipo de comentarios se recomienda usar el producto `collective.disqus`_.

----

.. _quills_quees:

Producto Quills
===============

El producto `Quills`_ es muy parecido a las características funcionales que 
ofrece Wordpress.

¿Qué hace?
----------

Este :term:`Producto Plone` es una suite de Blogging para Plone.

.. figure:: quills.png
  :align: center
  :alt: El producto Quills, para Bitácoras/Blogs

  El producto **Quills**, para Bitácoras/Blogs.

.. _quills_info:

.. sidebar:: Ficha técnica del producto

   :Pagina del proyecto: http://plone.org/products/quills
   :Repositorio de código: https://github.com/collective/Products.Quills
   :Programador del producto: Quills Team.

.. _quills_instalar:

¿Cómo instalarlo?
-----------------

La instalación de este producto se realiza usando la herramienta 
:ref:`zc.buildout <que_es_zcbuildout>` para esto usted tiene que agregar 
el producto a las sección ``eggs`` del archivo :file:`buildout.cfg` como 
se muestra a continuación:

.. code-block:: cfg

  eggs =
      ...
      Products.Quills

Luego ejecute el script :command:`buildout`, de la siguiente forma:

.. code-block:: sh

  $ ./bin/buildout -vN

Con este comando busca el paquete en el repositorio :term:`PyPI`, descarga e 
instala el producto en su instancia Zope para sus sitios Plone allí hospedados.

Entonces inicie la :term:`Instancia de Zope`, de la siguiente forma:

.. code-block:: sh

  $ ./bin/instance fg
  
Luego de esto ya tiene disponible el servidor Zope, el producto puede ser activado 
en cada sitio Plone dentro de su :term:`Instancia de Zope` como se describe a 
continuación:

Activarlo en Plone
------------------

#. Para activar este producto en un sitio Web Plone 4 usted debe acceder a la sección 
   :menuselection:`Configuración del sitio --> Complementos`, ubicada en la esquina 
   superior derecha en el nombre del usuario.

#. Después haga clic en panel de control **Complementos**.

#. Entonces marque la casilla llamada **Products.Quills** y luego presione el botón 
   **Activar**.

.. _quills_usar:

Usar el producto Quills
-----------------------

Este producto se usa mediante la agregación de nuevos tipos de contenidos en su sitio 
Plone. En la barra de acciones de contenidos valla al menú desplegable 
:menuselection:`Agregar nuevo... --> Weblog` este tipo de contenido sirve como contener 
de entradas del blog y la organización del mismo.

----

.. _scrawl_quees:

Producto Scrawl
===============

`Scrawl`_, es una suite de Blogging con un enfoque extremadamente simple para Plone.

¿Qué hace?
----------

Este :term:`Producto Plone` copia el tipo de contenido Noticia para crear el tipo de 
contenido Blog Entry (with a slightly tweaked view template) y agrega una alternativa vista 
para las Colecciones (blog_view).

Note que la vista blog_view shows either the description of each contained blog entry 
(if it exists) or the entire body.  It's up to the user to limit those results in an 
intelligent way so that page loads doesn't take too long.

.. figure:: scrawl.png
  :align: center
  :alt: El producto Scrawl, para Bitácoras/Blogs

  El producto **Scrawl**, para Bitácoras/Blogs.

.. _scrawl_info:

.. sidebar:: Ficha técnica del producto

   :Pagina del proyecto: http://plone.org/products/scrawl
   :Repositorio de código: https://github.com/collective/Products.Scrawl
   :Programador del producto: Jon Baldivieso.

.. _scrawl_instalar:

¿Cómo instalarlo?
-----------------

La instalación de este producto se realiza usando la herramienta 
:ref:`zc.buildout <que_es_zcbuildout>` para esto usted tiene que agregar 
el producto a las sección ``eggs`` del archivo :file:`buildout.cfg` como 
se muestra a continuación:

.. code-block:: cfg

  eggs =
      Products.Scrawl
      
Luego ejecute el script :command:`buildout`, de la siguiente forma:

.. code-block:: sh

  $ ./bin/buildout -vN

Con este comando busca el paquete en el repositorio :term:`PyPI`, descarga e 
instala el producto en su instancia Zope para sus sitios Plone allí hospedados.

Entonces inicie la :term:`Instancia de Zope`, de la siguiente forma:

.. code-block:: sh

  $ ./bin/instance fg
  
Luego de esto ya tiene disponible el servidor Zope, el producto puede ser activado 
en cada sitio Plone dentro de su :term:`Instancia de Zope` como se describe a 
continuación:

Activarlo en Plone
------------------

#. Para activar este producto en un sitio Web Plone 4 usted debe acceder a la sección 
   :menuselection:`Configuración del sitio --> Complementos`, ubicada en la esquina 
   superior derecha en el nombre del usuario.

#. Después haga clic en panel de control **Complementos**.

#. Entonces marque la casilla llamada **Scrawl** y luego presione el botón
   **Activar**.

.. _scrawl_usar:

Usar el producto Scrawl
-----------------------

Este producto se usa mediante la agregación de nuevos tipos de contenidos en su sitio 
Plone. En la barra de acciones de contenidos valla al menú desplegable 
:menuselection:`Agregar nuevo... --> Blog Entry` este tipo de contenido describe la 
entrada de su blog en si mismo.

Descarga código fuente
======================

Usted puede obtener el código fuente usado en estas configuraciones buildout para este 
ejemplo, ejecutando el siguiente comando:

.. code-block:: sh

  $ git clone https://github.com/plone-ve/plonedemos.suite.git

Luego de descargar este código fuente, es recomendable leer el archivo :file:`README.rst` 
y siga las instrucciones descrita en ese archivo.

.. _blog.star: https://pypi.python.org/pypi/collective.blog.star
.. _collective.flowplayer: https://pypi.python.org/pypi/collective.flowplayer
.. _qi.portlet.TagClouds: https://pypi.python.org/pypi/qi.portlet.TagClouds
.. _collective.twitterportlet: https://pypi.python.org/pypi/collective.twitterportlet
.. _collective.disqus: https://pypi.python.org/pypi/collective.disqus
.. _Quills: http://plone.org/products/quills/
.. _Scrawl: http://plone.org/products/scrawl/

