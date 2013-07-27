.. -*- coding: utf-8 -*-

.. highlight:: rest

.. _diseno_visual_de_plone:

Diseño visual de los sitios web Plone
==========================================

Plone permite a diseñadores y administradores crear diseños únicos para sus
sitios. En esta sección se hace un breve recorrido por el esquema de Plone y
algunos ejemplos de diseño.

¿Como luce un sitio web hecho con Plone?. Desde hace varios anos existe un
diseño consistente para la apariencia por defecto de Plone. El diseño por
defecto generalmente se parece a lo siguiente:

.. image:: images/plone-default-design-areas.png
    :alt: Áreas de diseño por defecto de Plone
    :align: center

Aunque un sitio Plone puede tener un diseño radicalmente distinto a este,
igual debería identificar los elementos comunes, como por ejemplo el enlace
de entrar, un panel de navegación o un menú. En el diseño por defecto, el
menú de navegación esta a la izquierda y usualmente muestra una lista de
carpetas. También puedo haber un grupo de pestañas *Entrar, información sobre
la ubicación* en la franja de la parte superior.

Es posible distinguir entre el *diseño* de un sitio web y su *funcionalidad*.
Para realmente realizar el trabajo, concentrese en la funcionalidad y no se
preocupe demasiado por la apariencia y diseño del sitio web. Una fortaleza
del sistema de contenidos de Plone, es que un sitio web puede ser
radicalmente rediseñado sin afectar al contenido ni funcionalidad. El menú de
navegación puede moverse de izquierda a derecha y funcionara del mismo modo.
El área de la derecha puede eliminarse ya que normalmente la funcionalidad
que se le da a esta no es necesaria. Las áreas de la izquierda, principal, y
derecha, tal como se describe arriba y abajo, pueden cambiarse a la parte
superior, media, e inferior, y aun así debajo de todo esto seguiría siendo un
sitio web Plone.

Usaremos el diseño por defecto de Plone como ejemplo de una división típica
de pantalla:

.. image:: images/plonedefaultareaslabeled.png
    :alt: Áreas por defecto de etiquetada de Plone
    :align: center


Usted tal ves requiera adaptar estos términos (áreas) según sea necesario
para el diseño de su sitio web Plone. Seguramente se usaran términos (áreas)
variados para describir el diseño real del sitio, como por ejemplo, los
"slots" o paneles izquierdo y derecho para las columnas laterales. Los
"portlets" o "viewlets" para las áreas discretas o "cajas", entre otros.

A modo de ejemplo, se seleccionara tres sitios para comparar tomados de la
`lista de sitios web Plone`_:

.. image:: images/akamaidesign.png
    :alt: Diseño de Akamai
    :align: center

En la figura, se muestra el sitio de Akamai, un líder proveedor de
herramientas y tecnologías de aceleración web. El encabezado posee un simple
menú con enlaces que lista horizontalmente a las cinco secciones principales
de contenido. A la derecha, el encabezado posee otro menú horizontal y un
cuadro de búsqueda. Al pie del encabezado se muestra la opción para entrar al
sitio, opción empleada por los responsables del mismo. Debajo del encabezado
y a la izquierda, hay un área para gráficos llamativos y temas actuales. El
área principal en el centro a la izquierda se encuentra el texto principal.
La columna derecha contiene una serie de "portlets." El pie de pagina posee
un menú horizontal con las mismas opciones del encabezado convenientemente.
Por ultimo, a la derecha hay una columna con opciones de zoom.

.. image:: images/discoverdesign.png
    :alt: Diseño de Discover Magazine
    :align: center

Este es el sitio web de Discover Magazine. El área de encabezado contiene un
extenso menú horizontal o si se quiere "menú principal," en la esquina
superior derecha hay otro menú y un cuadro de búsqueda. Este sitio posee un
gran numero de "portlets" de texto que cubren diferentes temas, los cuales
están agrupados en tres columnas, izquierda, centro y derecha. En la parte
superior de la columna del centro hay un área con un vídeo. Y en diferentes
partes del sitio abundan cuadros interactivos. El pie de pagina contiene
información básica sobre la identificación y un enlace a "acerca de". En
sitios complejos como lo es la revista Discover, los responsables de
contenido entran mediante pantallas de edición personalizadas y hay una gran
automatización de flujos de datos - Plone esta construido sobre Zope, un
sistema sofisticado de almacenamiento, y Python un excelente lenguaje de
programación que facilita mucho "cableado" inteligente de flujo de texto y
gráficos en el sitio web.

.. image:: images/smealdesign.png
    :alt: Diseño de Penn State University's Smeal College of Business
    :align: center

El ultimo ejemplo para examinar de los tres sitios web es el de Penn State
University's Smeal College of Business (Escuela de Negocios Smeal de la
Universidad Estatal de Pensilvania) El encabezado contiene un logotipo, un
menú horizontal para las áreas principales y un cuadro de búsqueda a la
derecha. El sitio posee un menú principal a la izquierda, el cual es uno de
los elementos mas tradicionales en sitios web Plone. Una área grande que
contiene una animación móvil. Y otro gráfico pequeño en la columna izquierda.
Hay tres columnas textuales que completan el diseño arriba del pie de pagina
de identificación. Los responsables de este sitio web acceden a través de una
pagina de inicio de sesión personalizada, con la sesión y información del
usuario mostrados en la parte inferior del área de encabezado superior.

Para concluir, ¿como luce un sitio web hecho en Plone?, Tradicionalmente,
recién instalado luce como se mostró en las primeras figuras de esta pagina,
con encabezado, menú, columnas y pie de pagina. Los tres sitios mostrados,
son ejemplos de como los diseñadores pueden combinar distintas áreas, menús
horizontales y verticales, "portlets", contenido textual, ubicados
generalmente en una serie de columnas. La maquinaria base es Plone, sobre
Zope y Python, pero el diseño llamado "tema" o "skin" puede modificarse para
que luzca en la forma que quiera el diseñador.

.. _lista de sitios web Plone: http://plone.net/sites
