.. -*- coding: utf-8 -*-

.. _python_index:

Python
======

Python es el lenguaje con el que están desarrollados tanto Zope como Plone,
por lo que es muy importante conocerlo para poder tomar máxima ventaja de
estos sistemas. Es imprescindible programar en Python para poder crear
productos y tipos de contenido para Plone.

En esta sección tenemos el tutorial oficial de Python, preparado por la
asociación de Python de Argentina y la fundación de Python.

.. toctree::
   :maxdepth: 1

   Tutorial de Python <tutorial-usla/index>


Inmersión al modo interactivo de Python
---------------------------------------

La idea de este tutorial es que alguien que **NUNCA** ha trabajando con el
interprete de `Python`_ pueda tener un primer acercamiento **SIN PROGRAMAR**, 
solamente con conocer el uso del interprete y sus comando básicos.

.. _Python: http://www.python.org/

.. toctree::
   :maxdepth: 1

   una_pequena_inmersion_python


Entornos virtuales en Python
----------------------------

Python ofrece un mecanismo para poder experimentar con nuevas versiones de 
librerías Python en formato :term:`Egg`, sin afectar su sistema, o para crear 
un entorno de instalación Python aislado al interprete Python de su sistema 
operativo, por eso está sección que se dedica a explicar sus casos de uso.

.. toctree::
   :maxdepth: 1

   creacion_entornos_virtuales


Sistema de paquetes Python
--------------------------

Python ofrece un sistema de paquetes para aplicaciones Python en formato 
:term:`Egg`, para la cual posee dos especificaciones de como hacer 
:term:`paquetes Egg` y sus respectivas utilidades para la gestión de estos 
paquetes, por eso está sección que se dedica a explicar sus diferencias.

.. toctree::
   :maxdepth: 1

   setuptools
   distribute_pip
   instalar_config_propio_mirror_pypi


Esqueletos de proyectos
-----------------------

Como parte de la filosofía de desarrollo ágil de aplicaciones, varios proyectos 
Python ofrecen mecanismo de plantilla de proyectos y tipos de módulos que cumplen 
con las buenas practicas implementadas en sus proyectos.

.. toctree::
   :maxdepth: 1

   skel_proyectos_python
   skel_proyectos_openerp
   skel_proyectos_plone