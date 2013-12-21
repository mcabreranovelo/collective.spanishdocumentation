.. -*- coding: utf-8 -*-

.. _cambiar_favicon_default:

===========================================
Cambiar el favicon.ico por defecto de Plone
===========================================

:Autor(es): Leonardo J. Caballero G.
:Correo(s): leonardocaballero@gmail.com
:Compatible con: Plone 3, Plone 4
:Fecha: 20 de Diciembre de 2013

Como cambiar el `icono`_ (`favicon`_) que muestra por defecto en la pestaña
del navegador de `Mozilla Firefox`_ o de la barra de dirección `Internet Explorer`_ 
cunado los usuarios visitan un sitio Plone.

1.  ­Crear una imagen en `formato PNG`_ de 16 x 16 (ya que se ve bien en
    16 x 16).

2.  Entonces convierta esta a un archivo .ico de 16x16  (Yo uso 
    `GIMP para crear los iconos`_)

3.  Coloque el archivo :file:`favicon.ico` dentro de su carpeta 
    **/portal_skins/custom/** a través de la interfaz de Plone en 
    :menuselection:`Configuración del Sitio --> Interfaz de Administración de Zope --> portal_skins --> custom`
    estando en este directorio, haga clic en la lista desplegable ubicada a mano derecha debajo de las
    pestañas de navegación de la *Interfaz de Administración de Zope*,
    seleccione **Image**.

    .. image:: select_add_image.png
        :align: center
        :alt: Seleccionar Imagen para el favicon

4.  Luego muestra la ventana llamada **Add Image** donde debe hacer
    clic en la caja de texto **id** y agregue el valor :file:`favicon.ico`,
    posterior haga clic en el botón **Browse...**, examine el archivo
    :file:`favicon.ico` en su sistema de archivo y luego haga clic en **Aceptar**,
    por ultimo haga clic al botón **Add** (usted también puede colocarlo en
    una carpeta adecuada de un sistema de archivos basado en skin).


    .. image:: add_image_favicon.png
        :align: center
        :alt: Ventana para colocar el archivo favicon


Usted necesitara forzar una recarga del navegador empleado para ver la página
antes de poder apreciar los cambios, tenga en cuenta borrar los archivos
temporales de su navegador y la cache (también tenga en cuenta que algunos navegadores 
no soportan el comportamiento de favicon).

.. image:: favicon_screenshot.jpg
    :align: center
    :alt: Screenshot showing custom Favicons for various sites

Usted puede colocar un archivo :file:`favicon.ico` personalizado en su skin de plone.
Un favicon será mostrado en sus pestaña de navegación y en la barra de
direcciones de su navegador.


Referencia
==========

- `Cambiar el favicon.ico por defecto de Plone`_ desde la comunidad Plone Venezuela.
- `Setting the site icon (favicon) for your Plone Site`_.


.. _icono: http://es.wikipedia.org/wiki/Icono_%28inform%E1tica%29
.. _favicon: http://es.wikipedia.org/wiki/Favicon
.. _Mozilla Firefox: http://es.wikipedia.org/wiki/Mozilla_Firefox
.. _Internet Explorer: http://es.wikipedia.org/wiki/Internet_Explorer
.. _formato PNG: http://es.wikipedia.org/wiki/PNG
.. _GIMP para crear los iconos: http://www.desarrolloweb.com/articulos/video-crear-icono-favicon-gimp.html
.. _Cambiar el favicon.ico por defecto de Plone: http://www.coactivate.org/projects/ploneve/cambiar-el-favicon-ico-por-defecto-de-plone
.. _Setting the site icon (favicon) for your Plone Site: http://plone.org/documentation/kb/setting-the-site-icon-favicon-for-your-plone-site