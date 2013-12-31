.. -*- coding: utf-8 -*-

.. _que_es_zope:

===============================
Z Object Publishing Environment
===============================

:Autor(es): Leonardo J. Caballero G.
:Correo(s): leonardocaballero@gmail.com
:Fecha: 31 de Diciembre de 2013

.. _ficha_tecnica_zope:

.. sidebar:: Ficha técnica

    :Desarrollador: :ref:`Zope Corporation <zope_corporation>`.
    :Diseñador: :ref:`Zope Corporation <zope_corporation>`.
    :Lanzamiento:    1998.
    :Ver. estable: `2.13.19`_, 31 de octubre de 2012.
    :Ver. pruebas: `4.0a1`_
    :Género: `Servidor de aplicaciones`_ Web.
    :Programado en: :ref:`Python <python_index>`.
    :Sistema base: `Multiplataforma`_, `Mac OS X`_, `GNU/Linux`_, `Windows`_, `BSD`_, `Solaris`_.
    :Plataforma: `Zope <http://es.wikipedia.org/wiki/Zope>`_.
    :Licencia: `Zope Public License`_.
    :Estado actual: Estable.
    :Idiomas: 1.
    :En español: No.

**Zope** es un proyecto comunitario activista de un entorno de desarrollo para la 
creación de `sitios web`_ dinámicos y/o aplicaciones web usando 
un `servidor de aplicaciones web`_ `orientado al objeto`_, escrito en el 
`lenguaje de programación`_ :ref:`Python <python_index>` (con algunos 
componentes fueron escritos en `lenguaje C`_ para optimizar su rendimiento) 
de `código abierto`_ publicado bajo la licencia `Zope Public License`_.

.. figure:: images/zope-logo.png
  :width: 180px
  :alt: Logotipo de Zope
  :align: center

  Logotipo de Zope

Aunque el nombre **Zope** viene del `acrónimo`_ inglés *"Z Object Publishing 
Environment – Zope"*, su origen se debe a un tipo de pez `Cyprinus ballerus`_ 
es conocido como **zope** o **blue bream** [#cite_note-1]_.

Históricamente ha sido reconocido como una `aplicación determinante`_ que ayudó 
a colocar :ref:`Python <python_index>` en el centro de atención de los programadores 
a nivel mundial [#cite_note-2]_ [#cite_note-3]_.

Muchas cosas que son actualmente parte del núcleo de :ref:`Python <python_index>` 
originalmente fueron innovaciones en su momento dadas por el desarrollo de Zope 
a la comunidad de programadores Python, un ejemplo de esto es la librería ``datetime`` 
que proviene del ``DateTime`` de Zope 2.

Historia
--------

En el año de 1995, **Digital Creations** fue establecida en `Fredericksburg (Virginia)`_, 
fundada como una empresa conjunta de la fusión de varios `periódicos`_. Los primeros 
empleados fueron `Paul Everitt`_ y `Rob Page`_, bastante pronto se sumaría empleado como 
`Jim Fulton`_.

En 1996, `Jim Fulton`_, ahora el CTO de :ref:`Zope Corporation <zope_corporation>`, fue 
seleccionado ​​para dar una clase de programación sobre `Common Gateway Interface - CGI`_, 
a pesar de no saber mucho sobre el tema. La programación en CGI fue el modelo web de 
desarrollo de uso común del momento, el cual a los programadores les permitía construir 
sitios web dinámicos. Entonces el viajar a la clase, Jim estudió toda la documentación 
existente en CGI. En el camino de vuelta, Jim considerado lo que no me gustó de entornos 
de programación tradicionales basados ​​en CGI. A partir de estas reflexiones iniciales, 
el núcleo de Zope fue escrito durante el vuelo de regreso de la clase de programación en 
CGI [#cite_note-4]_.

En mayo de 1997, se convierte en el consorcio de periódicos del `Digital Creations`_, 
para ese momento, ya algunas empresas e usuarios estaban usando el producto gratuito 
**Bobo**, uno de esos usuarios fue `Hadar Pedhazur`_, el cual tenía el deseo de invertir 
en el consorcio. Las negociaciones, sin embargo, no tuvieron éxito, porque las diferencias 
de visiones del futuro que Hadar vio para **Digital Creaciones** como una empresa de 
servicios, en cambio Paul y Rob le interesaban que sus productos de software **Bobo**, 
un `ORB`_ ligero para la web; **Document Template**, un `lenguaje de scripting`_, 
**BoboPOS**, una `base de datos orientada a objetos`_ estuvieran dentro del aplicación 
comercial **Principia**, un `servidor de aplicaciones`_ Web, bajo un modelo de venta como 
`soluciones propietarias`_.

Un año después, Hadar volvió a **Digital Creations**, tras el éxito alcanzado *(aunque no 
fue tanto como se esperaba)*, fue entonces en noviembre de 1998 que llegaron al acordó de 
publicar el código fuente de sus productos emblemáticos **Bobo** y **Principia**, esta 
decisión fue influenciada por Hadar, principal inversionista en la compañía [#cite_note-5]_. 
La combinación de Bobo y Principia fue rebautizado entonces como **Zope**. Esta decisión 
resultó de una empresa de servicios de Digital Creations (hoy en día 
:ref:`Zope Corporation <zope_corporation>`), y además proporciona en ese entonces mucha más 
visibilidad e interés en torno a Zope del que jamas *Principia* tuvo antes.

En julio de 1999 Zope 1.10.3 fue publicado [#cite_note-6]_ como primer revisión estable del
proyecto y unos meses después en septiembre de 1999 fue publicado [#cite_note-7]_ Zope 2.0.0 
como versión estable. 
En noviembre de 2004 fue publicado :ref:`Zope 3 <bluebream>`, es casi completamente reescrito 
y contiene sólo la :ref:`base de datos orientada a objeto ZODB <que_es_zodb>` y el 
:ref:`motor de plantillas ZPT <lenguajes_plantillas>`.


Características
---------------

Siendo Zope un `servidor de aplicaciones web`_ ofrece una mezcla única de características, 
algunas son similares y otras muy diferentes de las que ofrecen otros soluciones existentes:

-  Cumple con los estándares `XHTML`_ y `CSS`_.

-  Soporte a plantillas con HTML5 y CCS3.

-  Operaciones sobre registros como *Cortar / Copiar / Pegar*.

-  `Motor de workflow`_ integrado.

-  Configuración del :term:`Flujo de trabajo` de forma localizada.

-  Soporta comportamiento tipo `Wiki`_.

-  Mecanismos de colaboración en la construcción colectiva de contenidos.

-  Compartir documentos de otros usuarios y otorgar permisos específicos.

-  Gestión del histórico de reversiones de documento, con posibilidad de 
   comparar versiones y la anulación de cambios realizados.

-  Soporte para múltiples formatos de `marcado`_.

-  Altos niveles de seguridad.

-  Motor de búsqueda integrado, indexación en tiempo real (todo el contenido 
   están indexados).

-  Gestión de contenido multilingüe.

-  `Localización`_ de la interfaz en modo nativo.

-  Reducción de tamaño de los recursos multimedia.

-  Modulable a través de :ref:`Productos adicionales <modulable_zope>`, evolutivo y fácilmente personalizable.

-  :ref:`Arquitectura abierta <arquitectura_componentes_zope>` y escalable.

-  Autenticación del `back-end`_ a través de `PAS`_ / `LDAP`_ / `SSO`_ / Auth\_tkt.

-  Administración de encabezados HTML para Caching.

-  Integración con `proxy Caché`_.

-  Paquetes de instalación para `múltiples plataformas`_.

-  Soporta `WebDAV`_ [#cite_note-8]_ y `FTP`_ [#cite_note-9]_.

-  Brinda soporte de `copia de seguridad`_.

A continuación se presenta las frecuentes ventajas y desventajas de los
`servidores de aplicaciones web`_ alternativos a Zope:

+---------------------------------------+---------------------------------------+
| Otros servidor de aplicaciones        |  Zope                                 |
+=======================================+=======================================+
| No tienen un interfaz administrativa  | Posee un interfaz administrativa de   |
| sencilla y por lo tanto algo son      |  usuario muy sencillo.                |
| complicados de manejar.               |                                       |
+---------------------------------------+---------------------------------------+
| Muchas veces requieren una            | Es fácil de instalar y no requiere    |
| configuración muy compleja.           | configuraciones ser utilizarlo.       |
+---------------------------------------+---------------------------------------+
| Requieren de productos adicionales    | Trabaja con cualquier Navegador       |
| para el desarrollo y además son       | estándar y no requiere herramientas   |
| propietarios.                         | adicionales.                          |
+---------------------------------------+---------------------------------------+
| Algunas aplicaciones no escalan de    | Dispone de un sistema de gestión      |
| la misma manera que Zope le permite   | poderoso y consistente que permite su |
| a un amplio número de usuarios        | escalabilidad a múltiples usuarios    |
| y programadores.                      | con una única y fácil gestión de      |
|                                       | privilegios.                          |
+---------------------------------------+---------------------------------------+
| La mayoría son herramientas           | Es un software libre.                 |
| comerciales con código cerrado que    |                                       |
| le impide la extensión,               |                                       |
| personalización y distribución.       |                                       |
+---------------------------------------+---------------------------------------+

.. _beneficios_zope:

Beneficios de Zope
------------------

Existente una serie de beneficios al adaptar Zope en su organización a
continuación se describen:

.. _modulable_zope:

Modulable
~~~~~~~~~

La funcionalidad de Zope puede ser extendida gracias a un gran número de extensiones 
disponibles libremente, estos son comúnmente llamados :ref:`Productos <productos_addons_modulos>` 
(del Inglés: Products) y para ser adaptados a las necesidades, ejemplo de esto son 
`sistema de Wiki`_ como `Zwiki`_, sistema de publicación de noticias y discusiones como 
`Squishdot`_, `álbum de fotografías`_ como `PhotosCommandes`_, Calendarios corporativos 
con `CorpCalendar`_ entre otros productos que son desarrollados y mantenidos por la 
comunidad de usuarios en la sección de `productos de Zope.org`_, lista de productos en 
`Open Source Content Management Software`_.

Estas extensiones están colocadas cada una en su propio directorio en el sistema de archivos 
y se puede remover completamente mediante la eliminación del directorio y reiniciar nuevo el 
servicio de Zope. 
Tendrán toda la extensión de la programación en lenguaje :ref:`Python <python_index>` 
que este disponible, incluyendo la integración de bibliotecas escritas en :ref:`Python <python_index>` 
o `lenguaje C`_.

Portabilidad
~~~~~~~~~~~~

Zope es casi enteramente en escrito :ref:`Python <python_index>`. Sólo algunas partes del 
sistema están escrito en `lenguaje C`_ por críticos de velocidad. Todo el sistema puede así, 
en principio, estar disponible en todas las plataformas con un intérprete :ref:`Python <python_index>` 
y un compilador C para ejecutarse.
Para `GNU/Linux`_, `Windows`_, `BSD`_, `Mac OS X`_ y `Solaris`_ hay disponibles paquetes previamente
compilados que incluyen Zope y :ref:`Python <python_index>`.

Adquisición
~~~~~~~~~~~

Se trata de uno de los mecanismos más potentes de Zope. Gracias a él,
los objetos pueden obtener atributos, métodos y otros objetos del
entorno que están en un "sub-árbol heredados completamente". Es similar a
la herencia, solo que en vez de buscar en la jerarquía de objetos
utiliza contenedores jerárquicos. De esta manera, si una variable no se
encuentra en el contenedor actual se busca en los contenedores
superiores, hasta dar con su valor. De esta forma se pueden centralizar
valores que son luego adquiridos por toda una jerarquía de objetos. Este
mecanismo es la base principal para decir de tener sitios dinámicos
hechos con Zope.

Seguridad
~~~~~~~~~

Zope tiene un framework de seguridad que le permite a los llamados roles
que construyen una definición detallada sobre "quien, donde y que" puede
hacerse. Para cada objeto se puede determinar cuál es el rol que se
necesita para el tipo de acceso, estos roles pueden usuarios
individuales a los cuales también pueden asignarse localmente, por
ejemplo, para conceder acceso únicamente a una determinada sub-árbol.

Además, el trabajo de los internautas no les gusta interactuar con
lenguajes scripting clásicos como `PHP`_, `Perl`_, etc, en el sistema de 
archivos del servidor y menos en un entorno virtual separado. Para romper 
con esta practica de como hacer sitios dinámicos Web solamente posible cuando 
el programador desee adoptar nuevos patrones de trabajo. La tecnología Zope 
impide el acceso a otra información almacenada en el servidor y por
consiguiente alterar los patrones comunes de ataque informáticos.

Escalabilidad
~~~~~~~~~~~~~

Zope tiene la capacidad `multihilo`_. La distribución de la carga de una 
instancia de Zope para múltiples procesadores, sino para prevenir por un 
global de bloqueo del intérprete Python. Con la ayuda de 
:ref:`Zope Enterprise Objects - ZEO <que_es_zeo>`, es posible que varios 
servidores pueden acceder a la misma base de datos. Tales sistemas distribuidos 
son capaces de hacer uso de múltiples procesadores.

Alta disponibilidad
~~~~~~~~~~~~~~~~~~~

Zope puede configurarse para escenarios donde se requieren funcionamiento de alta 
disponibilidad a través de configuraciones con Servidores Web como `Apache`_, `Nginx`_, 
Zope; con Proxies / Balanceador de Carga como `HAProxy`_, `Pound`_, `Squid`_, entre otros; 
con servidor de Cacheo Web Externo como `Varnish`_, `Squid`_, `Apache`_ y `Memcache`_; 
replicación de Base de Datos con la librería `Relstorage`_ o `Neopod`_.

.. _comunidad_zope:

Comunidad Zope
--------------

La comunidad está compuesta por los usuarios y los programadores. Muchos de los miembros 
de la comunidad son profesionales tales como consultores, programadores y `webmasters`_, 
que dedican su tiempo y dinero al soporte de Zope. Otros muchos son estudiantes y usuarios 
curiosos, que aprenden cómo usar esta herramienta.

Los encuentros presenciales formales e informales se dan de vez en cuando en `conferencias 
Python`_ o `conferencias Plone`_ pero pasa la mayor parte del tiempo discutiendo sobre Zope 
en las `listas de correo electrónico`_, por ejemplo la lista de `Zope en Español`_, y los sitios
Web de `zope.org`_. Muchos actores que cumplen muchas funciones que a continuación describimos:

Desarrolladores
~~~~~~~~~~~~~~~

Para Enero de 2013, cuenta con 230 programadores de núcleo de Zope al rededor del mundo [#cite_note-10]_.

Soporte
~~~~~~~

Para soporte oficial en Zope puede contactar a la :ref:`Zope Corporation <zope_corporation>`, 
a los proveedores de BlueBream [#cite_note-11]_ o por lo generar los proveedores de servicios de 
:ref:`Plone <soporte_plone>` ofrecen también soporte comercial en las tecnologías Zope, adicionalmente 
ofrece otros medios de asistencia técnica por medio de los `recursos comunitarios`_, que ofrece 
soporte vía chat IRC, soporte comunitario por medio de grupos activistas en tu región.

.. _fundacion_zope:

Fundación Zope
~~~~~~~~~~~~~~

Es una organización que promueve el desarrollo de la plataforma Zope mediante el apoyo a la 
comunidad que desarrolla y mantiene los componentes de software que componen la plataforma 
de software.

Sus objetivos son:

-  Ser la propietaria de los códigos fuentes, `derechos de
   autor`_, `marcas registradas`_ y `dominios en la Internet`_ de
   Zope [#cite_note-12]_.

-  Actuar como la representación legal de la comunidad Zope, sus
   usuarios, los programadores y proveedores de soluciones.

-  Gestiona los sitios web zope.org, la cual es una infraestructura de
   colaboración de código abierto.

-  Supervisar una diversa comunidad de código abierto colaboradores que
   trabajan en una variedad de proyectos relacionados.

La `fundación Zope`_ promueve a la comunidad que incluye tanto el software de código abierto, 
la documentación y la infraestructura Web de los contribuyentes, así como los clientes de 
negocios y de la organización de la plataforma de software.

Miembros nombrados
~~~~~~~~~~~~~~~~~~

Para Enero de 2013, cuenta con 49 miembros designados (una afiliación individual y libre) de 
la Fundación, [#cite_note-13]_ los miembros si quieres formar parte de la 
:ref:`fundación Zope <fundacion_zope>` puedes llenar su `solicitud`_ cumpliendo con los 
requerimientos necesarios.

.. _miembros_patrocinadores:

Miembros patrocinadores
~~~~~~~~~~~~~~~~~~~~~~~

Los miembros que deseen patrocinar económicamente a la Fundación pueden pagar membresías desde 
sólo **$399 por año**. Para Enero de 2013, la :ref:`fundación Zope <fundacion_zope>` posee 
miembros patrocinadores que proporcionan apoyo monetario a la Fundación [#cite_note-14]_.

.. _zope_corporation:

Zope Corporation
~~~~~~~~~~~~~~~~

Es una empresa que ofrece una serien de productos y servicios basados en el 
`servidor de aplicaciones`_ Zope. La Zope Corporation es :ref:`miembro patrocinador <miembros_patrocinadores>` 
de la :ref:`fundación Zope <fundacion_zope>`. 
Debido a que Zope fue una de la primeras herramientas de este tipo que se convirtió 
en software libre [#cite_note-15]_ la Zope Corporation desarrolló un modelo único de 
negocios de `código abierto`_ con el cual le permite seguir contribuyendo al continuo 
control de software a sus clientes y además le permite continuamente seguir apoyando 
el desarrollado global y vibrante en la *comunidad Zope* alrededor del sitio `zope.org`_ 
en el cual se enriquece el software, aportando complementos necesarios, suministrando 
correcciones a errores, respondiendo preguntas.

.. _productos_addons_modulos:

Productos / Addons / Módulos
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

La comunidad soporta y distribuye sus módulos a través de los sitios web de los *proveedores 
de servicios* pero la mayoría están en el :term:`PyPI`. Los cantidad de paquetes publicados 
hasta la fecha de Enero de 2013 en vía :term:`PyPI` para :ref:`Zope 2 <zope2>` son de 876 
paquetes, [#cite_note-16]_ para :ref:`Zope 3 <bluebream>` son de 930 paquetes, [#cite_note-17]_ 
para :ref:`ZODB <que_es_zodb>` son de 48 paquetes, [#cite_note-18]_ para `Pyramid`_ son de 
84 paquetes [#cite_note-19]_ y para :ref:`Buildout <que_es_zcbuildout>` son de 428 paquetes, 
[#cite_note-20]_ entre otros mas.

.. _infraestructura_servicios_zope:

Infraestructura de servicios Zope
---------------------------------

Este proporciona infraestructura y servicios que agilizan enormemente el desarrollo, que 
consiste en varios componentes diferentes que trabajan de manera conjunta para ayudarte 
a construir aplicaciones Web que se describen a continuación:
 
.. image:: images/infraestructura_servicios_zope.png
  :alt: Infraestructura de servicios Zope
  :align: center
  :width: 463px
  :height: 468px
  :target: ../_images/infraestructura_servicios_zope.png

.. _servidor_aplicaciones_web_oao:

Servidor de aplicaciones Web orientado a objeto
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Es un servicio de publicación de objeto, que se encarga de servir los contenidos tanto 
a usted como a sus usuarios, y fue el primer sistema utilizando la metodología objeto 
de publicación ahora común para la Web.
Puede que dispongas ya en su sistema de otro servidor web, como `Apache`_ o `Microsoft IIS`_ 
y no le interesa usar el servicio de Zope, no se preocupe, Zope trabaja también con 
estos servidores web modernos que soportan a `CGI`_, `HTTP`_/`WebDAV`_, `XML-RPC`_, `FTP`_ 
y `WSGI`_.

Interfaz administrativa Web
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Posee una **Interfaz basado en Web**, llamada ":ref:`Zope Management Interface - ZMI <que_es_zmi>`" 
le puede utilizar su navegador para interactuar en la gestión de Zope. Este interfaz es un entorno 
de desarrollo bajo el concepto a través de la Web, que le permite hacer cosas como: crear páginas web, 
añadir imágenes y documentos, interactuar con bases de datos relacionales externas y escribir 
:ref:`scripts en diferentes lenguajes <lenguajes_basados_scripts>`.

.. _base_datos_objetos:

Base de datos de objetos
~~~~~~~~~~~~~~~~~~~~~~~~

.. note:: Artículo principal: :ref:`Zope Object Database <que_es_zodb>`.

Posee por defecto un mecanismo de almacenamiento en una `base de datos de objetos`_, llamada 
":ref:`Zope Object Database - ZODB <que_es_zodb>`", cuando usted trabaja con Zope, la mayoría 
de la veces trabajará con objetos almacenados en la :ref:`ZODB <que_es_zodb>`. El interfaz de 
gestión de Zope proporciona una manera simple y familiar de administrar objetos que se asemeja 
bastante a la forma de trabajar con los tradicionales gestores de ficheros, pero cada objeto 
tiene propiedades, métodos u otros objetos. Esta aproximación es muy diferente de las 
`base de datos relacionales`_ habituales.

Integración con Base de datos Relacional
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Si usted no requiere almacenar su información en la :ref:`ZODB <que_es_zodb>`, Zope dispone de 
múltiples conectores a diferentes `base de datos relacionales`_ como `Oracle Database`_, `MySQL`_, 
`PostgreSQL`_, `Sybase`_ y entre otras, ofreciendo sistemas básicos de conexión y consulta 
abstrayéndolos como objetos.

.. _lenguajes_basados_scripts:

Lenguajes basados en scripts
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Ofrece **soporte de lenguajes basados en scripts**, le permite escribir aplicaciones en varios 
lenguajes diferentes como :ref:`Python <python_index>`, [#cite_note-21]_ `Perl`_, [#cite_note-22]_ 
`PHP`_, [#cite_note-23]_ `JSP`_ [#cite_note-24]_ dentro del :ref:`servidor de aplicaciones de Zope <servidor_aplicaciones_web_oao>`.

.. _lenguajes_plantillas:

Lenguajes de plantillas
~~~~~~~~~~~~~~~~~~~~~~~

La tecnologías de Zope proporciona tres mecanismos para la creación de `plantillas HTML`_:

**Document Template Markup Language (DTML)**, es un lenguaje basado en etiquetas que permite 
la ejecución de secuencias de comando simples en las plantillas. DTML ha sido el primero 
lenguaje de marcado dentro de Zope por un largo tiempo [#cite_note-25]_. DTML contiene 
disposiciones para la inclusión variable, condiciones y bucles. Sin embargo, DTML tiene 
inconvenientes importantes: etiquetas DTML intercalados con formato HTML no son válidos 
a los documentos HTML, y la inclusión descuidada de la lógica da como resultados que las 
plantillas sean un código muy ilegible.

**Zope Page Templates (ZPT)**, es una tecnología que corrige los defectos del DTML, por 
consiguiente es el lenguaje de marcado recomendado primariamente dentro de Zope es hoy 
en día [#cite_note-26]_. Las plantillas ZPT pueden ser documentos `XML`_ bien formados 
o documentos `HTML`_, debido a que presentan todas las marcas especiales como atributos 
en el namespace `Template Attribute Language - TAL`_ (Lenguaje de plantillas de atributos). 
ZPT ofrece un conjunto muy limitado de herramientas para la inclusión condicional y la 
repetición de elementos XML. En consecuencia, las plantillas son por lo general bastante 
simple, con más lógica implementada en el código :ref:`Python <python_index>`. 
Una ventaja importante de las plantillas ZPT es que se puede editar en los editores gráficos 
de `HTML`_. ZPT también ofrece soporte directo para la `internacionalización`_ de software.

**Chameleon**, es un motor de `Page Templates`_ escrito en :ref:`Python <python_index>` el 
cual se caracteriza por ser **más rápido** ya que las plantillas son compiladas a byte-code 
esto lo hace muy optimizado en su velocidad; **es extensible** ya que es fácil de extender un 
lenguaje o crearse su propio lenguaje al estilo ``taglibs`` [#cite_note-27]_ y **está probado** 
con pruebas automatizadas evitar problemas. Chameleon es una nueva implementación del motor de 
Page Templates por consiguiente hay que tener en cuentas sus diferencias e incompatibilidades 
[#cite_note-28]_.

Servidores de aplicaciones
--------------------------

El desarrollo principal del proyecto Zope ahora es mantenido por la :ref:`fundación Zope <fundacion_zope>` 
que está compuesto por miembros de la comunidad de programadores. Actualmente es independiente de 
cualquier conexión con :ref:`Zope Corporation <zope_corporation>`. En la actualidad se desarrollará 
en paralelo y activamente tres ramas principales del desarrollo que se mantienen por separado 
por la comunidad Zope:

.. _zope2:

Zope 2
~~~~~~

Un sitio web Zope se compone generalmente de objetos en una `base de datos de objetos de Zope <http://es.wikipedia.org/wiki/Zope_Object_Database>`_ no son archivos en un sistema de archivos, como es habitual en 
la mayoría de servidores web. Esto permite a los usuarios aprovechar las ventajas de las tecnologías 
de objetos, tales como encapsulación. Zope mapea las direcciones URL a objetos utilizando el árbol 
de contenidos de tales objetos, los métodos se consideran que deben figurar en sus objetos también. 
Los datos pueden ser almacenados en otras bases de datos, así, o en el sistema de archivos, pero
:ref:`ZODB <que_es_plone>` por defecto. La plataforma de aplicaciones web Zope 2 ha estado en continuo 
desarrollo como un sistema de `código abierto`_ desde 1998.

.. _bluebream:

BlueBream
~~~~~~~~~

Formalmente conocido como **Zope 3**, fue inicialmente publicado bajo ese nombre, como es una nueva 
implementación del servidor :ref:`Zope 2 <zope2>`, pero debido a la incompatibilidad entre las versiones 
del framework Zope 2 y 3, entonces fue renombrado [#cite_note-29]_ a BlueBream el 17 de enero de 2010 
para marcar diferencia de :ref:`Zope 2 <zope2>`.

Se convierte en la siguiente generación de la plataforma web desarrollada por la comunidad Zope. Fue 
publicado en 2005 como una plataforma de desarrollo orientado. Su objetivo es ofrecer una colección 
de muchos pequeños componentes que lo conforman los cuales se pueden combinar para crear potentes 
aplicaciones Web.

Con BlueBream un corte se hizo con la compatibilidad atrás con :ref:`Zope 2 <zope2>`, se decidió 
corregir los errores del pasado, volcando toda la experiencia adquirida en :ref:`Zope 2 <zope2>` 
para revisar la estructura interna fundamental del proyecto. Estos cambios incluyen una 
:ref:`arquitectura de componentes Zope <arquitectura_componentes_zope>`, un efecto secundario es 
que muchos componentes también se pueden utilizar fuera de Zope ahora en otros proyectos Python.

Para ofrecer compatibilidad hacia atrás a los componentes hechos para :ref:`Zope 2 <zope2>` 
desde BlueBream /Zope 3, puede usar el componente llamado :ref:`Five <five>`.

.. _grok:

Grok
~~~~

Es un `framework para aplicaciones web`_ de código abierto basado en la tecnología del 
:ref:`Zope Toolkit <zope_toolkit>`. El proyecto inicio en 2006 de la mano un grupo de 
programadores Zope [#cite_note-30]_. Grok desde entonces ha tenido lanzamientos regulares. 
Sus tecnologías centrales (*Martian*, *grokcore.component*) también se utiliza en otros 
proyectos basados ​​en Zope [#cite_note-31]_ [#cite_note-32]_.

El primer motivo detrás del proyecto Grok, es hacer a la tecnología del :ref:`Zope Toolkit <zope_toolkit>` 
más accesible y más fácil de usar para los recién llegados y, al mismo tiempo, a la velocidad 
de desarrollo de aplicaciones, de acuerdo con el paradigma de la `programación ágil`_ [#cite_note-33]_.

Para ello, utiliza de la convención Grok es usar la `convención sobre configuración`_ en
lugar de utilizar un lenguaje explícito de configuración basado en XML (`ZCML`_) como el 
:ref:`Zope Toolkit <zope_toolkit>` y BlueBream hacen. Grok usa código
Python para la configuración del componente, y tiene muchos valores por defecto implícitos 
y convenciones. Grok es similar en sentir a otros marcos Web de Python como `TurboGears`_,
`Pylons`_ y `Django`_ [#cite_note-34]_.

Librerías de desarrollo
-----------------------

Durante más de una década la :ref:`Zope Corporation <zope_corporation>` y la :ref:`comunidad Zope <comunidad_zope>` 
han aumentado en un sistema excepcional de productos y tecnologías, que influyen en el desarrollo 
general de Python, servidores basados ​​en aplicaciones web y herramientas. A continuación se describen 
las más importantes de ellas:

.. _arquitectura_componentes_zope:

Arquitectura de componentes Zope
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Este dispone de un `framework`_ que soporta el diseño y la `programación basada en componentes`_
llamado Arquitectura de Componentes de Zope viene del inglés ":ref:`Zope Component Architecture - ZCA <zca-es>`".
Esta funciona muy bien al desarrollar sistemas de software grandes en Python. La ZCA no es específica 
al servidor de aplicaciones Zope, se puede utilizar para desarrollar cualquier aplicación Python 
[#cite_note-35]_.

.. _zope_toolkit:

Zope Toolkit
~~~~~~~~~~~~

Del Ingles *"Zope Toolkit - ZTK"*, es un kit de herramientas para el desarrollo de Zope y fue creado 
como resultado del desarrollo de Zope 3 / BlueBream, ahora hay muchos paquetes de Python independientes 
usados y desarrollados como parte de BlueBream, y aunque muchos de estos son utilizables fuera de 
BlueBream, muchos no lo son. El proyecto Zope Toolkit (ZTK) se inició para clarificar que paquetes 
eran utilizables fuera BlueBream, y para mejorar la aptitud para la reutilización de los paquetes. 
Así, el kit de herramientas de Zope es una base para los framework de Zope. Con Zope 2.13 [#cite_note-36]_ 
fue la primera versión de un framework web que se basa en Zope Toolkit, Grok, [#cite_note-37]_ BlueBream 
[#cite_note-38]_ y Plone [#cite_note-39]_ también lo adoptaron.

Zope Content Management Framework
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note:: Artículo principal: `Zope Content Management Framework`_.

Es un conjunto de componentes construidos encima de :ref:`Zope 2 <zope2>` para ayudar en la creación de 
sistemas de gestión de contenidos. Un ampliamente conocido sistema de gestión de contenidos que emplea el 
`Zope CMF`_ es :ref:`Plone <que_es_plone>`.

.. _five:

Five
~~~~

El nombre de `proyecto Five`_ deriva el juego de palabras: *Zope 2 + 
Zope 3 = Cinco*, fue creado para solventar el problema de las incompatibilidad entre versiones Zope 2 y
Zope 3 desde el punto de vista del desarrollador de aplicaciones web, producido como resuelto una librería 
que le permite usar muchos de los conceptos y técnicas de Zope 3 en Zope 2. Gracias a esta un desarrollador 
puede migrar las aplicaciones a utilizar Zope 2 y adoptar gradualmente la :ref:`arquitectura de componente Zope 3 <arquitectura_componentes_zope>` a lo largo de una trayectoria 
continua. Five se incorporó a la distribución original de Zope 2, y cada versión posterior integra un número 
cada vez mayor de características de Zope 3.

Herramientas
------------

El proyecto Zope ha creado algunas herramientas útiles, a continuación
se describen:

Buildout
~~~~~~~~

.. note:: Artículo principal: :ref:`Buildout <que_es_zcbuildout>`.

Es un sistema de auto-construcción basado en Python para crear,
ensamblar y desplegar aplicaciones desde diversas partes a partir de
piezas múltiples, algunos de los cuales pueden ser piezas de software no
basado en Python [#cite_note-40]_.

.. _software_basado_zope:

Software basado en Zope
-----------------------

Una gran cantidad de software se ha construido en la sobre la Zope. A
continuación una lista de los proyectos más conocidos:

-  El `gestor de listas de correo`_ basado en la web de código abierto `GroupServer`_ diseñado 
   para los grandes sitios de la `lista de correo`_.

-  El `motor de Wiki`_ `Zwiki`_ el cual soporta un numero de estilos de marcado wiki como `MoinMoin`_,
   Structured text, `reStructuredText`_, permite editar paginas en `LaTeX`_ o con un editor
   `WYSIWYG`_ en `HTML`_.

-  El `sistema de gestión de contenido`_ de código abierto :ref:`Plone <que_es_plone>`,
   `Silva`_, `Zwook`_, `woost`_ y `Naaya`_ este último inicialmente desarrollado para 
   `Agencia Europea de Medio Ambiente`_.

-  `ZMS`_ es `sistema de gestión de contenido`_ de `código abierto`_ para la Ciencia, la Tecnología
   y la Medicina.

-  `KARL`_ es un sistema web de `código abierto`_ para la colaboración, intranets organizacionales 
   y gestión del conocimiento.

-  `Nuxeo Collaborative Nuxeo Portal Server - Nuxeo CPS`_ es una plataforma de `código abierto`_ 
   disponible para la construcción de aplicaciones `Enterprise Content Management (ECM)`_.

-  El `sistema de gestión documental`_ de `código abierto`_ `NauDoc`_.

-  El `sistema de planificación de recursos empresariales`_ `ERP5`_.

-  La sistema global de información estudiantil `schooltool`_.

-  El `sistema de apoyo a procesos legislativos - SAPL`_ desarrollado por el `Programa Interlegis`_
   para la `Cámara de Diputados de Brasil`_ del `gobierno de Brasil`_.

-  La `plataforma de desarrollo colaborativo de software`_ llamado `Launchpad`_ (el mismo utilizado 
   para el desarrollo de la distribución de `Ubuntu Linux`_).

-  El `framework Web`_ `Pyramid`_ y :ref:`Grok <grok>`.

-  El sistema de almacenamiento descentralizado `Tahoe-LAFS`_.

-  El sistema de eventos / conferencia digital integrado `INDICO`_ del `CERN`_.

Alternativas a Zope
-------------------

Existen muchas herramientas disponibles que te ayudan en la construcción de aplicaciones web. 
Al comienzo de la historia de la web, las aplicaciones web sencillas eran construidas casi de 
forma exclusiva mediante programas `CGIs <http://es.wikipedia.org/wiki/CGI>`_ escritos en 
`Perl`_ u otras lenguajes de la época temprana de la Web. 
Ahora hay una multitud de opciones que van desde las soluciones `código abierto`_ como `PHP`_,
:ref:`Python <python_index>`, `Ruby`_ a opciones comerciales como `ColdFusion`_ de Adobe 
(originalmente de `Allaire`_), `Java Application Servers`_ o `Story Server`_ de Vingette.

Enlaces externos
----------------

-  `Página oficial de Zope <http://www.zope.org/>`_ (en Inglés)

-  `Fundación Zope <http://foundation.zope.org/>`_ (en Inglés)

-  `Zope 2 <http://zope2.zope.org/>`_ (en Inglés)

   -  `La wiki de Zope 2 <http://wiki.zope.org/zope2>`_ (en Inglés)

   -  `Proyectos relacionados con Zope2 en el Python Package Index <http://pypi.python.org/pypi?:action=browse&show=all&c=514>`_ (en Inglés)

   -  `ZopePlone - Blog de desarrollo Plone <http://www.zopeplone.es/>`_ (en Español)
   
   -  `Zopeteca <http://www.zopeteca.com/>`_ (en Español)
   
   -  `Traducción del Zope Book (Castellano) <http://usuarios.multimania.es/zope/Indice.html>`_ (en Español)
   
   -  `Tutorial - Curso practico de Zope <http://www.programatium.com/manuales/zope/index.htm>`_ (en Español)
   
   -  `Artículo - Zope: El servidor de aplicaciones libre <http://www.programacion.com/articulo/zope:_el_servidor_de_aplicaciones_libre_69>`_ (en Español)

-  `BlueBream <http://bluebream.zope.org/>`_ (AKA Zope 3) (en Inglés)

   -  `La wiki de BlueBream <http://wiki.zope.org/bluebream>`_ (en Inglés)
   
   -  `Proyectos relacionados con Zope3 en el Python Package Index <http://pypi.python.org/pypi?:action=browse&show=all&c=515>`_ (en Inglés)
   
   -  `La wiki de Zope 3 <http://wiki.zope.org/zope3>`_ (en Inglés)
   
   -  `Zope 3 en launchpad.net <https://launchpad.net/zope3>`_ (en Inglés)
   
   -  `Ejemplos de Zope 3 <http://code.google.com/p/zope3demos>`_ (en Inglés)

-  `The Zope Book <http://www.zope.org/Documentation/Books/ZopeBook/>`_ (en Inglés)

-  `Mas wikis sobre Zope <http://wiki.zope.org/>`_ (en Inglés)

-  `Zope Corporation <http://zope.com/>`_ (en Inglés)

.. rubric:: Referencias

.. [#cite_note-1] colaboradores de Wikipedia (27 de enero del 2013). Wikipedia, La enciclopedia libre. (ed.): « `Cyprinus ballerus -
   Wikipedia, la enciclopedia libre <http://es.wikipedia.org/wiki/Cyprinus_ballerus>`_ » (en español) (Web). Consultado el 27 de enero de 2013. «conocido como zope o blue bream».
.. [#cite_note-2] Lutz, Mark (2006). « `18: Advanced Internet Topics <http://books.google.com/books?id=5zYVUIl7F0QC&lpg=PA1130&pg=PA1130#v=onepage&q=&f=false>`_ ». *Programming Python*. `O'Reilly Media <http://es.wikipedia.org/wiki/O%27Reilly_Media>`_. `http://books.google.com/books?id=5zYVUIl7F0QC&lpg=PA1130&pg=PA1130#v=onepage&q=&f=false <http://books.google.com/books?id=5zYVUIl7F0QC&lpg=PA1130&pg=PA1130#v=onepage&q=&f=false>`_. Consultado el 20 de enero de 2013. «The use of Zope has spread so quickly that many Pythonistas have looked to it as a Python *Killer Application* - a system so good that it naturally pushes Python into the development spotlight.» 
.. [#cite_note-3] Udell, Jon. «`Zope Is Python's Killer App. <http://web.archive.org/web/20000302033606/http://www.byte.com/feature/BYT20000201S0004>`_ », `BYTE <http://es.wikipedia.org/w/index.php?title=BYTE&action=edit&redlink=1>`_, 07 de febrero de 2000. Consultado el 20 de enero de 2013.
.. [#cite_note-4] Zope Foundation (2009). « `The history of Zope — The Zope 2 Application Server <http://zope2.zope.org/about-zope-2/the-history-of-zope>`_ » (en ingles). Zope Foundation. Consultado el 30 de enero de 2013.
.. [#cite_note-5] David Sims (1 de febrero de 2000). David Sims (ed.): «[www.oreillynet.com/pub/a/network/2000/01/25/interview/index.html Opening Zope: An Interview with Paul Everitt]» (en ingles) (Web). O'Reilly Network. Consultado el 27 de enero de 2013. «By 1997, the application server market was full of billion-dollar companies. It's pretty hard to crack into that kind of market.».
.. [#cite_note-6] ZopeOrgSite (19 de julio de 1999). « `Zope.org - 1.10.3 <http://old.zope.org/Products/Zope/1.10.3/1.10.3/>`_ » (en ingles). Zope Foundation. Consultado el 30 de enero de 2013.
.. [#cite_note-7] ZopeOrgSite (17 de septiembre de 1999). « `Zope.org - 2.0.0 <http://old.zope.org/Products/Zope/2.0.0-donotuseme/2.0.0/>`_ » (en ingles). Zope Foundation. Consultado el 31 de enero de 2013.
.. [#cite_note-8] Caballero G., Leonardo J. (17 de diciembre del 2012). `Configurar Zope como un servidor WebDAV <https://plone-spanish-docs.readthedocs.org/en/latest/zope/zope_como_servidor_webdav.html>`_. Plone Venezuela. `https://plone-spanish-docs.readthedocs.org/en/latest/zope/zope\_como\_servidor\_webdav.html <https://plone-spanish-docs.readthedocs.org/en/latest/zope/zope_como_servidor_webdav.html>`_. Consultado el 24 de enero de 2013. 
.. [#cite_note-9] Caballero G., Leonardo J. (17 de diciembre del 2012). `Configurar Zope como un servidor FTP <https://plone-spanish-docs.readthedocs.org/en/latest/zope/zope_como_servidor_ftp.html>`_. Plone Venezuela. `https://plone-spanish-docs.readthedocs.org/en/latest/zope/zope\_como\_servidor\_ftp.html <https://plone-spanish-docs.readthedocs.org/en/latest/zope/zope_como_servidor_ftp.html>`_. Consultado el 24 de enero de 2013. 
.. [#cite_note-10] « `The Zope Open Source Project on Ohloh : Contributors Listing Page <http://www.ohloh.net/p/zope/contributors>`_ » (en ingles). Ohloh.net. Consultado el 28 de enero de 2013.
.. [#cite_note-11] Zope Foundation. « `Companies and Contractors Providing Commercial Support for BlueBream — BlueBream v1.0 documentation <http://bluebream.zope.org/commercial.html>`_ » (en ingles). Consultado el 29 de enero de 2013.
.. [#cite_note-12] Zope Corporation. « `Zope Corporation \| Zope Corporation Trademark Management Open Letter <http://www.zope.com/about_us/legal/ZopeCorpTrademarkManagement_OpenLetter.html>`_ » (en ingles). Zope Corporation. Consultado el 29 de enero de 2013.
.. [#cite_note-13] « `Nominated members - Zope Foundation <http://foundation.zope.org/members/nominated_members>`_ » (en ingles). Zope Foundation. Consultado el 28 de enero de 2013.
.. [#cite_note-14] « `Sponsorship members — Zope Foundation <http://foundation.zope.org/members/sponsorship_members>`_ » (en ingles). Zope Foundation. Consultado el 28 de enero de 2013.
.. [#cite_note-15] Díaz Asenjo, Nacho; Pelletier, Michel; Latteier, Amos (10 de febrero de 2001). « `Capítulo 1: Introducción a Zope <http://usuarios.multimania.es/zope/Capitulo1.html>`_ » (en Español, HTML). *Zope Book (Castellano)*. New Riders Publishing. `http://usuarios.multimania.es/zope/Capitulo1.html <http://usuarios.multimania.es/zope/Capitulo1.html>`_. Consultado el 29 de enero de 2013. «Zope fue una de la primeras herramientas de este tipo que se convirtió en software libre.» 
.. [#cite_note-16] « `Framework :: Zope2 : Browse : Python Package Index <http://pypi.python.org/pypi?:action=browse&show=all&c=514>`_ » (en ingles). Pypi.python.org. Consultado el 28 de enero de 2013.
.. [#cite_note-17] « `Framework :: Zope3 : Browse : Python Package
   Index <http://pypi.python.org/pypi?:action=browse&show=all&c=515>`_ »
   (en ingles). Pypi.python.org. Consultado el 28 de enero de 2013.
.. [#cite_note-18] « `Framework :: ZODB : Browse : Python Package
   Index <http://pypi.python.org/pypi?:action=browse&show=all&c=513>`_ »
   (en ingles). Pypi.python.org. Consultado el 28 de enero de 2013.
.. [#cite_note-19] « `Framework :: Pyramid : Browse : Python
   Package
   Index <http://pypi.python.org/pypi?:action=browse&show=all&c=582>`_ »
   (en ingles). Pypi.python.org. Consultado el 28 de enero de 2013.
.. [#cite_note-20] « `Framework :: Buildout : Browse : Python
   Package
   Index <http://pypi.python.org/pypi?:action=browse&show=all&c=512>`_ »
   (en ingles). Pypi.python.org. Consultado el 28 de enero de 2013.
.. [#cite_note-21] Zope Developers Community. « `9. Basic Zope
   Scripting — Zope 2 v2.x
   documentation <http://docs.zope.org/zope2/zope2book/BasicScripting.html>`_ »
   (en ingles). Zope.org. Consultado el 27 de enero de 2013.
.. [#cite_note-22] Roberts, Michael (01 de abril de 2001) (en
   Ingles). `Zope for the Perl/CGI
   programmer <http://www.ibm.com/developerworks/library/l-zope/index.html>`_.
   developerWorks Content/Raleigh/IBM.
   `http://www.ibm.com/developerworks/library/l-zope/index.html <http://www.ibm.com/developerworks/library/l-zope/index.html>`_.
   Consultado el 27 de enero de 2013. 
.. [#cite_note-23] Wei He (1 de julio de 2005). « `Zope.org -
   PHParser/PHPGateway <http://old.zope.org/Members/hewei/PHParser/>`_ »
   (en ingles). Zope.org. Consultado el 27 de enero de 2013.
.. [#cite_note-24] Ioan Coman (11 de marzo de 2004). « `Zope.org -
   Jsp for Zope <http://old.zope.org/Members/Ioan/ZopeJsp/>`_ » (en
   ingles). Zope Foundation. Consultado el 30 de enero de 2013.
.. [#cite_note-25] Zope Developers Community (2010). « `16. Basic
   DTML <http://docs.zope.org/zope2/zope2book/DTML.html>`_ » (en
   Ingles). *The Zope2 Book*. Zope Developers Community.
   `http://docs.zope.org/zope2/zope2book/DTML.html <http://docs.zope.org/zope2/zope2book/DTML.html>`_.
   Consultado el 29 de enero de 2013. «DTML has been the primary markup
   language within Zope for a long time.» 
.. [#cite_note-26] Zope Developers Community (2010). « `16. Basic
   DTML <http://docs.zope.org/zope2/zope2book/DTML.html>`_ » (en
   Ingles). *The Zope2 Book*. Zope Developers Community.
   `http://docs.zope.org/zope2/zope2book/DTML.html <http://docs.zope.org/zope2/zope2book/DTML.html>`_.
   Consultado el 29 de enero de 2013. «However the recommended primary
   markup language within Zope is nowadays ZPT (Zope Page Templates)» 
.. [#cite_note-27] Roberto Canales Mora (5 de julio de 2003).
   « `TagLibs y
   JSPs <http://www.adictosaltrabajo.com/tutoriales/pdfs/taglibs.pdf>`_ »
   (en español). AdictosAlTrabajo.com. Archivado desde el
   `original <http://www.adictosaltrabajo.com/tutoriales/tutoriales.php?pagina=taglibs>`_
   el 2 de enero de 2006. Consultado el 29 de enero de 2013.
.. [#cite_note-28] Borch, Malthe; Repoze Community (2011). « `Zope
   Page Templates — Chameleon 2.0
   documentation <http://chameleon.repoze.org/docs/latest/zpt.html#incompatibilities-and-differences>`_ »
   (en Ingles). *Repoze Community* (Repoze Community).
   `http://chameleon.repoze.org/docs/latest/zpt.html#incompatibilities-and-differences <http://chameleon.repoze.org/docs/latest/zpt.html#incompatibilities-and-differences>`_.
   Consultado el 29 de enero de 2013. 
.. [#cite_note-29] Muthukadan, Baiju; Combelles Christophe,
   Khabibullin Ilshad, Tenney Kent, Haubenwallner Michael, McDonough
   Chris, Nilsson Daniel (29 de agosto de 2011) (en Ingles). `1.
   Introduction — BlueBream v1.0b4
   documentation <http://bluebream.zope.org/doc/1.0/introduction.html#overview>`_.
   Zope Foundation.
   `http://bluebream.zope.org/doc/1.0/introduction.html#overview <http://bluebream.zope.org/doc/1.0/introduction.html#overview>`_.
   Consultado el 27 de enero de 2013. 
.. [#cite_note-30] Martijn Faassen (9 de noviembre de 2006). Martijn
   Faassen (ed.): « `Grok: or what I did on my
   holiday <http://blog.startifact.com/posts/older/grok-or-what-i-did-on-my-holiday.html>`_ »
   (en ingles). Consultado el 27 de enero de 2013.
.. [#cite_note-31] Lennart Regebro (26 de abril de 2008). Lennart
   Regebro (ed.): « `Announcing five.grok: Grok on Zope 2! « Lennart
   Regebro: Python, Plone,
   Web <http://regebro.wordpress.com/2008/04/26/announcing-fivegrok-grok-on-zope-2/>`_ »
   (en ingles). Consultado el 27 de enero de 2013.
.. [#cite_note-32] Martin Aspeli (28 de agosto de 2008).
   « `Dexterity meet Grok — Martin
   Aspeli <http://martinaspeli.net/articles/dexterity-meet-grok>`_ »
   (en ingles). Consultado el 27 de enero de 2013.
.. [#cite_note-33] The Grok Community. « `Why Grok? —
   Grok <http://grok.zope.org/about/why-grok>`_ » (en ingles). The Grok
   Community. Consultado el 27 de enero de 2013.
.. [#cite_note-34] The Grok Community. « `Competition —
   Grok <http://grok.zope.org/about/competition>`_ » (en ingles). The
   Grok Community. Consultado el 27 de enero de 2013.
.. [#cite_note-35] Muthukadan, Baiju; Gil Sanchez, Lorenzo;
   Haubenwallner, Michael; Quintana, Nando; Klein, Stephane; Cook, Tim;
   Gill, Kamal; Herve, Thomas (24 de noviembre de 2009) (en Ingles). `A
   Comprehensive Guide to Zope Component Architecture <http://www.muthukadan.net/docs/zca.html>`_. India:
   Baiju Muthukadan. pp. 102.
   `http://www.muthukadan.net/docs/zca.html <http://www.muthukadan.net/docs/zca.html>`_.
   Consultado el 27 de enero de 2013. 
.. [#cite_note-36] Zope Foundation and Contributors. « `Zope2
   2.13.19 : Python Package
   Index <http://pypi.python.org/pypi/Zope2/#a2-2010-07-13>`_ » (en
   ingles). Zope Foundation. Consultado el 28 de enero de 2013.
.. [#cite_note-37] The Grok Community. « `Grok 1.2 released! —
   Grok <http://grok.zope.org/blog/grok-1.2-released>`_ » (en ingles).
   The Grok Community. Consultado el 28 de enero de 2013.
.. [#cite_note-38] Zope Foundation and Contributors. « `bluebream
   1.0 : Python Package
   Index <http://pypi.python.org/pypi/bluebream#features>`_ » (en
   ingles). Zope Foundation. Consultado el 28 de enero de 2013.
.. [#cite_note-39] Aspeli, Martin (12 de noviembre de 2009) (en
   Ingles). `What is Grok and five.grok? — Plone CMS: Open Source
   Content
   Management <http://plone.org/products/dexterity/documentation/manual/five.grok/background/what-is-grok-and-five.grok>`_.
   Plone.org.
   `http://plone.org/products/dexterity/documentation/manual/five.grok/background/what-is-grok-and-five.grok <http://plone.org/products/dexterity/documentation/manual/five.grok/background/what-is-grok-and-five.grok>`_.
   Consultado el 28 de enero de 2013. 
.. [#cite_note-40] Leonardo J. Caballero G. (17 de diciembre del
   2012). « `Replicación de proyectos Python — Documentación en Español
   de
   Plone <https://plone-spanish-docs.readthedocs.org/en/latest/buildout/replicacion_proyectos_python.html>`_ »
   (en español). Documentación en Español de Plone. Consultado el 29 de
   enero de 2013.

Obtenido de «`http://es.wikipedia.org/w/index.php?title=Zope&oldid=69880666 <http://es.wikipedia.org/w/index.php?title=Zope&oldid=69880666>`_».

.. _2.13.19: http://zope2.zope.org/releases
.. _4.0a1: http://docs.zope.org/zope2/releases/4.0/INSTALL.html
.. _Servidor de aplicaciones: http://es.wikipedia.org/wiki/Servidor_de_aplicaciones
.. _Multiplataforma: http://es.wikipedia.org/wiki/Multiplataforma
.. _GNU/Linux: http://es.wikipedia.org/wiki/GNU/Linux
.. _Windows: http://es.wikipedia.org/wiki/Microsoft_Windows
.. _Mac OS X: http://es.wikipedia.org/wiki/Mac_OS_X
.. _BSD: http://es.wikipedia.org/wiki/BSD
.. _Solaris: http://es.wikipedia.org/wiki/Solaris_(sistema_operativo)
.. _Zope Public License: http://es.wikipedia.org/wiki/Zope_Public_License
.. _sitios web: http://es.wikipedia.org/wiki/Sitio_web
.. _servidor de aplicaciones web: http://es.wikipedia.org/wiki/Servidor_de_aplicaciones
.. _orientado al objeto: http://es.wikipedia.org/wiki/Programaci%C3%B3n_orientada_a_objetos
.. _lenguaje de programación: http://es.wikipedia.org/wiki/Lenguaje_de_programaci%C3%B3n
.. _lenguaje C: http://es.wikipedia.org/wiki/Lenguaje_C
.. _código abierto: http://es.wikipedia.org/wiki/C%C3%B3digo_abierto
.. _acrónimo: http://es.wikipedia.org/wiki/Acr%C3%B3nimo
.. _Cyprinus ballerus: http://es.wikipedia.org/wiki/Cyprinus_ballerus
.. _aplicación determinante: http://es.wikipedia.org/wiki/Aplicaci%C3%B3n_asesina
.. _Fredericksburg (Virginia): http://es.wikipedia.org/wiki/Fredericksburg_(Virginia)
.. _periódicos: http://es.wikipedia.org/wiki/Peri%C3%B3dico_(publicaci%C3%B3n)
.. _Paul Everitt: http://pauleveritt.wordpress.com/
.. _Rob Page: http://www.zope.com/about_us/management/rob_page.html
.. _Jim Fulton: http://www.zope.com/about_us/management/james_fulton.html
.. _Common Gateway Interface - CGI: http://es.wikipedia.org/wiki/Common_Gateway_Interface
.. _Digital Creations: http://www.digicool.com/
.. _Hadar Pedhazur: http://www.zope.com/about_us/management/hadar_pedhazur.html
.. _ORB: http://es.wikipedia.org/wiki/Object_Request_Broker
.. _lenguaje de scripting: http://es.wikipedia.org/wiki/Lenguaje_de_scripting
.. _base de datos orientada a objetos: http://es.wikipedia.org/wiki/Base_de_datos_orientada_a_objetos
.. _servidor de aplicaciones: http://es.wikipedia.org/wiki/Servidor_de_aplicaciones
.. _soluciones propietarias: http://es.wikipedia.org/wiki/Software_propietario
.. _XHTML: http://es.wikipedia.org/wiki/XHTML
.. _CSS: http://es.wikipedia.org/wiki/CSS
.. _Motor de workflow: http://es.wikipedia.org/wiki/Flujos_de_trabajo
.. _Wiki: http://es.wikipedia.org/wiki/Wiki
.. _marcado: http://es.wikipedia.org/wiki/Lenguaje_de_marcado
.. _Localización: http://es.wikipedia.org/wiki/Internacionalizaci%C3%B3n_y_localizaci%C3%B3n
.. _back-end: http://es.wikipedia.org/wiki/Back-end
.. _PAS: http://developer.plone.org/reference_manuals/old/pluggable_authentication_service/index.html
.. _LDAP: http://es.wikipedia.org/wiki/LDAP
.. _SSO: http://es.wikipedia.org/wiki/SSO
.. _proxy Caché: http://es.wikipedia.org/wiki/Proxy_cach%C3%A9
.. _múltiples plataformas: http://es.wikipedia.org/wiki/Multiplataforma
.. _WebDAV: http://es.wikipedia.org/wiki/WebDAV
.. _FTP: http://es.wikipedia.org/wiki/File_Transfer_Protocol
.. _copia de seguridad: http://es.wikipedia.org/wiki/Copia_de_seguridad
.. _servidores de aplicaciones web: http://es.wikipedia.org/wiki/Servidor_de_aplicaciones
.. _PHP: http://es.wikipedia.org/wiki/PHP
.. _Perl: http://es.wikipedia.org/wiki/Perl
.. _sistema de Wiki: http://es.wikipedia.org/wiki/Wiki_software
.. _Zwiki: http://zwiki.org/
.. _Squishdot: http://old.zope.org/Members/chrisw/Squishdot/
.. _álbum de fotografías: http://es.wikipedia.org/wiki/Fotograf%C3%ADas_digitales
.. _PhotosCommandes: http://old.zope.org/Members/nledez/PhotosCommandes/swpackage_view
.. _CorpCalendar: http://old.zope.org/Members/malikz/CorpCalendar/swpackage_view
.. _productos de Zope.org: http://old.zope.org/Products/index.html
.. _Open Source Content Management Software: http://www.contentmanagementsoftware.info/zope
.. _multihilo: http://es.wikipedia.org/wiki/Hilo_de_ejecuci%C3%B3n
.. _Apache: http://es.wikipedia.org/wiki/Apache_HTTP_Server
.. _Nginx: http://es.wikipedia.org/wiki/Nginx
.. _HAProxy: http://haproxy.1wt.eu/
.. _Pound: http://es.wikipedia.org/wiki/Pound_-_Servidor_Proxy_Reverso
.. _Squid: http://es.wikipedia.org/wiki/Squid_(programa)
.. _Varnish: http://varnish-cache.org/
.. _Memcache: http://es.wikipedia.org/wiki/Memcached
.. _Relstorage: http://pypi.python.org/pypi/RelStorage
.. _Neopod: http://www.neoppod.org/
.. _webmasters: http://es.wikipedia.org/wiki/Webmaster
.. _conferencias Python: http://www.pycon.org/
.. _conferencias Plone: http://www.ploneconf.org/
.. _listas de correo electrónico: https://mail.zope.org/mailman/listinfo/
.. _Zope en Español: https://mail.zope.org/mailman/listinfo/zope-es
.. _zope.org: http://zope.org
.. _recursos comunitarios: http://www.zope.org/front-page/2/community
.. _derechos de autor: http://es.wikipedia.org/wiki/Derecho_de_autor
.. _marcas registradas: http://es.wikipedia.org/wiki/Marca_(registro)
.. _dominios en la Internet: http://es.wikipedia.org/wiki/Dominio_de_Internet
.. _fundación Zope: http://foundation.zope.org/
.. _solicitud: http://foundation.zope.org/members/join
.. _Zope Content Management Framework: http://es.wikipedia.org/wiki/Zope_Content_Management_Framework
.. _sistema de gestión de contenido: http://es.wikipedia.org/wiki/Sistema_de_gesti%C3%B3n_de_contenidos
.. _Agencia Europea de Medio Ambiente: http://es.wikipedia.org/wiki/Agencia_Europea_de_Medio_Ambiente
.. _Pyramid: http://docs.pylonsproject.org/projects/pyramid/en/latest/index.html
.. _Microsoft IIS: http://es.wikipedia.org/wiki/Internet_Information_Services
.. _CGI: http://es.wikipedia.org/wiki/Interfaz_de_entrada_com%C3%BAn
.. _HTTP: http://es.wikipedia.org/wiki/HTTP
.. _XML-RPC: http://es.wikipedia.org/wiki/XML-RPC
.. _WSGI: http://en.wikipedia.org/wiki/Web_Server_Gateway_Interface
.. _base de datos de objetos: http://es.wikipedia.org/wiki/Base_de_datos_orientada_a_objetos
.. _base de datos relacionales: http://es.wikipedia.org/wiki/Base_de_datos_relacional
.. _PostgreSQL: http://es.wikipedia.org/wiki/PostgreSQL
.. _Oracle Database: http://es.wikipedia.org/wiki/Oracle_Database
.. _MS SQL: http://es.wikipedia.org/wiki/MS_SQL
.. _Sybase: http://es.wikipedia.org/wiki/Sybase#Gestores_de_bases_de_datos
.. _MySQL: http://es.wikipedia.org/wiki/MySQL
.. _JSP: http://es.wikipedia.org/wiki/JSP
.. _plantillas HTML: http://en.wikipedia.org/wiki/Template_(software_engineering)
.. _XML: http://es.wikipedia.org/wiki/XML
.. _HTML: http://es.wikipedia.org/wiki/HTML
.. _internacionalización: http://es.wikipedia.org/wiki/Internacionalizaci%C3%B3n_y_localizaci%C3%B3n
.. _Template Attribute Language - TAL: http://en.wikipedia.org/wiki/Template_Attribute_Language
.. _Page Templates: http://pagetemplates.org/
.. _framework para aplicaciones web: http://es.wikipedia.org/wiki/Framework_para_aplicaciones_web
.. _programación ágil: http://es.wikipedia.org/wiki/Metodolog%C3%ADa_%C3%A1gil
.. _convención sobre configuración: http://es.wikipedia.org/wiki/Convenci%C3%B3n_sobre_Configuraci%C3%B3n
.. _ZCML: http://docs.zope.org/zope.component/zcml.html
.. _TurboGears: http://es.wikipedia.org/wiki/TurboGears
.. _Pylons: http://en.wikipedia.org/wiki/Pylons_project
.. _Django: http://es.wikipedia.org/wiki/Django_(framework)
.. _programación basada en componentes: https://es.wikipedia.org/wiki/Programacion_basada_en_componentes
.. _framework: http://es.wikipedia.org/wiki/Framework
.. _Zope CMF: http://es.wikipedia.org/wiki/Zope_Content_Management_Framework
.. _proyecto Five: http://wiki.zope.org/zope2/Five
.. _gestor de listas de correo: http://es.wikipedia.org/wiki/Lista_de_correo_electr%C3%B3nico#Servicios_de_listas_de_correo_electr.C3.B3nico
.. _GroupServer: http://groupserver.org/groupserver
.. _lista de correo: http://es.wikipedia.org/wiki/Lista_de_correo
.. _motor de Wiki: http://es.wikipedia.org/wiki/Wiki_software
.. _MoinMoin: http://es.wikipedia.org/wiki/MoinMoin
.. _reStructuredText: http://es.wikipedia.org/wiki/ReStructuredText
.. _LaTeX: http://es.wikipedia.org/wiki/LaTeX
.. _WYSIWYG: http://es.wikipedia.org/wiki/WYSIWYG
.. _Silva: http://infrae.com/products/silva
.. _Zwook: http://www.zwook.org/fr
.. _woost: http://www.woost.info/es
.. _Naaya: http://en.wikipedia.org/wiki/Naaya
.. _ZMS: http://www.zms-publishing.com/
.. _KARL: http://karlproject.org/
.. _Nuxeo Collaborative Nuxeo Portal Server - Nuxeo CPS: http://cps-cms.org/sections/index-en
.. _Enterprise Content Management (ECM): http://en.wikipedia.org/wiki/Enterprise_Content_Management
.. _sistema de gestión documental: http://es.wikipedia.org/wiki/Document_management_system
.. _NauDoc: http://www.naudoc.ru/en/
.. _sistema de planificación de recursos empresariales: http://es.wikipedia.org/wiki/Sistema_de_planificaci%C3%B3n_de_recursos_empresariales
.. _ERP5: http://www.erp5.com/
.. _schooltool: http://www.schooltool.org/
.. _sistema de apoyo a procesos legislativos - SAPL: http://www.coactivate.org/projects/ploneve/instalando-sapl
.. _Programa Interlegis: http://www.interlegis.leg.br/institucional/acerca-de-interlegis
.. _Cámara de Diputados de Brasil: http://es.wikipedia.org/wiki/C%C3%A1mara_de_Diputados_de_Brasil
.. _gobierno de Brasil: http://es.wikipedia.org/wiki/Gobierno_de_Brasil
.. _plataforma de desarrollo colaborativo de software: http://es.wikipedia.org/wiki/Forja_(software)
.. _Launchpad: http://es.wikipedia.org/wiki/Launchpad
.. _Ubuntu Linux: http://es.wikipedia.org/wiki/Ubuntu_Linux
.. _framework Web: http://es.wikipedia.org/wiki/Framework_web
.. _Tahoe-LAFS: https://tahoe-lafs.org/trac/tahoe-lafs
.. _INDICO: http://indico-software.org/
.. _CERN: http://es.wikipedia.org/wiki/CERN
.. _Ruby: http://es.wikipedia.org/wiki/Ruby_on_Rails
.. _ColdFusion: http://es.wikipedia.org/wiki/ColdFusion
.. _Allaire: http://en.wikipedia.org/wiki/Allaire_Corporation
.. _Java Application Servers: http://es.wikipedia.org/wiki/Java_EE
.. _Story Server: http://en.wikipedia.org/wiki/StoryServer