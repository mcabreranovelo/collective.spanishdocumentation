.. -*- coding: utf-8 -*-

.. _agregando_nuevo_contenido:

Agregando Nuevo Contenido
==============================

Una descripción general de como agregar nuevos elementos de contenidos en
Plone, incluyendo definiciones de cada tipo de contenido estándar.

Los nuevos contenidos son agregados vía el menú desplegable **Agregar elemento**:

.. image:: ../images/image_preview.png
  :alt: addnew_image.gif
  :align: center

Agregar contenido en Plone se hace de manera *agradable*, lo que quiere
decir que usted debe navegar a la sección de su sitio web Plone en donde
quiere que el nuevo contenido resida antes de usar el menú desplegable
**Agregar elemento**. Por supuesto usted puede cortar, copiar y pegar
elementos de contenido desde una sección a otra si es necesario.

Tipos de Contenido
------------------

En Plone, usted puede usar un numero de **Tipos de Contenido** para publicar
ciertos tipos de contenido. Por ejemplo, para subir una imagen usted puede
usar el tipo de contenido **Imagen**. La siguiente es una lista de tipos de
contenidos disponibles en el orden de su aparición, y para que se usa cada
uno:

.. glossary::

  Colección
    Las Colecciones son usadas para agrupar y mostrar contenido basado
    en una serie de **criterios** los cuales puede definir. Estas trabajan 
    como una consulta a una base de datos.

  Evento
    Un evento es un tipo de contenido como una pagina especial para
    publicar información acerca de un evento (como una recaudación de 
    fondos, parrillada, etc). Este tipo de contenido tiene una función 
    que le permite al visitante del sitio agregar el evento a su calendario 
    de escritorio con el estándar iCal o vCal. Este formato es soportado 
    por aplicaciones como: Google Calendar, Outlook, Sunbird y otros.
    
    Para agregar un evento a su calendario, haga clic en el enlace vCal o 
    iCal al lado del texto "Agregar evento al calendario" en la vista principal 
    de un elemento de evento.
    
    .. image:: ../images/image_preview.jpeg
      :alt: Tabla resumen de Eventos
      :align: center
    
    Desde Plone 3.3 usted puede obtener también todos los eventos en una carpeta
    en un solo paso (actualmente solo disponible en formato iCal). Para descargar
    el archivo iCal, agregue *@@ics_view* al final de la dirección URL de la
    carpeta que contiene los eventos. Por ejemplo, si usted quiere obtener todos
    los eventos dentro de la carpeta *Eventos* en el raíz de su sitio, vaya a
    *http://misitio.com/events/@@ics_view*. Hay maneras para proveer un enlace a
    este calendario iCal dentro de la Interfaz de usuario en futuras publicaciones.

  Archivo
    Un archivo en Plone es cualquier archivo binario que usted desee subir 
    con la intención de que este sea descargado por los visitantes de su 
    sitio. Ejemplos comunes son archivos PDF, Documentos de ofimática como 
    MS Word y Hojas de Calculo.

  Carpeta
    La carpetas trabajan en Plone muy parecido a como lo hacen las
    carpetas en su computadora. Usted puede usar carpetas para organizar 
    su contenido, y dar a su sitio web Plone una estructura de navegación.

  Imagen
    El tipo de contenido Imagen es usado para subir archivos de imagen
    (JPG, GIF, PNG) que usted puede insertarlas dentro de paginas u otro 
    tipos de contenidos de tipo pagina.

  Enlace
    También asociado como el 'Objeto enlace'; no confundirlos con los
    enlaces que usted crea vía Kupu, editor visual de paginas Plone. 
    El tipo de contenido Enlace es regularmente usado para incluir un 
    enlace a un sitio web externo en la navegación y otros usos 
    especializados.

  Noticia
    Este tipo de contenido es similar al Evento, solamente que estos
    elementos son especialmente para publicar noticias. Usted puede 
    también adjuntar una imagen miniatura a una Noticia, la cual 
    aparecerá en la vista de resumen en la carpeta al lado del resumen 
    de la Noticia.

  Pagina
    Una Pagina en Plone es uno contenidos disponibles mas simples. 
    uselas para escribir la mayor parte de sus paginas web en el 
    sitio Web Plone.

.. note::
    Dependiendo de que productos adicionales tenga usted instalado, tendrá
    mas opciones en su menú desplegable **Agregar elemento** de las que
    aparecen aquí. Para mas información acerca de esos tipos de contenidos
    adicionales, consulte la documentación del Producto adicional a utilizar.


Titulo
------

Todos los tipos de contenidos en Plone tiene dos campos en común: **Titulo**
y **Descripción.**

El **Titulo** de los elementos de contenido, incluyendo carpetas, imágenes,
paginas, etc., puede ser cualquier cosa que usted quiera -- puede usar
cualquier carácter del teclado, incluyendo espacios. Los **Títulos** son
parte de la dirección web para cada elemento creado en Plone. La dirección
web, también conocida como URL, son las escritas en el navegador web para ir
a una ubicación especifica en un sitio web (o navegando a través del sitio),
como:

www.misitio.com/acerca/personal/sally/bio

o

www.misitio.com/imágenes/mariposas/skippers/long-tailed-skippers

Las direcciones web *si* tienen restricciones sobre los caracteres del
teclado permitidos, y los espacios no son permitidos. Plone hace el buen
trabajo de mantener las direcciones web correctas mediante el uso de
direcciones muy similares al **Titulo** que usted eligió, convirtiéndolas a
minúsculas, y sustituyendo guiones por espacios y otras puntuaciones.

En Plone nos referimos a la dirección web de un elemento como **nombre
corto**. Cuando usted use la función **Renombrar**, usted puede ver el nombre
corto junto con el titulo.

Los campos variaran en relación al tipo de contenido. Por ejemplo, el tipo de
contenido Enlace tiene el campo de dirección URL. El tipo de contenido
Archivo tiene el campo de Archivo, así continua con todos los campos.

Descripción
-----------

La **Descripción** aparece al tope de las paginas, justo abajo del Titulo.
Las descripciones regularmente son usadas en conjunción con una variante de
vistas de Carpeta y Colección (como un Estándar o Resumen). La Descripción
también aparece en los resultados de búsquedas vía el motor de búsqueda
nativa de Plone.

