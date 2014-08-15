.. -*- coding: utf-8 -*-

.. highlight:: rest

.. _resumen_conceptual:

Resumen conceptual
=======================

Una explicación de Plone como sistema de gestión de contenidos


¿Qué es Plone?
--------------

Plone es un sistema de gestión de contenidos (del inglés, Content Management
System - CMS) que puede emplearse para construir un sitio web. Empleando
Plone, las personas sin conocimientos de programación o sin la ayuda un
experto pueden contribuir al contenido de un sitio web. Plone funciona vía
web, por lo tanto no necesita instalar ningún software especializado en la
computadora del cliente. La palabra *contenido* es usada en un sentido
general ya que usted puede publicar distintos tipos de información,
incluyendo:

.. figure:: ../images/content_types_into_plone.png
    :align: center
    :alt: Tipos de contenidos dentro de Plone


Un sitio web Plone contiene diferentes tipos de contenido, incluyendo textos,
fotos e imágenes. Estos pueden ser almacenados en diferentes formas:
documentos, noticias, eventos, vídeos, archivos de audio y cualquier tipo de
archivo que pueda ser subido o creado en un sitio web. El contenido también
puede subirse desde una computadora local, además, Plone le permite crear
*carpetas* para organizar el contenido y crear una estructura de navegación:

.. image:: ../images/content_is_added_to_folders.png
    :align: center
    :alt: Contenido es agregado en carpetas



¡Usted adora las mariposas!
---------------------------

Si se deseara agregar contenido sobre mariposas, por ejemplo, se puede crear
una carpeta llamada "Mariposas" y luego agregar texto a una página dentro de
la carpeta:

.. image:: ../images/butterflies_folder_text.png
    :alt: Texto de Carpeta Mariposas
    :align: center


También se pueden agregar algunas imágenes a la carpeta:

.. image:: ../images/butterflies_folder.png
    :alt: Carpeta Mariposas
    :align: center


Dentro de una carpeta usted puede agregar muchos contenidos de distintos
tipos, incluyendo sub-carpetas. Luego de agregar algunos reportes y vídeos a
la carpeta Mariposas, el contenido debería estar organizado como se muestra a
continuación, con dos sub-carpetas dentro de la carpeta Mariposas:

.. image:: ../images/folders_within_folders.png
    :alt: Carpeta en carpeta
    :align: center


¿Qué ocurre tras bambalinas?
----------------------------

Es probable que el lector se pregunte cómo funciona todo. Un sitio Web Plone
típico existe como una instalación de Plone instalada en un servidor web. El
servidor web puede estar en cualquier sitio, usualmente en una compañía de
hospedaje con una "pila" de computadoras dedicadas a realizar la tarea:

.. image:: ../images/server_rack.png
    :alt: Rack del servidor
    :align: center


El diagrama muestra los cables que conectan los servidores individuales a
internet, a través de rápidas conexiones de red. Su sitio Plone es solo un
software y almacenamiento de base de datos instalados en uno de los
servidores individuales. Cuando introduce texto o hace clic en algún lugar del sitio, la computadora
del usuario envía y recibe datos a través de cables de red y canales de
comunicación en internet que interactúan con la instalación de Plone en el
servidor.

Simplifiquemos el diagrama que muestra como se interactúa con Plone:

.. image:: ../images/client_to_server_simple.png
    :alt: Del cliente al servidor
    :align: center


Usted usa su navegador web; Mozilla Firefox, Safari, Internet Explorer, etc.
-- para ver y editar su sitio web Plone, y éste guarda los cambios realizados
en su sistema de almacenamiento de bases de datos.

Por ejemplo, imagine que su sitio web Plone de Mariposas esta ubicado en el
sitio misitio.com. Usted escribe www.misitio.com en su navegador web. Luego
presiona la tecla Enter, la siguiente secuencia de eventos es llevada a cabo
entre el navegador y el servidor de www.misitio.com:

.. image:: ../images/client_request.png
    :alt: Solicitud del cliente
    :align: center

Luego el software Plone responde:

.. image:: ../images/server_response.png
    :alt: Respuesta del servidor
    :align: center


Plone lee su respectiva base de datos para buscar la información almacenada
en misitio.com. Luego envía de vuelta la página web a su computadora en un
código llamado HTML que es un lenguaje de computadora que describe con luce
una página web. Este incluye texto, gráficos, tipos de letras, color del
fondo, etc. En Internet existen muchos sitios donde se puede aprender HTML
detalladamente, pero una de las ventajas de Plone es que no es necesario
aprender (demasiado) sobre HTML. Esa es una de las razones por la que Plone y
otros software similares permiten al usuario concentrarse en el contenido,
por ejemplo, el texto y los gráficos de las mariposas en vez de aprender un
nuevo lenguaje de computadoras.

Pero regresemos a la interacción entre la computadora del usuario y el
servidor. El navegador web "suministra" (traduce) este HTML para que pueda
ver la página web resultante:

.. image:: ../images/my_site_served.png
    :alt: Mi sitio servido
    :align: center


Así que cuando ve su página web de mariposas, puede decidir si cambiarla o
agregarle contenido. Además en cualquier momento se puede subir fotos,
documentos, etc:

.. image:: ../images/plone_donut.png
    :alt: 
    :align: center


Luego que hace sus cambios y hace clic en "Guardar", la nueva versión de la
página web se mostrará a cualquiera que visite el sitio:

.. image:: ../images/plone_donut_full.png
    :alt: 
    :align: center

