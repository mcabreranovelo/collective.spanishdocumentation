.. -*- coding: utf-8 -*-

.. _plone:

Sistema de gestión de contenidos Plone
======================================

:Autor(es): Leonardo J. Caballero G.
:Correo(s): leonardocaballero@gmail.com
:Fecha: 31 de Diciembre de 2013

.. _ficha_tecnica_plone:

.. sidebar:: Ficha técnica

    :Desarrollador: **El equipo de Plone** http://plone.org/
    :Diseñador: Alan Runyan, Alexander Limi, Vidar Andersen.
    :Lanzamiento: `2001`_.
    :Ver. estable: 4.3.2 [#cite_note-1]_, 15 de abril de 2013.
    :Ver. pruebas: 4.3 [#cite_note-2]_, 15 de abril de 2013.
    :Género: `CMS`_.
    :Programado en: `Python`_, `XML`_, `JavaScript`_.
    :Sistema base: `Multiplataforma`_, `Mac OS X`_, `GNU/Linux`_, `Windows`_, `BSD`_, `Solaris`_.
    :Plataforma: `Zope`_.
    :Licencia: `GPL`_.
    :Estado actual: Estable.
    :Idiomas: 60.
    :En español: Sí.

.. _que_es_plone:

¿Qué es Plone?
==============

**Plone** es un `sistema de gestión de contenidos`_ que puede utilizarse para 
construir cualquier tipo de `sitio web`_ como portales, sitios webs corporativos, 
sitios web `externos`_ o `internos`_, sitios de publicación de noticias, incluyendo 
`blogs`_, `tiendas en línea`_ (E-commerce), como repositorio de documentos y 
`herramienta colaborativa`_. [#cite_note-3]_

Plone es un desarrollo basado en `código abierto`_ publicado bajo la `GNU General Public License`_ 
(GPL), basado en `Zope`_ y programado en `Python`_. Los principales desarrollos son 
conducidos periódicamente durante `reuniones especiales`_ llamadas `Plone Sprints`_. 
Adicionalmente esta diseñado para extender sus funcionalidades por defecto por medio 
de módulos adicionales llamados :ref:`Products <productos_plone>`. Pone también tiene 
respaldo legal del Consejo de la `Software Freedom Law Center`_. Los puntos fuertes de 
Plone son sus flujo de trabajo `flexibles y adaptables`_, muy buena seguridad, extensibilidad, 
facilidad de uso y flexibilidad.

Según estudio efectuado por `Real Story Group`_ llamado **2012 Content Technology Vendor Map** [#cite_note-4]_ 
clasifican a Plone como un `Document & Records Management`_, `Sistema de gestión de contenidos`_ y 
`Gestión del conocimiento`_ *(Web Content & Experience Management)*, `Software colaborativo`_ y `Software social`_ 
*(Collaboration & Social Software)*. 

Aparte de este estudio, existen publicaciones donde se ha analizado sus capacidades como 
Sistema de `Gestión de Conocimiento`_ [#cite_note-5]_.

Debido a la su capacidad de extender su funcionalidad por defecto basado en 
:ref:`Productos <productos_plone>`, existe experiencias realizadas por 
proveedores de servicios de Plone donde frecuentemente han utilizado a Plone 
como `CRM`_, [#cite_note-6]_ [#cite_note-7]_ como un `software GIS`_ 
para `cartografía en entornos web`_, [#cite_note-8]_ [#cite_note-9]_ entre 
otros usos, aun cuando Plone no fue diseñado como tal para estas funcionalidades.


Historia
--------

El proyecto Plone comenzó en 1999 por Alan Runyan, Alexander Limi, y Vidar 
Andersen. Se hizo como una capa de usabilidad en la parte superior del 
`Zope Content Management Framework`_. La primera versión (**Plone 1.0**) 
fue lanzada en 2001 [#cite_note-10]_. El proyecto se convirtió rápidamente 
en una comunidad, recibiendo un montón de nuevos productos complementarios 
de sus usuarios. El aumento de la comunidad condujo a la creación de la 
conferencia anual de Plone en 2003, [#cite_note-11]_ que todavía se sigue 
realizando en la actualidad [#cite_note-12]_. Además, se llevan a cabo los 
llamados "`Sprints`_", donde grupos de desarrolladores se reúnen para trabajar 
en Plone, que van desde un par de días a una semana.

En marzo de 2004, **Plone 2.0** fue lanzado [#cite_note-13]_. Esta versión 
trajo más características personalizables a Plone, y ampliado las funciones 
:ref:`add-on <productos_plone>`. En mayo de 2004, la :ref:`Fundación Plone <fundacion_plone>` 
fue creada. El 12 de marzo de 2007, **Plone 3** fue lanzado [#cite_note-14]_. 
Hasta septiembre de 2007, ha habido más de 200 desarrolladores que contribuyen 
al código fuente de Plone alrededor del mundo.

Esta nueva versión trajo la edición en línea, el editor mejorado visual, y 
fortalecimiento de la seguridad, entre muchas otras mejoras. En septiembre 
de 2010 fue lanzado **Plone 4** [#cite_note-15]_. Plone ganó dos el reconocimiento 
del **Packt Open Source CMS Awards** [#cite_note-16]_.

Histórico de publicaciones
~~~~~~~~~~~~~~~~~~~~~~~~~~

Las versiones estable de Plone están disponibles en `http://plone.org/products/plone`_

+-------------------+--------------+---------------------------------------+-----------------------------+
| Versión estable   | Fecha ISO    | Aproximadamente diferencia en meses   | Notas                       |
+===================+==============+=======================================+=============================+
| 0.1               | 1999         | --                                    | Inicio del proyecto Plone   |
+-------------------+--------------+---------------------------------------+-----------------------------+
| 1.0               | 2003-02-06   | --                                    | Primera versión estable     |
+-------------------+--------------+---------------------------------------+-----------------------------+
| 2.0               | 2004-03-23   | 13                                    |                             |
+-------------------+--------------+---------------------------------------+-----------------------------+
| 2.1               | 2005-09-06   | 18                                    |                             |
+-------------------+--------------+---------------------------------------+-----------------------------+
| 2.5               | 2006-09-19   | 12                                    |                             |
+-------------------+--------------+---------------------------------------+-----------------------------+
| 3.0               | 2007-08-21   | 11                                    |                             |
+-------------------+--------------+---------------------------------------+-----------------------------+
| 3.1               | 2008-05-02   | 8                                     |                             |
+-------------------+--------------+---------------------------------------+-----------------------------+
| 3.2               | 2009-02-07   | 9                                     |                             |
+-------------------+--------------+---------------------------------------+-----------------------------+
| 3.3               | 2009-08-19   | 6                                     |                             |
+-------------------+--------------+---------------------------------------+-----------------------------+
| 4.0               | 2010-09-01   | 12                                    |                             |
+-------------------+--------------+---------------------------------------+-----------------------------+
| 4.1               | 2011-08-08   | 11                                    |                             |
+-------------------+--------------+---------------------------------------+-----------------------------+
| 4.2               | 2012-07-05   | 11                                    |                             |
+-------------------+--------------+---------------------------------------+-----------------------------+
| 4.3               | 2013-04-15   | 9                                     |                             |
+-------------------+--------------+---------------------------------------+-----------------------------+

.. _fundacion_plone:

Fundación Plone
---------------

En el 2004 se creó la `Fundación Plone`_ con la misión de la fundación es el de 
proteger y promover Plone. A pesar de que la fundación fue creada para proteger 
los derechos de propiedad, Plone sigue siendo de código abierto [#cite_note-17]_.

Sus objetivos son:

-  Ser la propietaria de los códigos fuentes, `derechos de autor`_, `marcas registradas`_ 
   y `dominios en la Internet`_ de Plone.

-  Proporcionar una estructura de toma de decisiones para las actividades esenciales 
   de la comunidad.

-  Velar por que, como crece Plone, sigue siendo un campo de juego nivelado.

-  Actuar como la voz de Plone para anuncios oficiales, comunicados de prensa y 
   otras comunicaciones.

-  Ayude a crear material de promoción, entrevistas, discursos y otras actividades 
   en el mercado Plone.

Esta conformada por 7 miembros en la Junta directiva, (eventualmente) 7 miembros 
asesores [#cite_note-18]_ y posee mas de 120 :ref:`miembros <miembros_fundacion_plone>`.


Características
---------------

Esta son algunas características disponibles [#cite_note-19]_ en Plone 4:

-  Soporte a HTML5.

-  Cumple con los estándares `XHTML`_ y `CSS`_.

-  Cumple `Accesibilidad`_.

-  Enfocado a la `usabilidad`_.

-  Soporte de canal `RSS`_, y opcional vía producto adicional soporte a `ATOM`_.

-  Edición de las páginas en tiempo real y en contexto.

-  Operaciones sobre el contenido como *Cortar / Copiar / Pegar*.

-  Reordenación de los contenidos con `Drag and drop`_.

-  Diversos modo de presentación de los contenidos.

-  `Motor de workflow`_ integrado.

-  Configuración del :term:`Flujo de trabajo` de forma localizada.

-  Soporte a Copia de Trabajo, mas :term:`Workflow`, aplicar y rechazar revisiones del documento.

-  La utilización adecuada de carpetas virtuales y ":term:`Flujo de trabajo`" le permiten adaptarse 
   a múltiples funciones (por ejemplo, como `CRM`_).

-  Comprobación de la integridad de enlaces y referencias.

-  Bloqueo automático y desbloqueo de documentos.

-  Soporta comportamiento tipo `Wiki`_.

-  Mecanismos de colaboración en la construcción colectiva de contenidos.

-  Compartir documentos de otros usuarios y otorgar permisos específicos.

-  Aporte a discusiones y comentarios de cualquier tipo de contenido, opcional 
   se integra con el servicio `DISQUS`_.

-  Gestión del histórico de reversiones de documento, con posibilidad de comparar 
   versiones y la anulación de cambios realizados.

-  Indexación completa de texto de documentos `Word`_ y `PDF`_.

-  Colecciones / Carpetas inteligentes de los criterios de búsqueda 
   definidos.

-  Navegación dinámica y un mapa del sitio dinámico en el archivo 
   :file:`sitemaps.xml` mas árboles contenido.

-  Soporte para múltiples formatos de `marcado`_.

-  Generación de navegación *anterior / siguiente* automáticamente.

-  Motor de reglas de contenido.

-  Generación automática de tablas de contenido.

-  `Motor de Portlets`_.

-  Soporte, desarrollo, hosting y capacitación a través de mas de 300 de 
   :ref:`proveedores de servicios <soporte_plone>` a nivel mundial.

-  Altos niveles de seguridad.

-  Motor de búsqueda integrado, indexación en tiempo real (todo el contenido están indexados).

-  LiveSearch en `portlet`_.

-  Resultados en la página de búsqueda son dinámicamente mostrado a medida que usted escribe.

-  Gestión de contenido multilingüe.

-  `Localización`_ de la interfaz en modo nativo.

-  Publicación y caducidad de contenidos basada en fechas específicas.

-  Direcciones URLs legible por humanos.

-  Potente editor gráfico de páginas.

-  Reducción de tamaño de los recursos multimedia.

-  Modulable a través de :ref:`Productos adicionales <productos_plone>`, evolutivo y fácilmente personalizable.

-  `Arquitectura abierta`_ y escalable.

-  Autenticación del `back-end`_ a través de `PAS`_ / `LDAP`_ / `SSO`_ / Auth\_tkt.

-  Administración de encabezados HTML para Caching.

-  Integración con `proxy Caché`_.

-  Exportaciones de archivos en formato `XML`_ con configuraciones de sitios.

-  Plantillas ajustables en contenido.

-  Los tipos de contenido estándar.

-  El contenido se formatean automáticamente para ser impreso.

-  Generación de miniaturas y ampliación automática de la imágenes.

-  Soporte a formatos de Vídeo a través `Plumi`_.

-  Paquetes de instalación para `múltiples plataformas`_.

-  Soporta `Microformatos`_.

-  Soporta `WebDAV`_ [#cite_note-20]_ y `FTP`_ [#cite_note-21]_ .

-  Brinda soporte de `copia de seguridad`_.

Filosofía del desarrollo
~~~~~~~~~~~~~~~~~~~~~~~~

.. tip:: Artículo principal: `Arquitectura de Zope`_.

Plone es construido sobre una arquitectura de componentes reutilizables. 
Numerosas extensiones que permiten desplegar los componentes de oficio
específicos.

El modelo de desarrollo de Plone (`Zope`_ en realidad) sigue un diseño 
orientado a aspectos muy bien implementado. Esto posibilita que aspectos 
como la seguridad, la presentación, la gestión de errores, 
:ref:`workflow <motor_flujo_trabajo_plone>` o transacciones sean tratados 
"ortogonalmente" sin estorbarse.

El sistema de plantillas utilizado para la capa de presentación es también 
extraordinario, ya que le permite crear etiquetas propias de marcado como 
las conocidas **taglibs**.

Integración a los sistemas heterogéneos
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

La integración a los sistemas existentes es fácil, ya sea la autentificación 
(`LDAP`_, `SQL`_, sistema operativo), sobre el principio de la autentificación 
única del usuario, el usuario accede al conjunto de los servicios del sitio 
después de su identificación. El almacenamiento de los datos están definidos 
en una base de datos integrada o `SGBD`_ externa como `PostgreSQL`_, `Oracle`_, 
`MS SQL`_, `Sybase`_, `MySQL`_), entre otros.

Almacenamiento de datos
~~~~~~~~~~~~~~~~~~~~~~~

.. tip:: Artículo principal: :ref:`Zope Object Database <que_es_zodb>`.

Gran parte del mérito de `Zope`_/Plone lo tuvo la arriesgada decisión de fundar 
los pilares de la aplicación en una `base de datos de objetos`_ enlazados como 
la :ref:`ZODB <que_es_zodb>` (en contraposición a una `base de datos relacional`_). 
Esta decisión a largo plazo se mostró altamente acertada y permite un desarrollo 
mucho más natural ya que el modelo relacional falla cuando el esquema es "difuso", 
algo común en un sistema documental donde el objeto base, el documento, no tiene 
un esquema sólido y definido. Para que todo pueda funcionar en la práctica se 
requería sin embargo un sistema de indexación muy potente para poder ejecutar 
búsquedas o recorrer la "red de objetos" rápidamente.

Motor de Búsqueda
~~~~~~~~~~~~~~~~~

El sistema de indexación fue implementado de nuevo con gran éxito hasta el punto 
que el mismo permite hacer "búsquedas en tiempo real" aún en bases de datos con 
decenas de Gigabytes y crear carpetas inteligentes (búsquedas almacenadas que el 
usuario ve como una carpeta de contenido) con un tiempo de respuesta extremadamente 
rápido (décimas de segundo en bases de datos de más de un `gigabytes`_) [#cite_note-22]_.

Instalación y configuración
~~~~~~~~~~~~~~~~~~~~~~~~~~~

La instalación de Plone es fácil por la independencia a cada sistema operativo 
(`GNU/Linux`_, `Windows`_, `Mac OS X`_, `BSD`_, `Solaris`_). Su configuración se hace 
en base a scripts de políticas de personalización [#cite_note-23]_.

.. _motor_flujo_trabajo_plone:

Motor de Flujo de trabajo
~~~~~~~~~~~~~~~~~~~~~~~~~

El motor de :term:`Flujo de trabajo` (*Workflow*) reproduce los procesos `burocráticos`_ 
de su organización, permite que los documentos (incluyendo los usuarios) estén 
basados en estados los cuales pueden disparar tipo de acciones.

Seguridad
~~~~~~~~~

Sobre la seguridad, Plone pone a disposición de los usuarios roles y
grupos con mucha flexibilidad. También es posible manejar localmente la
seguridad y no solamente al nivel del conjunto del sistema. Es decir un
usuario puede ser administrador de la zona "/financiero" al tiempo que
sólo es miembro restringido de "/soporte".

Interfaz de Usuario
~~~~~~~~~~~~~~~~~~~

Plone se centra en el contenido (o documento) como unidad central de
trabajo ofreciendo una alta productividad a sus usuarios, que no se ven
distraídos por menús y barras de herramientas "laberínticas" como en
herramientas ofimáticas convencionales. El acento es puesto en una
interfaz de usuarios agradable e intuitiva: numerosas pruebas de
`usabilidad`_ fueron efectuadas para comprobar su eficacia.

La interfaz de Plone es compatible con los estándares de `CSS`_ y 
de `XHTML`_. El uso intensivo de `CSS`_ permite beneficiar a una 
interfaz ligera. En nativo, cada página del sitio es optimizada 
para la impresión. También cada página tiene su propio modo de 
visualización.

Lenguajes usados
~~~~~~~~~~~~~~~~

Plone es principalmente desarrollado en `Python`_. Se usan, además, otros 
lenguajes en el proyecto. A continuación una lista que resume los lenguajes 
usados en Plone, como esta aparece en el `sitio de ohloh del proyecto Plone`_:

-  `Python`_ 54%

-  `JavaScript`_ 27%

-  `XML`_ 12%

-  Otros 7%

En la categoría de "Otros" se incluyen `HTML`_, `Perl`_, `AWK`_, `Make`_ y otras
más [#cite_note-24]_.

Comunidad
---------

La comunidad alrededor de Plone tienen muchos actores que cumplen muchas
funciones que a continuación describimos:

Desarrolladores
~~~~~~~~~~~~~~~

Para Enero de 2013 cuenta con 441 desarrolladores de núcleo de Plone en todo el 
mundo [#cite_note-25]_.

.. _soporte_plone:

Soporte
~~~~~~~

Para Enero de 2013, cuenta con soporte comercial por **367** proveedores de servicios 
en **115** países en todo el mundo, [#cite_note-26]_ adicionalmente ofrece otros medios 
de asistencia técnica por medio del `Plone Support Center`_, que ofrece soporte vía 
`chat IRC`_, soporte comunitario por medio de `grupos activistas de Plone`_ en tu región 
y `capacitación`_ ofrecida por los proveedores de servicios comercial.

.. _miembros_fundacion_plone:

Miembros de la Fundación Plone
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Para Enero de 2013, cuenta con 125 miembros de la Fundación, [#cite_note-27]_ si quieres 
formar parte de la :ref:`Fundación Plone <fundacion_plone>` puedes llenar su `solicitud`_ 
cumpliendo con los requerimientos necesarios.

Patrocinadores
~~~~~~~~~~~~~~

Para Enero de 2013, la :ref:`Fundación Plone <fundacion_plone>` posee más de 10 patrocinadores 
que proporcionan apoyo monetario incluyendo `Google`_, `OpenID Foundation`_ y 
`Computer Associates`_ [#cite_note-28]_.

Implementaciones
~~~~~~~~~~~~~~~~

Para Enero de 2013, cuenta con más de 2317 de altos perfiles sitios web [#cite_note-29]_ 
construido con Plone incluyendo:

#. `FBI`_.

#. `CIA`_.

#. `Amnistía Internacional`_.

#. `Gobierno de Brasil`_.

#. `Discover Magazine`_.

#. `NASA`_.

#. `Nokia`_.

#. La `Free Software Foundation`_.

#. `Universidad de Yale`_.

.. _productos_plone:

Productos / Addons / Módulos
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

La comunidad soporta y distribuye miles de módulos vía sitios web de *proveedores 
de servicios* pero la mayoría están en el :term:`PyPI` y www.plone.org. Los cantidad 
de paquetes publicados hasta la fecha de `Diciembre de 2013`_ son de 2674 en la categoría 
*Framework :: Plone* vía :term:`PyPI` para personalizar Plone [#cite_note-30]_.

Distribuciones basadas en Plone
-------------------------------

Una distribución Plone consiste en un paquete de diferentes productos
configurados previamente y / o modificados y que dan solución a una
necesidad específica. La ventaja de trabajar con distribuciones es la
facilidad en tener una solución completa funcionando en poco tiempo y
poder seguir contando con la flexibilidad de Plone que permite agregar
nuevos productos y reconfigurar los existentes a la medida, en
diferentes áreas como las que a continuación se en listan:

Gobierno electrónico
~~~~~~~~~~~~~~~~~~~~

-  `Project Portfolio Manager (PPM)`_, es una aplicativo para cualquier 
   organización que desee un framework para administración de proyectos 
   y propuestas de estos mismos, inicialmente desarrollado por la comunidad 
   PloneGov `Open eGov`_ de `EUA`_, actualmente el desarrollo es mantenido por la
   `fundación Cenditel`_ de `Venezuela`_.

-  `Gestión de discusiones con PloneMeeting`_, una solución para gestión de reuniones, decisiones de 
   las mismas para el sector de gobierno, desarrollada por la comunidad 
   PloneGov `CommunesPlone`_ de `Bélgica`_. Dispone un `sitio demostrativo`_ 
   para comprender las capacidades técnicas de esta distribución.

-  `PloneTask`_, una solución para asignación y gestión de tareas, que se puede
   integrar perfectamente con `PloneMeeting`_ para el seguimiento de las decisiones 
   tomadas a través de PloneMeeting, decisiones de las mismas para el sector de gobierno,
   desarrollada por la comunidad PloneGov `CommunesPlone`_ de `Bélgica`_.

Intranet / Enterprise 2.0
~~~~~~~~~~~~~~~~~~~~~~~~~

-  `Ploomcake`_, una distribución de
   **Plone** para escenarios diferentes como sitios web de noticias,
   portal de colaboración, intranets, etc.

-  `Cyn.in`_, una plataforma de trabajo grupal alternativa a `SharePoint`_ de
   `Microsoft`_. Dispone un `sitio demostrativo para Cyn.in`_ para comprender 
   las capacidades técnicas de esta distribución.

-  `OpenCore Software`_, es una línea de base común de herramientas de 
   colaboración para ayudar a los grupos de trabajo colectivo, incluidos 
   los espacios de colaboración con `Wiki`_, las `listas de correo`_ 
   a través de `Listen`_ que integra la administración de este servicio 
   como un foro de discusión, `bitácoras en línea`_ a través de
   :ref:`Deliverance <apariencias_deliverance>` y el sistema de Blog `Wordpress`_ 
   y herramientas de gestión del equipo de trabajo y de sus roles. Dispone 
   un `servicio gratuito para usarlo`_ para comprender las capacidades técnicas 
   de esta distribución.

Educación / E-learning
~~~~~~~~~~~~~~~~~~~~~~

-  `PloneEdu`_, comunidad que ofrece una serie de productos que permiten crear 
   sitios web para centros educativos en Plone. Dispone de instrucciones de como 
   `construir un sitios modelo`_ para comprender las capacidades técnicas de esta 
   distribución.

-  `EduCommons`_, una plataforma exclusiva a gestión de contenidos de aprendizaje 
   `OpenCourseWare`_ para ofrecer los contenidos de las clases presenciales o a 
   distancia alternativa el movimiento `OWC`_ en Plone. Dispone un `sitio demostrativo de EduCommons`_ 
   para comprender las capacidades técnicas de esta distribución.

-  `EduComponents`_, una plataforma de acompañamiento y seguimientos estudiantil para
   clases presenciales y a distancia alternativa a un `LMS`_ en Plone como `Moodle`_. 
   Dispone un `sitio demostrativo de EduComponents`_ para comprender las capacidades 
   técnicas de esta distribución.

Comercio electrónico
~~~~~~~~~~~~~~~~~~~~

-  `Open Tiendas`_, una plataforma de comercio electrónico basada en Plone.

Artistas / Web 2.0
~~~~~~~~~~~~~~~~~~~

-  `Plumi`_, una plataforma que permite a los usuarios crear una sitio de intercambio 
   de vídeo como alternativas no comerciales, de código abierto a los sitios de vídeo 
   comerciales como `YouTube`_. Dispone un `sitio demostrativo de Plumi`_ para comprender 
   las capacidades técnicas de esta distribución.

-  `Plone4Artists`_, una plataforma que permite la creación de sitios Web para artistas
   musicales, alternativa a `MySpace`_.

Dispositivos Móviles
~~~~~~~~~~~~~~~~~~~~

-  `gomobile`_, una alternativa para hacer accesible Plone desde dispositivos `móviles`_.

-  `Responsive theme for Plone`_, existe una serie de temas que son responsable con soporte 
   a diversos dispositivos `móviles`_ en Plone.


Enlaces externos
----------------

-  `Sitio oficial de Plone <http://www.plone.org/>`_ (en Ingles).

-  `Sitio web demostrativo de Plone <http://demo.plone.org/>`_ (en Ingles).

-  `Directorio de proveedores de servicios, casos de estudios, y elementos de noticias relacionadas a Plone <http://plone.org/support/network>`_ (en Ingles).

-  `Guía definitiva de Plone en pdf <http://plone.org/documentation/manual/definitive-guide/definitive_guide_to_plone.pdf>`_ (en Ingles).

-  `The Plone Book <http://enfoldsystems.com/support/a-users-guide-to-plone.html>`_ (en Ingles).

-  `Plone en Español <http://www.plone.es/>`_, sitio web de las comunidades de España y de los países de habla hispana (en Español).

-  `Documentación oficial de Plone en Español <http://plone-spanish-docs.rtfd.org>`_ (en Español).

-  `Plone Cono Sur, comunidad de usuarios de Plone para el Cono Sur <http://www.plone.org/countries/conosur>`_ (en Español).

-  `Plone Chile, comunidad de usuarios de Plone para Chile <http://www.plonechile.cl/>`_ (en Español).

-  `Plone Venezuela, comunidad de usuarios de Plone para Venezuela <http://www.plone.org.ve/>`_ (en Español).

-  `Plone México, comunidad de usuarios de Plone para México <http://www.plone.mx/>`_ (en Español).

-  `Introducción a Plone, un Screencast <http://www.archive.org/details/SeanKellyIntroducingPlone>`_ (en Ingles).

-  `Desarrollos de Portales y Extranet con Plone - Qué es, introducción y estudios de casos <http://rover.objectis.net/techie/ploneUser/material/portalesExtranet.pdf>`_ (en Español).

-  `Plone en entornos Gubernamentales <http://rover.objectis.net/techie/ploneUser/material/plone-gov.pdf>`_ (en Español).

-  `Manual de usuario de Plone en castellano <http://dailymp.googlepages.com/PlataformaPloneZope.pdf>`_ (en Español).

.. rubric:: Referencias

.. [#cite_note-1] «`Plone 4.3 — Plone CMS: Open Source Content Management <http://plone.org/products/plone/releases/4.3>`_» (en ingles). Plone.org (8 de mayo de 2013). Consultado el 8 de mayo de 2013.
.. [#cite_note-2]  «`Plone 4.3 — Plone CMS: Open Source Content Management <http://plone.org/products/plone/releases/4.3>`_» (en ingles). Plone.org (8 de mayo de 2013). Consultado el 8 de mayo de 2013.
.. [#cite_note-3] Allende, Roberto (15 de octubre 2006) (en Español, Presentación PDF). `Desarrollos de Portales y Extranet con Plone <http://rover.objectis.net/techie/ploneUser/material/portalesExtranet.pdf>`_. Menttes. `http://rover.objectis.net/techie/ploneUser/material/portalesExtranet.pdf <http://rover.objectis.net/techie/ploneUser/material/portalesExtranet.pdf>`_. Consultado el 21 de enero de 2013. 
.. [#cite_note-4] Real Story Group (13 de enero de 2011). «`Vendor Map from The Real Story Group (formerly CMS Watch) <http://www.realstorygroup.com/images/subway_Graphic_5.23.12.pdf>`_» (en ingles) (PDF) pág. `http://www.realstorygroup.com/#32 <http://www.realstorygroup.com/#32>`_ ; Boston, MA, USA: Real Story Group. Archivado desde el `original <http://www.realstorygroup.com/vendormap/>`_ el 13 de enero de 2011. Consultado el 24 de enero de 2013.
.. [#cite_note-5] Zhou, Chuanhong; Zeng Huilan (2006) (en Ingles). `Knowledge Enterprise: Intelligent Strategies in Product Design, Manufacturing, and Management - Enterprise Knowledge Management Based on Plone Content Management System <http://www.springerlink.com/content/c2g71846hu5051q5/fulltext.pdf>`_. IFIP Advances in Information and Communication Technology. 207. Springer US.  pp. 115-120. `ISSN <http://es.wikipedia.org/wiki/International_Standard_Serial_Number>`_ `1571-5736 <http://worldcat.org/issn/1571-5736>`_. `http://www.springerlink.com/content/c2g71846hu5051q5/fulltext.pdf <http://www.springerlink.com/content/c2g71846hu5051q5/fulltext.pdf>`_. Consultado el 21 de enero de 2013. 
.. [#cite_note-6] Franco Pellegrini (24 de noviembre de 2010). «`CMS + CRM: Integrando Plone y Salesforce <http://www.slideshare.net/menttes/cms-crm-integrando-plone-y-salesforce>`_» (en español) (PDF). Menttes. Consultado el 24 de enero de 2013.
.. [#cite_note-7] Franco Pellegrini (24 de noviembre de 2010). «`Watch CMS + CRM: Integrando Plone y Salesforce \| menttes Episodes <http://blip.tv/menttes/cms-crm-integrando-plone-y-salesforce-4720838>`_» (en español). Menttes. Consultado el 24 de enero de 2013.
.. [#cite_note-8] Borelli, Giorgio (11 de octubre de 2012). `Giorgio Borelli: Where is my content? Geo-referencing content types in Plone with collective.geo - YouTube <http://www.youtube.com/watch?v=tUiJ99jKlsM>`_. Plone Conference 2012. `http://www.youtube.com/watch?v=tUiJ99jKlsM <http://www.youtube.com/watch?v=tUiJ99jKlsM>`_. Consultado el 24 de enero de 2013.
.. [#cite_note-9] Brehault, Eric (11 de octubre de 2012). `Eric Brehault: I want a nice map! - YouTube <http://www.youtube.com/watch?v=1jjpcAlkVSU>`_. Plone Conference 2012. `http://www.youtube.com/watch?v=1jjpcAlkVSU <http://www.youtube.com/watch?v=1jjpcAlkVSU>`_. Consultado el 24 de enero de 2013. 
.. [#cite_note-10] Alex Limi (31 de enero de 2003). «`Plone 1.0 release! — Plone CMS: Open Source Content Management <http://plone.org/events/community/plone-release>`_» (en ingles). Plone.org. Consultado el 24 de enero de 2013.
.. [#cite_note-11] «`Plone Conference 1 — Plone CMS: Open Source Content Management <http://plone.org/events/conferences/new-orleans-2003>`_» (en ingles). Plone.org. Consultado el 24 de enero de 2013.
.. [#cite_note-12]  «`Plone Conference 2013: Call for Proposals — Plone CMS: Open Source Content Management <http://plone.org/events/conferences/plone-conference-2013>`_» (en ingles). Plone.org. Consultado el 24 de enero de 2013.
.. [#cite_note-13] William Deegan (23 de marzo de 2004). «`Plone 2.0 — Plone CMS: Open Source Content Management <http://plone.org/products/plone/releases/2.0>`_» (en ingles). Plone.org. Consultado el 24 de enero de 2013.
.. [#cite_note-14] Alex Limi (3 de enero de 2009). «`Plone 3.0 released! — Plone CMS: Open Source Content Management <http://plone.org/news/plone-3.0-released>`_» (en ingles). Plone.org. Consultado el 24 de enero de 2013.
.. [#cite_note-15] Mark Corum (1 de septiembre de 2010). «`Plone 4 CMS Unveiled: Advancing Power, Performance & User Experience — Plone CMS:- Open Source Content Management <http://plone.org/news/plone-4-released>`_» (en ingles). Plone.org. Consultado el 24 de enero de 2013.
.. [#cite_note-16] «`Open Source Awards Previous Winners \| Packt Publishing <http://www.packtpub.com/article/open-source-awards-previous-winners>`_» (en ingles). Packt Publishing. Consultado el 24 de enero de 2013.
.. [#cite_note-17] Joel Burton (3 de enero de 2009). «`Plone Foundation FAQs — Plone CMS: Open Source Content Management <http://plone.org/foundation/about/faq>`_» (en ingles). Plone.org. Consultado el 24 de enero de 2013.
.. [#cite_note-18] Paul Roeland (17 de enero de 2013). «`Plone Foundation Board for 2012-2013 — Plone CMS: Open Source Content Management <http://plone.org/foundation/board/>`_» (en ingles). Plone.org. Consultado el 24 de enero de 2013.
.. [#cite_note-19] Jon Stahl (2 de septiembre de 2010). «`What’s New in Plone 4 — Plone CMS: Open Source Content Management <http://plone.org/products/plone/features>`_» (en ingles). Plone.org. Consultado el 23 de enero de 2013.
.. [#cite_note-20] Caballero G., Leonardo J. (17 de diciembre del 2012). `Configurar Zope como un servidor WebDAV <https://plone-spanish-docs.readthedocs.org/en/latest/zope/webdav/index.html>`_ . Plone Venezuela. `https://plone-spanish-docs.readthedocs.org/en/latest/zope/webdav/index.html <https://plone-spanish-docs.readthedocs.org/en/latest/zope/zope_como_servidor_webdav.html>`_. Consultado el 29 de diciembre de 2013.
.. [#cite_note-21] Caballero G., Leonardo J. (17 de diciembre del 2012). `Configurar Zope como un servidor FTP <https://plone-spanish-docs.readthedocs.org/en/latest/zope/ftp/index.html>`_. Plone Venezuela. `https://plone-spanish-docs.readthedocs.org/en/latest/zope/ftp/index.html <https://plone-spanish-docs.readthedocs.org/en/latest/zope/ftp/index.html>`_. Consultado el 29 de diciembre de 2013.
.. [#cite_note-22] Jon Stahl (31 de agosto de 2010). «`Massively improved handling of large files & media — Plone CMS: Open Source Content Management <http://plone.org/products/plone/features/massively-improved-handling-of-large-files-media>`_» (en ingles). Plone.org. Consultado el 24 de enero de 2013.
.. [#cite_note-23] De la Guardia, Carlos; Leonardo J. Caballero G. (17 de diciembre del 2012). «`Creación de un producto de configuración <https://plone-spanish-docs.readthedocs.org/en/latest/programacion/crear_producto_policy.html#producto-policy>`_». Plone Venezuela. Consultado el 29 de diciembre de 2013.
.. [#cite_note-24] «`The Plone Open Source Project on Ohloh <http://www.ohloh.net/p/plone/analyses/latest/languages_summary>`_» (en ingles). Ohloh.net (24 de enero de 2013). Consultado el 24 de enero de 2013. 
.. [#cite_note-25] «`Plone Plone Developers: Open Source Content Management <http://plone.org/team/Committers>`_» (en ingles). Plone.org. Consultado el 20 de enero de 2013.
.. [#cite_note-26] «`Plone Service Providers — Plone CMS: Open Source Content Management <http://plone.org/support/providers>`_» (en ingles). Plone.org. Consultado el 20 de enero de 2013.
.. [#cite_note-27] Andrei, Érico (31 de octubre de 2012). `Gestión de Contenido con Plone <http://www.slideshare.net/simplesconsultoria/gestin-de-contenido-con-plone>`_. pp. 10. `http://www.slideshare.net/simplesconsultoria/gestin-de-contenido-con-plone <http://www.slideshare.net/simplesconsultoria/gestin-de-contenido-con-plone>`_. Consultado el 20 de enero de 2013. 
.. [#cite_note-28] «`Plone Foundation Sponsors and Donors — Plone CMS: Open Source Content Management <http://plone.org/foundation/donors>`_» (en ingles). Plone.org. Consultado el 20 de enero de 2013.
.. [#cite_note-29] «`Plone Sites — Plone CMS: Open Source Content Management <http://plone.org/support/sites>`_» (en ingles).
   Plone.org. Consultado el 20 de enero de 2013.
.. [#cite_note-30] «`Browse : Python Package Index <https://pypi.python.org/pypi?:action=browse&c=518>`_» (en ingles). Pypi.python.org. Consultado el 29 de diciembre de 2013.

.. note:: 
    Obtenido de «`http://es.wikipedia.org/w/index.php?title=Plone&oldid=69979133 <http://es.wikipedia.org/w/index.php?title=Plone&oldid=69979133>`_».


.. _2001: http://plone.org/documentation/faq/plone-history
.. _CMS: http://es.wikipedia.org/wiki/CMS
.. _Multiplataforma: http://es.wikipedia.org/wiki/Multiplataforma
.. _GPL: http://es.wikipedia.org/wiki/Licencia_p%C3%BAblica_general_de_GNU
.. _sistema de gestión de contenidos: http://es.wikipedia.org/wiki/Sistema_de_gesti%C3%B3n_de_contenidos
.. _sitio web: http://es.wikipedia.org/wiki/Sitio_web
.. _externos: http://es.wikipedia.org/wiki/Extranet
.. _internos: http://es.wikipedia.org/wiki/Intranet
.. _blogs: http://es.wikipedia.org/wiki/Blogs
.. _tiendas en línea: http://es.wikipedia.org/wiki/Tienda_en_l%C3%ADnea
.. _herramienta colaborativa: http://es.wikipedia.org/wiki/Groupware
.. _código abierto: http://es.wikipedia.org/wiki/C%C3%B3digo_abierto
.. _GNU General Public License: http://es.wikipedia.org/wiki/GNU_General_Public_License 
.. _Zope: http://es.wikipedia.org/wiki/Zope
.. _Python : http://es.wikipedia.org/wiki/Python
.. _reuniones especiales: http://es.wikipedia.org/wiki/Hackathon
.. _Plone Sprints: http://plone.org/events/sprints
.. _Software Freedom Law Center: http://www.softwarefreedom.org/
.. _flexibles y adaptables: http://es.wikipedia.org/wiki/Flujo_de_trabajo
.. _Real Story Group: http://www.realstorygroup.com/
.. _Document & Records Management: http://en.wikipedia.org/wiki/Electronic_document_and_records_management_system
.. _Sistema de gestión de contenidos: http://es.wikipedia.org/wiki/Sistema_de_gesti%C3%B3n_de_contenidos
.. _Gestión del conocimiento: http://es.wikipedia.org/wiki/Gesti%C3%B3n_del_conocimiento
.. _Software colaborativo: http://es.wikipedia.org/wiki/Software_colaborativo
.. _Software social: http://es.wikipedia.org/wiki/Software_social
.. _Gestión de Conocimiento: http://es.wikipedia.org/wiki/Gesti%C3%B3n_del_conocimiento
.. _CRM: http://es.wikipedia.org/wiki/Customer_relationship_management
.. _software GIS: http://es.wikipedia.org/wiki/Sistema_de_Informaci%C3%B3n_Geogr%C3%A1fica#Software_SIG
.. _cartografía en entornos web: http://es.wikipedia.org/wiki/Sistema_de_Informaci%C3%B3n_Geogr%C3%A1fica#Cartograf.C3.ADa_en_entornos_web
.. _Zope Content Management Framework: http://es.wikipedia.org/wiki/Zope_Content_Management_Framework
.. _Sprints: http://plone.org/events/sprints
.. _http://plone.org/products/plone: http://plone.org/products/plone
.. _Fundación Plone: http://plone.org/foundation/
.. _derechos de autor: http://es.wikipedia.org/wiki/Derecho_de_autor
.. _marcas registradas: http://es.wikipedia.org/wiki/Marca_(registro)
.. _dominios en la Internet: http://es.wikipedia.org/wiki/Dominio_de_Internet
.. _XHTML: http://es.wikipedia.org/wiki/XHTML
.. _CSS: http://es.wikipedia.org/wiki/CSS
.. _Accesibilidad: http://es.wikipedia.org/wiki/Accesibilidad
.. _usabilidad: http://es.wikipedia.org/wiki/Usabilidad
.. _RSS: http://es.wikipedia.org/wiki/RSS
.. _ATOM: http://es.wikipedia.org/wiki/Atom_(formato_de_redifusi%C3%B3n)
.. _Drag and drop: http://es.wikipedia.org/wiki/Drag_and_drop
.. _Motor de workflow: http://es.wikipedia.org/wiki/Flujos_de_trabajo
.. _CRM: http://es.wikipedia.org/wiki/Customer_relationship_management
.. _Wiki: http://es.wikipedia.org/wiki/Wiki
.. _DISQUS: http://en.wikipedia.org/wiki/Disqus
.. _Word: http://es.wikipedia.org/wiki/Microsoft_Word
.. _PDF: http://es.wikipedia.org/wiki/PDF
.. _marcado: http://es.wikipedia.org/wiki/Lenguaje_de_marcado
.. _Motor de Portlets: http://es.wikipedia.org/wiki/Portlet
.. _portlet: http://es.wikipedia.org/wiki/Portlet
.. _Localización: http://es.wikipedia.org/wiki/Internacionalizaci%C3%B3n_y_localizaci%C3%B3n
.. _Arquitectura abierta: http://es.wikipedia.org/wiki/Zope#Arquitectura_de_Zope
.. _back-end: http://es.wikipedia.org/wiki/Back-end
.. _PAS: http://developer.plone.org/reference_manuals/old/pluggable_authentication_service/index.html
.. _LDAP: http://es.wikipedia.org/wiki/LDAP
.. _SSO: http://es.wikipedia.org/wiki/SSO
.. _proxy Caché: http://es.wikipedia.org/wiki/Proxy_cach%C3%A9
.. _XML: http://es.wikipedia.org/wiki/XML
.. _Plumi: https://en.wikipedia.org/wiki/Plumi
.. _múltiples plataformas: http://es.wikipedia.org/wiki/Multiplataforma
.. _Microformatos: http://es.wikipedia.org/wiki/Microformato
.. _WebDAV: http://es.wikipedia.org/wiki/WebDAV
.. _FTP: http://es.wikipedia.org/wiki/File_Transfer_Protocol
.. _copia de seguridad: http://es.wikipedia.org/wiki/Copia_de_seguridad
.. _Arquitectura de Zope: http://es.wikipedia.org/wiki/Arquitectura_de_Zope
.. _LDAP: http://es.wikipedia.org/wiki/LDAP
.. _SQL: http://es.wikipedia.org/wiki/SQL
.. _SGBD: http://es.wikipedia.org/wiki/SGBD
.. _PostgreSQL: http://es.wikipedia.org/wiki/PostgreSQL
.. _Oracle: http://es.wikipedia.org/wiki/Oracle_Database
.. _MS SQL: http://es.wikipedia.org/wiki/MS_SQL
.. _Sybase: http://es.wikipedia.org/wiki/Sybase#Gestores_de_bases_de_datos
.. _MySQL: http://es.wikipedia.org/wiki/MySQL
.. _base de datos de objetos: http://es.wikipedia.org/wiki/Base_de_datos_orientada_a_objetos
.. _base de datos relacional: http://es.wikipedia.org/wiki/RDBMS
.. _gigabytes: http://es.wikipedia.org/wiki/Gigabytes
.. _GNU/Linux: http://es.wikipedia.org/wiki/GNU/Linux
.. _Windows: http://es.wikipedia.org/wiki/Microsoft_Windows
.. _Mac OS X: http://es.wikipedia.org/wiki/Mac_OS_X
.. _BSD: http://es.wikipedia.org/wiki/BSD
.. _Solaris: http://es.wikipedia.org/wiki/Solaris_(sistema_operativo)
.. _Flujo de trabajo: http://es.wikipedia.org/wiki/Flujo_de_trabajo
.. _burocráticos: http://es.wikipedia.org/wiki/Burocr%C3%A1tico
.. _JavaScript: http://es.wikipedia.org/wiki/JavaScript
.. _sitio de ohloh del proyecto Plone: http://www.ohloh.net/p/plone/
.. _HTML: http://es.wikipedia.org/wiki/HTML
.. _Perl: http://es.wikipedia.org/wiki/Perl
.. _AWK: http://es.wikipedia.org/wiki/AWK
.. _Make: http://es.wikipedia.org/wiki/Make
.. _Plone Support Center: http://plone.org/support
.. _chat IRC: http://plone.org/support/chat
.. _grupos activistas de Plone: http://plone.org/support/local-user-groups
.. _capacitación: http://plone.org/events/training
.. _solicitud: http://plone.org/foundation/membership
.. _Google: http://es.wikipedia.org/wiki/Google
.. _OpenID Foundation: http://es.wikipedia.org/wiki/OpenID_Foundation
.. _Computer Associates: http://es.wikipedia.org/wiki/Computer_Associates
.. _FBI: http://es.wikipedia.org/wiki/FBI
.. _CIA: http://es.wikipedia.org/wiki/CIA
.. _Amnistía Internacional: http://es.wikipedia.org/wiki/Amnist%C3%ADa_Internacional
.. _Gobierno de Brasil: http://es.wikipedia.org/wiki/Gobierno_de_Brasil
.. _Discover Magazine: http://en.wikipedia.org/wiki/Discover_(magazine)
.. _NASA: http://es.wikipedia.org/wiki/NASA
.. _Nokia: http://es.wikipedia.org/wiki/Nokia
.. _Free Software Foundation: http://es.wikipedia.org/wiki/Free_Software_Foundation
.. _Universidad de Yale: http://es.wikipedia.org/wiki/Universidad_de_Yale
.. _Diciembre de 2013: http://es.wikipedia.org/wiki/Diciembre_de_2013
.. _Project Portfolio Manager (PPM): https://github.com/Cenditel/cenditel.ppm
.. _Open eGov: http://plonegov.org/software/products/open-egov/
.. _EUA: http://es.wikipedia.org/wiki/EUA
.. _fundación Cenditel: http://plataforma.cenditel.gob.ve/wiki/Plone/PPM
.. _Venezuela: http://es.wikipedia.org/wiki/Venezuela
.. _Gestión de discusiones con PloneMeeting: http://www.imio.be/produits/gestion-des-deliberations
.. _PloneMeeting: http://www.imio.be/produits/gestion-des-deliberations
.. _CommunesPlone: http://www.communesplone.org/
.. _Bélgica: http://es.wikipedia.org/wiki/B%C3%A9lgica
.. _sitio demostrativo: http://demo-pm.imio.be/
.. _PloneTask: http://svn.communesplone.org/svn/communesplone/PloneTask/
.. _Ploomcake: http://www.ploomcake.org/en
.. _Cyn.in: http://www.cynapse.com/cynin
.. _SharePoint: http://es.wikipedia.org/wiki/SharePoint
.. _Microsoft: http://es.wikipedia.org/wiki/Microsoft
.. _sitio demostrativo para Cyn.in: http://www.cynapse.com/community/home/sandbox-area
.. _OpenCore Software: http://www.coactivate.org/projects/opencore/project-home
.. _listas de correo: http://es.wikipedia.org/wiki/Servidor_de_correo
.. _Listen: http://www.coactivate.org/projects/listen/summary
.. _bitácoras en línea: http://es.wikipedia.org/wiki/Blog
.. _Wordpress: http://es.wikipedia.org/wiki/Wordpress
.. _servicio gratuito para usarlo: http://www.coactivate.org/projects/create
.. _PloneEdu: http://weblion.psu.edu/ploneedu/
.. _construir un sitios modelo: https://svn.it.uwosh.edu/svn/plone/buildouts/ploneedu/
.. _EduCommons: http://educommons.com/
.. _OpenCourseWare: http://es.wikipedia.org/wiki/OpenCourseWare
.. _OWC: http://es.wikipedia.org/wiki/OpenCourseWare
.. _sitio demostrativo de EduCommons: http://demo.educommons.com/
.. _EduComponents: http://www.coactivate.org/projects/ploneve/blog/2010/03/09/plone-y-educomponents-para-e-learning/
.. _LMS: http://es.wikipedia.org/wiki/LMS_(Learning_Management_System)
.. _Moodle: http://es.wikipedia.org/wiki/Moodle
.. _sitio demostrativo de EduComponents: http://wdok.cs.uni-magdeburg.de/demo/
.. _Open Tiendas: http://www.opentiendas.com
.. _YouTube: http://es.wikipedia.org/wiki/YouTube
.. _sitio demostrativo de Plumi: http://demo.plumi.org/
.. _Plone4Artists: https://www.ohloh.net/p/plone4artists
.. _MySpace: http://es.wikipedia.org/wiki/MySpace
.. _gomobile: https://web-and-mobile.readthedocs.org/en/latest/
.. _móviles: http://es.wikipedia.org/wiki/M%C3%B3viles
.. _Responsive theme for Plone: http://pypi.python.org/pypi?%3Aaction=search&term=plone+theme+responsive&submit=search