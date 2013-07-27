.. -*- coding: utf-8 -*-

.. highlight:: rest

.. _cuentas_usuarios_y_roles:

Cuentas y roles de usuarios en Plone
=========================================

Los elementos básicos al usar una cuenta de un sitio web Plone, distinción
entre un usuario anónimo y registrado y la descripción de los roles de
usuario.

Los sitios construidos sobre Plone son muy diversos: sitios personales,
sitios de comunidades, organizaciones o negocios con cientos de usuario. Cada
persona que agrega contenido a un sitio Plone debe tener su propia cuenta de
usuario. Una cuenta de usuario esta compuesta de un nombre de usuario y una
contraseña. Algunos sitios Plone permiten que sus visitantes creen sus
propias cuentas mediante el enlace **Registrar** y un formulario que requiere
información de usuario elemental. Otros sitios poseen cuentas que son creadas
por administradores, en cuyo caso las personas suelen recibir mensajes de
correo electrónico con los detalles de la cuenta de usuario.

Una vez creada la cuenta de usuario Plone, esta le permite a una persona
acceder al área de administración de contenido ingresando su nombre y
contraseña. Las contraseñas son sensibles a mayúsculas y minúsculas. Esto
significa que hay que prestar atención al momento de escribir la contraseña
porque no es lo mismo escribir una letra en mayúscula o minúscula. Por
ejemplo, si la contraseña es xcFGt6v hay que escribirla exactamente de ese
modo, caso contrario no se podrá lograr el acceso. En general se recomienda
emplear contraseñas que tengan distintos caracteres sobre contraseñas como
"raccoon" o "boardwalk" porque son mas complejas de descubrir y por lo tanto
son mas seguras.


Navegación de usuario registrado versus usuario anónimo
-------------------------------------------------------

La distinción entre *la navegación de usuarios anónimos* y la *actividad web
autenticada (registrado)* es muy importante:


Navegación de usuario anónimo
-----------------------------

     Esta es la manera normal en que una persona navega la web. Usted
     escribe la dirección del sitio en el navegador y observa las paginas
     web, ve vídeos e imágenes y no requiere iniciar sesión.. Por este motivo
     es llamado anónimo: cualquier persona puede navegar el sitio sin dar a
     conocer su identidad. Note la presencia del enlace *Entrar (Log in)* en
     la parte superior derecha de la siguiente figura. Si un sitio Plone
     muestra el enlace *Entrar (Log in)*, esto significa que el usuario no ha
     iniciado sesión, y el usuario esta navegando de forma anónima, como se
     muestra en la siguiente figura de un sitio Plone nuevo:

     .. image:: images/plonemain3.png
       :alt: Navegación de un sitio Plone como usuario anónimo
       :align: center


Actividad web autenticada (registrado)
--------------------------------------

     Usted puede estar familiarizado con el modo *autenticado*, por
     ejemplo, es el que emplea el sitio web de un banco, tarjeta de crédito,
     o cualquier otro sitio web que requiere una cuenta de usuario. El sitio
     web de un banco permite ver información sobre su cuenta, llenar
     formularios, transferir fondos y otras acciones, siempre y cuando haya
     iniciado sesión. Un sitio Plone no es muy diferente, con la diferencia
     que se pueden hacer cosas mas sofisticadas. Observe la siguiente imagen,
     el usuario "John Smith" ha iniciado su sesión. Cerca de la parte
     superior derecha usted puede ver enlaces para el nombre John Smith y
     salir de la sesión. Otra diferencia importante posterior al inicio de
     sesión -- sobre el cuerpo principal ahora aparece un encabezado verde
     con pestañas. Estas pestañas aparecen cuando un usuario tiene
     suficientes privilegios para modificar un área del sitio web. John Smith
     tiene los permisos para cambiar esta área principal. Las pestañas en el
     encabezado verde para el área principal variaran un poco, pero usted
     puede contar con que se parece a una interfaz con pestañas de este color
     verde particular. En la siguiente figura, el usuario John Smith ha
     iniciado sesión dentro de un nuevo sitio web Plone:

    .. image:: images/plonemain3_002.png
      :alt: Navegación de un sitio Plone como usuario registrado
      :align: center


Roles de usuario
----------------

La distinción entre los diferentes roles de usuarios es muy importante en un
sitio web Plone. Para ilustrar el caso mas simple, considere los dos roles de
usuarios, uno llamado *miembro* y otro llamado *administrador*. Estos roles
tienen diferentes privilegios o "poderes":


Miembro
-------

-   posee una cuenta de usuario y por ello puede iniciar sesión
-   puede agregar contenido, pero solamente en áreas especificas y no
    puede cambiar nada fuera de estas. A menudo a los usuarios se les otorga
    un "área base", para ser tratada como espacio personal donde pueden
    agregar contenido.
-   no pueden publicar contenido, lo que significa que no es visible a
    visitantes anónimos, incluso el mismo contenido que ellos agregaron. Una
    persona con el rol de Administrador debe aprobar el contenido para que
    sea publicado.



Administrador
-------------

-   posee una cuenta de usuario y por ello puede iniciar sesión
-   puede agregar contenido en cualquier parte del sitio y tiene
    privilegios para cambiar cualquier cosa
-   puede publicar cualquier contenido

Cuando usted obtiene una cuenta nueva en un sitio web Plone, se le debería
dar información de las áreas donde tiene privilegios para agregar contenido
una vez haya iniciado sesión. Si esto ocurre y el usuario abre la carpeta
donde tiene tales privilegios, en la parte superior del contenido se deben
visualizar pestañas de color verde con los nombres *Contenidos*, *Vista*,
*Editar*, Reglas, *Compartir*, e *Historia*:

.. image:: images/editstriptabs.png
    :alt: Pestañas
    :align: center


Si se hace clic en ellas es posible explorar las diferencias entre una y
otra, de todas maneras aquí están las descripciones para ayudarlo a empezar:

-   *Contenidos* - muestra una lista con los elementos que contenidos en
    la carpeta

-   *Vista* - muestra la vista que un usuario anónimo visualizara

-   *Editar* - cambia el panel a una vista de edición

-   *Reglas* - muestra un panel para controlar como son creados y
    administrados los elementos

-   *Compartir* - muestra un panel para establecer permisos para que
    otros usuarios puedan ver y editar el contenido
-   *Histórico* - muestra la bitácora de cambios realizados en un
    elemento


Debajo de las pestañas en la parte baja del encabezado verde puede ver varios
menús *Mostrar, Agregar elemento y Estado*:

.. image:: images/editstripmenus.png
    :alt: Menús
    :align: center

Explore estos también. Aquí están las descripciones básicas de estos menús:

-   *Mostrar* - permite seleccionar el tipo de vista (lista de elementos,
    vista de resumen, etc.)

-   *Agregar elemento* - muestra un menú con los diferentes elementos de
    contenidos que se pueden agregar (imágenes, paginas, carpetas, etc.)

-   *Estado* - permite cambiar el estado de publicación del elemento
    actual (privado, borrador publico, publico, etc.)

Estos menús y pestañas son los medios principales para interactuar con Plone.
A medida que usted aprenda mas sobre administrar un sitio web Plone, mas
familiar le resultaran los procesos.

