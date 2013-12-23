.. -*- coding: utf-8 -*-

.. _contentwellportlets:

Content Well Portlets
=====================

:Autor(es): Leonardo J. Caballero G.
:Correo(s): leonardocaballero@gmail.com
:Compatible con: Plone 4
:Fecha: 23 de Diciembre de 2013

En esta articulo es una traducción actualizada del articulo en Portugués 
`ContentWellPortlets — Tutorial Plone 4`_, el cual busca explicar la instalación 
del producto ContentWellPortlets.

¿Qué hace?
==========

Permite agregar ``portlets`` encima e abajo de la sección de contenido.


Información básica del producto
===============================

* Pagina del proyecto: http://plone.org/products/contentwellportlets

* Repositorio de código: http://weblion.psu.edu/

* Programador del producto: `WebLion Group`_.


¿Cómo instalarlo?
=================

La instalación de este producto se realiza usando la herramienta 
:ref:`zc.buildout <que_es_zcbuildout>` para esto usted tiene que agregar 
el producto a las secciones ``eggs`` y ``zcml`` (si es necesario) de archivo 
:file:`buildout.cfg` como se muestra a continuación:

.. code-block:: cfg

  eggs =
      Products.ContentWellPortlets
      

Indicar al :term:`recipe` `plone.recipe.zope2instance`_ que instale una 
configuración :term:`ZCML-slug`, como se muestra a continuación:

.. code-block:: cfg

  zcml =
      Products.ContentWellPortlets
      
Luego ejecute el script :command:`buildout`, de la siguiente forma:

.. code-block:: sh

  $ ./bin/buildout -vN

Con este comando busca el paquete en el repositorio :term:`PyPI`, descarga e 
instala el producto en su instancia Zope para sus sitios Plone allí hospedados.

Entonces inicie la :term:`Instancia de Zope`, de la siguiente forma:

.. code-block:: sh

  $ ./bin/instance fg
  

Luego de esto ya tiene disponible el producto para ser habilitado en cada sitio 
Plone dentro de su :term:`Instancia de Zope` como se describe a continuación:

Habilitarlo en Plone
--------------------

En Plone 4 acceda a la :menuselection:`Configuración del sitio --> Complementos` 
y marque la casilla llamada **ContentWellPortlets** y luego presione el botón **Habilitar**.

En Plone 3 (versiones anteriores) acceda a la :menuselection:`Configuración del sitio --> Agregar/Quitar Productos` 
y marque la casilla llamada **ContentWellPortlets** y luego presione el botón **Instalar**.

Configuración del Content Well Portlets
=======================================

Después de haber realizado la instalación del producto, todas las páginas presentaran 
dos o tres nuevos enlaces, como se muestra a continuación:

.. figure:: contentwellportlets_1.png
   :align: center
   :alt: Arriba del contenido

   Arriba del contenido

El enlace **Agregar, editar o eliminar un portlet encima del contenido** conduce a
la administración de portlets situados sobre el contenido de la página.

----

.. figure:: contentwellportlets_2.png
   :align: center
   :alt: Abajo del contenido

   Abajo del contenido

El enlace **Agregar, editar o eliminar un portlet a continuación el contenido** lleva a la página
de administración de portlets situados por debajo del contenido y el enlace **Añadir, editar
o eliminar un portlet en el pie de página** conduce la página
de administración de portlets situados en la parte inferior de la página. 

La interfaz estos casos es la misma, es posible disponer los portlets en tres columnas 
diferentes (A, B y C) y colocar mas de un portlet por columna.

.. figure:: contentwellportlets_3.png
   :align: center
   :alt: 


Resulta en:

.. figure:: contentwellportlets_4.png
   :align: center
   :alt: Un portlet de Calendario el contenido de la página

   Un portlet de Calendario el contenido de la página

Las columnas permiten una mayor libertad para la manipulación visual de loa portlets 
usando estilos CSS, ya que cada columna corresponde a un div class diferente.


.. _ContentWellPortlets — Tutorial Plone 4: http://www.ufrgs.br/tutorial-plone4/produtos-adicionais/contentwellportlets
.. _WebLion Group: http://plone.org/author/weblion
.. _plone.recipe.zope2instance: http://pypi.python.org/pypi/plone.recipe.zope2instance