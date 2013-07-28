.. -*- coding: utf-8 -*-

.. _definiendo_propiedades_basicas:

Definiendo Propiedades Básicas
====================================

Las pestañas disponibles para cada elemento de contenido poseen campos para
información básica. Proveer estos datos es importante, ya que es
"combustible" para los motores que ejecutan Plone.

Cuando el usuario con permisos de edición para elementos hace clic en
cualquier elemento de contenido, estos mostraran una serie de pestañas en el
tope para definir propiedades básicas:

.. image:: ../images/basicpropertiestabs.png
  :alt:
  :align: center


Las pestañas de propiedades básicas son:

-   *Predeterminado* - muestra el panel de entrada de datos principales
    para el elemento de contenido
-   *Categorización* - muestra un panel para crear y definir categorías
    (palabras claves) para el elemento
-   *Fechas* - muestra la Fecha de Publicación y la Fecha de Terminación
    para el elemento
-   *Propietario* - muestra un panel para definir los usuarios creadores,
    colaboradores, y cualquier información de derechos de autor para el
    elemento
-   *Configuración* - Muestra un pequeño panel para establecer si el
    elemento aparecerá o no en los menús de navegación y si se permiten
    comentarios sobre el mismo.


Los campos de entrada de estas pestañas comprenden la información descriptiva
básica llamada **metadatos**. Los Metadatos son a veces llamados "datos
acerca de datos." Plone puede usar este metadato de múltiples de formas.

Acá vemos el panel *Categorización*, mostrado en el elemento de contenido de
pagina (podría ser el mismo para otros tipos de contenidos):

.. image:: ../images/editpagecategorization.png
  :alt:
  :align: center


.. note::
    *Las categorías fueron formalmente llamadas palabras claves en Plone, 
    previo a la version 3.0.*

El campo principal de entrada en el panel sirve para especificar
*categorías*. Para crearlas nuevamente, simplemente introduzca palabras o
frases, una por linea, en la caja **Categorías nuevas**. Cuando usted
presiona el botón Guardar, las nuevas categorías serán creadas en el sistema
de categorías para el sitio web, y este elemento de contenido sera asociado
bajo estas. Si usted re-edita este elemento, o edita cualquier otro, la nueva
categoría se mostrara como **Categorías actuales**.

El campo *Elementos Relacionados* le deja establecer enlaces entre elementos
de contenido, que se muestran en la parte inferior cuando un elemento de
contenido es visualizado. Esto es útil cuando no quiere usar categorías
explicitas para conectar contenidos.

El campo *Localización* es una ubicación geográfica, adecuado para ser usado
con sistemas de información geográficas, pero apropiada también para mantener
un registro general.

La selección del *Idioma* normalmente se trata de incorporar para que, el
seleccionado, concuerde con la configuración por defecto del sitio, pero en
paginas web multilingües, idiomas diferentes podrían ser usados para una
mezcla de contenidos.

El panel *Fechas* tiene campos para la Fecha de Publicación y para la Fecha
de Terminación, y efectivamente fecha de inicio y culminación para el
contenido si usted las desea establecer:

.. image:: ../images/datessettings.png
  :alt:
  :align: center


El panel *Propietario* tiene tres campos de estilo libre para listar a los
creadores, colaboradores, e información acerca de los derechos de autor o los
derechos de propietario del contenido:

.. image:: ../images/ownershipsettings.png
  :alt:
  :align: center


El panel de *Configuración* tiene campos que tal vez varíen un poco de un
tipo de contenido a otro, pero generalmente hay campos que controlan si los
elementos aparecen o no en la navegación, si los comentarios son permitidos,
y otros controles similares:

.. image:: ../images/settingspanel.png
  :alt:
  :align: center


Recomendaciones
---------------

No hay requerimientos para ingresar la información especificada a través de
estos paneles, pero es muy buena idea hacerlo. Para el panel de
*Propietario*, proveer los datos es importante para las situaciones donde hay
muchas personas involucradas en la creación del contenido, especialmente si
hay múltiples creadores y colaboradores trabajando en grupos. Usted no
necesita siempre campos como los usados para Fechas de Publicación y
Terminación, idioma, y derechos de autor, pero estos datos podrían ser
especificados cuando sea el caso apropiado. Un sistema de gestión de
contenidos sera tan bueno como la plenitud de sus datos permita.

Especificar categorías requiere atención, pero si usted es capaz de crear el
habito y realmente comprometerse a la creación de un conjunto significativo
de categorías, tendrá una inversión que devolverá grandes ganancias. La
devolución sucede a través del uso de búsquedas y otras facilidades en Plone
que desactiva la categorización. Lo mismo se aplica para el establecimiento
de elementos relacionados. Usted podrá poner sus manos a la obra en lo que
necesite, y podrá ser capaz de descubrir y usar relaciones que hayan dentro
de los contenidos.

