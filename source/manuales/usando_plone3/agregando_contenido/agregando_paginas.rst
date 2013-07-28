.. -*- coding: utf-8 -*-

.. _agregando_paginas:


Agregando Paginas
======================

Las paginas en Plone varían considerablemente, pero son una "pagina web" de
un orden u otro.

Para agregar una pagina use el menú *Agregar elemento* en una carpeta:

.. image:: ../images/copy_of_addnewmenu.png
  :alt:
  :align: center

Seleccione **Pagina** en el menú desplegable y usted vera el panel *Agregar
Pagina*:

.. image:: ../images/editpagepanelplone3.png
  :alt:
  :align: center


Los campos **Titulo** y **Descripción** se encuentran en la parte de arriba.
Rellene cada uno de ellos apropiadamente. Hay un campo *Nota sobre el cambio*
al final de la sección, este es también un campo estándar que es muy útil
para almacenar memos útiles que describen los cambios a un documento a medida
que se hacen. Esto es beneficioso para paginas en las cuales puede estar
colaborando con otros.

El panel del medio, **Cuerpo del texto**, es donde esta la acción para las
paginas. El software usado para hacer Paginas en Plone, genéricamente llamado
*editor visual* y específicamente una herramienta llamada *Kupu*, es una
característica muy importante permitiéndole hacer edición WYSIWYG. La edición
WYSIWYG -- del ingles *What You See Is What You Get* que se traduce como "Lo
que ves es lo que obtienes" -- describe como funciona el software de
procesamiento de palabras. Cuando usted hace un cambio, como poner una
palabra en negrita, usted ve el texto en negrita inmediatamente. Lo que usted
ve es el texto en negrita - Plone se encarga de la parte HTML.

La gente generalmente se siente cómoda con la características WYSIWYG de los
procesadores de texto típicos. Nosotros describiremos esto aquí. Su
administrador del sitio también puede habilitar el tan llamado `lenguaje de marcado`_ 
para su sitio.

.. image:: ../images/lights-camera-action_002.png
  :alt: lights-camera-action.png
  :align: center

Ver un vídeo de Plone 2 donde se `usa el editor visual para editar el texto de cuerpo de una pagina`_.


Descripción de la barra de herramientas y iconos en el editor Kupu 1.4.x
------------------------------------------------------------------------

.. note::
    Kupu es una pieza de software incrustada en Plone que se usa como
    editor visual predeterminado -- usted no vera el nombre de Kupu en 
    ningún lado cuando este editando contenidos.

Una barra de herramientas típica de Kupu luce como esta:

.. image:: ../images/image_large.png
  :alt: kupu-grab
  :align: center

El formato de texto es normalmente definido en HTML, pero algunos sitios
ofrecen texto estructurado o otros lenguajes de marcado para edición de
paginas.

Los iconos son:

-   negrita,

-   itálica,

-   alineación a la izquierda,

-   alineación centrada,

-   alineación a la derecha,

-   lista numerada,

-   lista no ordenada,

-   lista de definiciones,

-   disminuir el nivel de la cita a la izquierda (bloque),

-   aumentar el nivel de la cita a la derecha (bloque),

-   insertar imagen (el icono "árbol"),

-   insertar un enlace interno (el icono "cadena"; hace un enlace a otra
    pagina en el mismo sitio),

-   insertar un enlace externo (el icono "mundo"; hace un enlace a una
    pagina web o recurso externo al sitio),

-   insertar anclas (el icono "ancla"; hace un enlace a una sección
    especifica de una pagina web),

-   insertar una tabla (agrega una tabla con filas y columnas),

-   cambiar entre editor visual y vista HTML (el icono "HTML"; si usted
    conoce HTML, edita directamente el HTML de la pagina),

-   y un menú de lista desplegable para estilos de textos.



Imágenes
--------

Coloque el cursor de su ratón sobre el texto de una pagina, luego haga clic
en el icono "árbol". Este panel mostrara una ventana emergente:

.. image:: ../images/image_large_002.png
  :alt: insert-image-current-folder.png
  :align: center

Haga clic en "Carpeta actual" del lado izquierdo del panel, si no esta ya
resaltada. La carpeta actual es la carpeta que contiene la pagina que usted
esta editando -- todas las paginas están contenidas dentro de alguna carpeta.
Hay muchas formas para administrar el almacenamiento de imágenes, incluyendo
el tener una carpeta central de imágenes, pero el método común es almacenar
las imágenes que se muestran en una pagina en la misma carpeta que contiene a
la pagina (la carpeta actual). En este método, las paginas y las imágenes son
asociadas y almacenadas junto con la estructura de la carpeta. Si usted hace
clic en el botón Subir, usted vera una ventana para seleccionar una imagen en
su computadora y subirla. Después de seleccionar una imagen para subir, el
panel derecho le permitirá a usted dar a la imagen un titulo para ser usado
en el sitio web, formas de colocar la imagen y opciones de tamaño. Al hacer
clic en el botón Registrar la imagen se subirá y se cargara en la pagina.

El mismo panel aparecerá si usted hace clic en una imagen en la pagina para
seleccionarla, entonces haga clic al mismo icono "árbol" para editar las
opciones de imagen o para cambiar la imagen.

Usted es responsable de cambiar y editar las imágenes en su computadora antes
de subirlas al sitio, pero una forma fácil de manipular las imágenes para
usarlas en la mayoría de paginas web es hacer una copia de una imagen en su
computadora, luego cambie las dimensiones alrededor de un máximo de 1000
píxeles. Esto es un tamaño razonable para subir -- no es necesario subir sus
imágenes de increíble tamaño que provienen desde su cámara digital. Plone
automáticamente creara varios tamaños de una imagen subida, incluyendo
"grande," "pequeño," y otros tamaños. Usted selecciona el tamaño que quiera
usar cuando suba o edite la imagen con el icono "árbol". Usted también puede
sobreescribir el tamaño de la imagen seleccionado la edición por HTML.


Enlaces Internos
----------------

Seleccione una palabra o frase, haga clic en el icono de *enlaces internos*,
y el panel *insertar enlace* aparecerá:

.. image:: ../images/insertlinkpanel.png
  :alt:
  :align: center

Usted use este panel haciendo clic en Inicio o Carpeta actual para iniciar la
navegación del sitio Web Plone y encontrar una carpeta, pagina, o imagen a la
cual le desea hacer un enlace. En el ejemplo anterior, una pagina nombrada
"Long-tailed Skippers" ha sido seleccionada para el enlace. Después de que
este panel es cerrado, un enlace a la pagina "Long-tailed Skippers" sera
establecido con la palabra o frase seleccionada para este enlace.


Enlaces externos
----------------

Seleccione una palabra o frase, haga clic en el icono de *enlaces externos*,
y el panel Enlace Externo aparecerá:

.. image:: ../images/externallinkpanel.png
  :alt:
  :align: center

Escriba la dirección web del sitio web externo en la caja que inicia con el
prefijo http://. Usted puede hacer clic en el botón *Vista Preliminar* si
necesita verificar la dirección web.  Si usted pega la dirección web,
asegúrese de no duplicar el prefijo http:// al inicio de la dirección.
Entonces haga clic en el botón *Registrar*. El enlace externo sera
establecido en la palabra o frase que usted selecciono.

Anclas
------

Las anclas son como marcadores de posición en un documento, basado en
encabezados, subtítulos, u otros estilos definidos dentro del documento. Como
un ejemplo, para una pagina llamada "Eastern Tiger Swallowtail," con
subtítulos como "Descripción," "Habitat," "Comportamiento," "Estados de
Conservación," y "Literatura," una simple grupo de enlaces a estos subtítulos
(a las posiciones de estos subtítulos dentro del documento) pueden ser
creados usando anclas.

Primero cree el documento con los subtítulos definido en el, y reescriba los
subtítulos en el tope del documento:

.. image:: ../images/anchortext.png
  :alt:
  :align: center


Entonces seleccione cada uno de los subtítulos reescritos en el tope y haga
clic en el icono de anclas para seleccionar los subtítulos:

.. image:: ../images/anchorset.png
  :alt:
  :align: center


Un panel aparecerá para seleccionar a cual subtitulo el enlace de ancla debe
conectarse:

.. image:: ../images/anchorwindow.png
  :alt:
  :align: center

La pestaña *Enlace a ancla* aparecerá. Al lado izquierdo se muestra una lista
de estilos que podrían establecerse dentro del documento. Para este ejemplo,
los subtítulos son usados en cada sección, que es el caso habitual, así que
los subtítulos se han seleccionado. Al lado derecho del panel se muestra los
subtítulos que han sido definidos dentro del documento. Aquí el subtitulo
*Descripción* es seleccionado para el enlace (para la palabra Descripción,
escrita en el tope del documento).

Usted puede ser creativo con esta poderosa característica, al tejer esos
vínculos a anclas dentro de un texto narrativo, mediante el establecimiento
de puntos de anclaje para otros estilos dentro del documento, y de esta
manera crear mezclas eficaces. Esta funcionalidad es especialmente importante
para documentos largos.


Tablas
------

Las tablas son útiles para tabular y listar datos. Para agregar una tabla,
coloque su cursor del ratón donde usted quiera y haga clic en el icono de
*Insertar una tabla*. Usted vera el panel *Tabla*:

.. image:: ../images/inserttablepanel.png
  :alt:
  :align: center

Definir filas y columnas es sencillo. Si usted marca la casilla *Crear
Títulos* usted tendrá un sitio para escribir el encabezado de columna para la
tabla. La Clase de Tabla se refiere a como quiere estilizar la tabla. Usted
tiene opciones como las siguientes:

.. image:: ../images/inserttablepanelclasses.png
  :alt:
  :align: center

Aquí unos ejemplos de estos estilos de tablas:

**plain:**


Thoroughbred Champions
Quarter Horse Champions

Man O' War
First Down Dash

Secretariat
Dashing Folly

Citation
Special Leader

Kelso
Gold Coast Express

Count Fleet
Easy Jet


**listing:**

Thoroughbred Champions
Quarter Horse Champions

Man O' War
First Down Dash

Secretariat
Dashing Folly

Citation
Special Leader

Kelso
Gold Coast Express

Count Fleet
Easy Jet


 Después de que la tabla ha sido creada usted puede hacer clic en una celda
 para mostrar los controles del tamaño de la tabla y los iconos de
 agregar/eliminar filas y columnas:


.. image:: ../images/tableediting.png
  :alt:
  :align: center

En la tabla de arriba, el cursor ha sido colocado en la celda "Special
Leader", la cual activa pequeños controles cuadrados alrededor de los filos
para cambiar la dimensión de la tabla entera. Esto también activa los iconos
de agregar/eliminar para la celda actual: "Special Leader". Haga clic en la
pequeña x dentro del circulo y eliminara la fila entera o la columna que
contenga la celda actual. Haciendo clic en los pequeños iconos de triángulos
laterales agregara una fila arriba o abajo, o una columna a la izquierda o a
la derecha de la celda actual.


Estilos de Texto
----------------

Los estilos de texto son definidos en el menú desplegable. Aquí están las
opciones:

Descripción Ejemplo
Párrafo Normal texto
Encabezado
texto
-----

Subtitulo
texto
-----

Literal ::texto
Sobrio texto
Cita destacada

texto

Resaltado

texto

Salto de pagina (solamente para imprimir)

Flotantes limpios (eliminar estilo)

Resaltar
texto

Como es normal al editar con un procesador de palabra, seleccione una
palabra, frase o párrafo con el cursor de su ratón, luego seleccione uno de
las opciones de estilos desde de la lista del menú desplegable y usted vera
los cambios aplicados inmediatamente.


Guardar
-------

Haga clic en el botón Guardar al final y sus cambios serán hechos en la
pagina.

-----------


Notas de pie de pagina
----------------------

**Lenguajes de marcado**

Si usted es de las personas que le gusta agregar texto usando los llamados
formatos de marcado, usted podría apagar el editor visual en sus preferencias
personales, lo cual remplazara el editor Kupu con un panel simplificado para
ingresar texto. Los formatos de marcado disponibles en Plone son:

-   `Markdown`_
-   `Textile`_
-   `Texto estructurado`_
-   `Texto Reestructurado`_

Cada uno de estos trabaja incrustando códigos especiales de formatos en el
texto. Por ejemplo, con el formato de texto estructurado, al encerrar una
palabra o frase con doble asterisco pondrá la palabra o frase en negrita,
como en **Este texto podría ser negrita**. Estos formatos de marcado merecen
aprenderse para la velocidad de entrada si usted quiere hacer una creación de
bastantes paginas, o si usted es adepto a introducir textos de una manera un
poco mas técnica Algunas personas prefieren estos formatos, no solo por la
velocidad en si, sino por la fluidez de expresión.


.. _lenguaje de marcado: http://plone.org/documentation/manual/plone-3-user-manual/adding-content/adding-pages#footnotes
.. _usa el editor visual para editar el texto de cuerpo de una pagina: http://media.plone.org/LearnPlone/Editing%20Body%20Text.swf
.. _Markdown: http://en.wikipedia.org/wiki/Markdown
.. _Textile: http://en.wikipedia.org/wiki/Textile_%28markup_language%29
.. _Texto estructurado: http://www.zope.org/Documentation/Articles/STX
.. _Texto Reestructurado: http://en.wikipedia.org/wiki/ReStructuredText

