.. -*- coding: utf-8 -*-

.. _zca-es:

==============================================================
Una guía comprensiva de la Arquitectura de Componentes de Zope
==============================================================

:Author: Baiju M
:Version: 0.5.6
:Printed Book: `http://www.lulu.com/content/1561045
                    <http://www.lulu.com/content/1561045>`_
:PDF en linea: `http://www.muthukadan.net/docs/zca.pdf
                  <http://www.muthukadan.net/docs/zca.pdf>`_
:Traductor(es): Lorenzo Gil Sanchez <lgs@sicem.biz>, 
                Leonardo Caballero <leonardoc@plone.org> 2011 - 2015
:URL en español: `http://www.muthukadan.net/docs/zca-es.pdf
                  <http://www.muthukadan.net/docs/zca-es.pdf>`_

Todos los derechos (C) 2007,2008 Baiju M <baiju.m.mail AT gmail.com>.

Se permite la copia, distribución y/o modificación de este documento
bajo los términos de la Licencia de Documentación Libre GNU, Versión
1.2 o (si lo prefiere) cualquier otra versión posterior publicada por
la Free Software Foundation.

El código fuente en este documento está sujeto a la Licencia
Pública Zope, Versión 2.1 (ZPL).

THE SOURCE CODE IN THIS DOCUMENT AND THE DOCUMENT ITSELF IS PROVIDED
"AS IS" AND ANY AND ALL EXPRESS OR IMPLIED WARRANTIES ARE DISCLAIMED,
INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF TITLE,
MERCHANTABILITY, AGAINST INFRINGEMENT, AND FITNESS FOR A PARTICULAR
PURPOSE.

.. sidebar:: Agradecimientos

  Muchas personas me han ayudado a escribir este libro.  EL borrador inicial fue
  revisado por mi colega Brad Allen.  Cuando yo anuncie este libro
  a través de mi blog, Tengo muchos comentarios alentadores para continuar con
  este trabajo.  Kent Tenney edito la mayor parte del libro, el también
  escribió de nuevo la aplicación ejemplo.  Muchos otros me enviaron correcciones y
  comentarios incluyendo, Lorenzo Gil Sanchez, Leonardo Caballero, Michael Haubenwallner,
  Nando Quintana, Stephane Klein, Tim Cook, Kamal Gill y Thomas
  Herve.  Lorenzo y Leonardo tradujo este trabajo al Español y Stephane
  traducido este al Francés.  Gracias a todos !

.. contents::
.. sectnum::


Primeros pasos
---------------

Introducción
~~~~~~~~~~~~

Desarrollar un sistema software grande es siempre muy complicado.  Se
ha visto que un enfoque orientado a objetos para el análisis, diseño
y programación funciona bien al tratar con sistemas grandes.  El diseño
basado en componentes, y la programación utilizando componentes se
están haciendo muy populares últimamente.  Hay muchos marcos de trabajo
que soportan el diseño basado en componentes en diferentes lenguajes,
algunos incluso son neutrales con respecto al lenguaje.  Ejemplos de esto son el COM de Microsoft y el XPCOM de Mozilla.

La **Arquitectura de Componentes de Zope (ZCA)** es un marco de trabajo
en Python que soporta el diseño y la programación basada en componentes.  La ZCA funciona muy bien al desarrollar sistemas de software grandes en
Python.  La ZCA no es específica al servidor de aplicaciones Zope, se
puede utilizar para desarrollar cualquier aplicación Python.  Quizás debería llamarse la 
`Arquitectura de Componentes de Python`.

El objetivo fundamental de la arquitectura de componentes de Zope es
utilizar objetos Python de forma eficiente  Los componentes son objetos
reusables con introspección para sus interfaces.  Un componente provee
una interfaz implementada en una clase, o cualquier objeto llamable.  No importa cómo se implemente el componente, lo que importa es
que cumpla los contratos definidos en su interfaz.  Utilizando la arquitectura de componentes de Zope puedes distribuir la complejidad
de sistemas entre varios componentes cooperantes.
La arquitectura de
componentes de Zope te ayuda a crear dos tipos básicos de componentes:
`adaptador` y `utilidad`.

Hay dos paquetes principales relacionados con la arquitectura de
componentes de Zope:

  - ``zope.interface`` utilizado para definir la interfaz de un 
    componente.

  - ``zope.component`` se encarga de registrar y recuperar
    componentes.

Recuerda, la ZCA no trata sobre los componentes en sí mismo, sino sobre
la creación, registro y recuperación de los componentes.  Recuerda
también, un `adaptador` es una clase Python normal (o una fábrica en
general) y una `utilidad` es un objeto llamable Python normal.

El marco de trabajo de la ZCA se desarrolla como parte del proyecto Zope 3.  La ZCA, como ya se ha mencionado, es un marco de trabajo
puramente Python, por tanto se puede utilizar en cualquier tipo de
aplicación Python.  Actualmente ambos proyectos Zope 3 y Zope 2 utilizan
este marco de trabajo extensivamente.  Hay otros muchos proyectos
incluyendo aplicaciones no web que utilizan la Arquitectura de
Componentes de Zope [#projects]_.

.. [#projects] http://wiki.zope.org/zope3/ComponentArchitecture


Una breve historia
~~~~~~~~~~~~~~~~~~

El proyecto del marco de trabajo ZCA comenzó en 2001 como parte del
proyecto Zope 3.  Fue tomando forma a partir de las lecciones aprendidas
al desarrollar sistemas software grandes usando Zope 2.  Jim Fulton fue el jefe de proyecto de este proyecto.
Mucha gente contribuyó al diseño
y a la implementación, incluyendo pero sin limitarse a, Stephan
Richter, Philipp von Weitershausen, Guido van Rossum (también conocido
como  Python BDFL*), Tres Seaver, Phillip J Eby y
Martijn Faassen.

Inicialmente la ZCA definía componentes adicionales; `servicios` y
`vistas`, pero los desarrolladores se dieron cuenta que la utilidad
podía sustituir `servicio` y el multi-adaptador podía sustituir `view`.  Ahora la ZCA tiene un número muy pequeño de tipos de componentes
principales: utilidades, adaptadores, subscriptores y manejadores.  En realidad, subscriptores y manejadores son dos tipos especiales de
adaptadores.

Durante el ciclo de la versión Zope 3.2, Jim Fulton propuso una gran
simplificación de la ZCA [#proposal]_.  Con esta simplificación se creó
una nueva interfaz única (`IComponentRegistry`) para registrar
componentes locales y globales.

.. [#proposal] http://wiki.zope.org/zope3/LocalComponentManagementSimplification

El paquete ``zope.component`` tenía una larga lista de dependencias,
muchas de las cuales no eran necesarias para una aplicación no Zope 3.  Durante la PyCon 2007, Jim Fulton añadió la característica
``extras_require`` de setuptools para permitir la separación de la
funcionalidad básica de la ZCA de las características adicionales [#extras]_.

.. [#extras] http://peak.telecommunity.com/DevCenter/setuptools#declaring-dependencies

Hoy el proyecto de la ZCA es un proyecto independiente con su propio
ciclo de versiones y su repositorio Subversion.  Sin embargo, los problemas y los errores aún se controlan como parte del proyecto
Zope 3 [#bugs]_, y la lista principal zope-dev se utiliza para los
debates de desarrollo [#discussions]_.  Allí también esta otra lista general de usuario para Zope 3 (`zope3-users`) la cual puede ser usada para cualquier consulta acerca del ZCA [#z3users]_.

.. [#bugs] https://bugs.launchpad.net/zope3
.. [#discussions] http://mail.zope.org/mailman/listinfo/zope-dev
.. [#z3users] http://mail.zope.org/mailman/listinfo/zope3-users

Instalación
~~~~~~~~~~~

El paquete ``zope.component``, junto con el paquete ``zope.interface``
son el núcleo de la arquitectura de componentes Zope.  Ofrecen
facilidades para definir, registrar y buscar componentes.  El paquete
``zope.component`` y sus dependencias están disponibles en formato
de Paquete Egg Python desde el Índice de Paquetes Python (PyPI)  [#pypi]_.

.. [#pypi] Repositorio de paquetes Python: http://pypi.python.org/pypi

Puedes instalar ``zope.component`` y sus dependencias utilizando
`easy_install` [#easyinstall]_ : ::

  $ easy_install zope.component

.. [#easyinstall] http://peak.telecommunity.com/DevCenter/EasyInstall

Este comando descargará ``zope.component`` y sus dependencias desde
PyPI y los instalará en tu ruta Python.

Alternativamente, puedes descargar ``zope.component`` y sus
dependencias desde PyPI y luego instalarlos.  Instala los paquetes en
el siguiente orden.  En Windows, puede que necesitas los paquetes
binarios de ``zope.interface`` y ``zope.proxy``.

  1. ``zope.interface``
  2. ``zope.proxy``
  3. ``zope.deferredimport``
  4. ``zope.event``
  5. ``zope.deprecation``
  6. ``zope.component``

Para instalar estos paquetes, después de haberlos descargados, puedes
utilizar el comando ``easy_install`` con los paquetes eggs como argumento.  (También puedes darle todos estos paquetes eggs como argumento en la misma
linea.): ::

  $ easy_install /ruta/a/zope.interface-3.4.x.tar.gz
  $ easy_install /ruta/a/zope.proxy-3.4.x.tar.gz
  ...

Usted también puede instalar esos paquetes después extrayéndolos cada uno separadamente.  Por ejemplo: ::

  $ tar zxvf /ruta/a/zope.interface-3.4.x.tar.gz
  $ cd zope.interface-3.4.x
  $ python setup.py build
  $ python setup.py install

Esos métodos instalarán el ZCA en el `Python de su sistema`, en el directorio ``site-packages``, el cual puede causar problemas.  En un correo enviado a la lista de Zope 3, Jim Fulton recomendaba en ves de usar el Python del sistema [#systempython]_.  ``virtualenv`` y/o ``zc.buildout`` son herramientas que instalan la
ZCA en un entorno de trabajo aislado. Esto es una buena práctica
para experimentar con código y el estar familiarizado con estas
herramientas será beneficioso para desarrollar e implantar
aplicaciones.

.. [#systempython] http://article.gmane.org/gmane.comp.web.zope.zope3/21045


Experimentando con código
~~~~~~~~~~~~~~~~~~~~~~~~~

Hay dos buenos paquetes en Python para definir entornos de trabajos aislados para desarrollos de aplicaciones Python.  El ``virtualenv``
creado por Ian Biking y el ``zc.buildout`` creado por Jim Fulton son estos dos paquetes.  Usted puede también usar esos paquetes juntos.  Usando esos paquetes usted puede instalar ``zope.component`` y otras dependencias dentro de un entorno de trabajo aislado.  Es es una buena práctica para experimentar con cualquier código Python, y familiarizarse con
esas herramientas será beneficioso con el desarrollo y implementaciones de aplicaciones.

Usted puede instalar ``virtualenv`` usando ``easy_install``: ::

  $ easy_install virtualenv

Ahora crea un nuevo entorno así: ::

  $ virtualenv miev

Esto creará un nuevo entorno virtual en el directorio ``miev``.
Ahora, desde dentro del directorio ``miev``, puedes instalar
``zope.component`` y sus dependencias utilizando el comando ``easy_install``
que hay dentro del directorio ``miev/bin``: ::

  $ cd miev
  $ ./bin/easy_install zope.component

Ahora puedes importar ``zope.interface`` y ``zope.component`` desde
el nuevo intérprete ``python`` dentro del directorio ``miev/bin``: ::

  $ ./bin/python

Este comando ejecutará un intérprete de Python que puedes usar
para ejecutar el código de este libro.

Utilizando ``zc.buildout`` con la receta ``zc.recipe.egg`` se
puede crear un intérprete de Python con los paquetes eggs Python especificados.  Primero instala ``zc.buildout`` usando el comando ``easy_install``.  (Puedes hacerlo también dentro de un entorno virtual).  Para crear un nuevo buildout para experimentar con paquetes Python, primero crea un
directorio e inicialízalo  usando el comando ``buildout init``: ::

  $ mkdir mibuildout
  $ cd mibuildout
  $ buildout init

Ahora el nuevo directorio ``mibuildout`` es un proyecto buildout.  El archivo
de configuración predeterminado de buildout es `buildout.cfg` .  Después
de la inicialización, tendrá el siguiente contenido: ::

  [buildout]
  parts =

Puedes cambiarlo a: ::

  [buildout]
  parts = py

  [py]
  recipe = zc.recipe.egg
  interpreter = python
  eggs = zope.component

Ahora ejecuta el comando ``buildout`` disponible dentro del directorio
``mibuildout/bin`` sin ningún argumento.  Esto creará un nuevo intérprete
Python dentro del directorio ``mibuildout/bin``: ::

  $ ./bin/buildout
  $ ./bin/python

Este comando ejecutará un intérprete de Python que puedes usar
para ejecutar el código de este libro.


Un ejemplo
----------


Introducción
~~~~~~~~~~~~

Considere una aplicación de negocios para registrar huéspedes que quedan en un hotel.  Python puede implementar esto en un numero de formas.  Empezaremos con un mirada breve a un enfoque procedural, y
después cambiaremos a un enfoque orientado a objetos básico.  Mientras
examinamos el enfoque orientado a objetos, veremos como podemos
beneficiarnos de los patrones de diseño clásicos, `adapter` e
`interface`.  Esto nos llevará al mundo de la Arquitectura de Componentes
de Zope.


Enfoque procedural
~~~~~~~~~~~~~~~~~~

En una aplicación de gestión de negocios, el almacenamiento de los datos es muy
importante y critico.  Por simplicidad, este ejemplo utilizará un diccionario
Python como almacenamiento.  Nosotros generaremos identificadores únicos para el diccionario, los valores asociados
serán diccionario de detalles acerca de registro: ::

  >>> huespedes_db = {} #clave: identificador único, valor: detalles en un diccionario

En una implementación mínima requiere una función el cual nosotros pasamos detalles
del registro, y también necesitas una función auxiliar para obtener el 
identificador único para la clave del diccionario de almacenamiento de datos.

Esta función auxiliar, para obtener el próximo identificador se puede
implementar así: ::

  >>> def obtener_proximo_id():
  ...     claves_db = huespedes_db.keys()
  ...     if claves_db == []:
  ...         proximo_id = 1
  ...     else:
  ...         proximo_id = max(claves_db) + 1
  ...     return proximo_id

Como puede ver, la implementación de la función `obtener_proximo_id` es muy
simple. Bueno, no es la forma ideal, pero es suficiente para explicar
conceptos.  La función obtiene todas una lista de claves del
almacenamiento y comprueba si una lista está vacía o no. Si la lista está
vacía, este es nuestro primer registro, entonces devuelve `1`. Si la lista no está vacía, agrega `1` al valor máximo en la 
lista y lo devuelve.

Ahora usaremos la función anterior para crear entradas en el 
diccionario huespedes_db: ::

  >>> def registrar_huesped(nombre, lugar):
  ...     huesped_id = obtener_proximo_id()
  ...     huespedes_db[huesped_id] = {
  ...     'nombre': nombre,
  ...     'lugar': lugar
  ...     }

Los requerimientos de una aplicación de administración de huéspedes de un hotel que requiere
considerar los siguientes datos adicionales:

  - números telefónicos
  - opciones de habitación
  - formas de pago
  - ...

Y programar la administración de la data de:

  - cancelar una reservación
  - actualizar una reservación
  - pago para una habitación
  - la persistencia de la data
  - incidentes de seguridad de la data
  - ...

Si continuáramos con el ejemplo de procedural, crearíamos muchos
funciones, pasando datos de ida y vuelta entre ellos.  Como los requerimientos anterior son cambiantes y fueron agregados, la programación viene a ser dura para el mantenimiento y los errores viene a ser difícil de buscar y corregir.

Nosotros finalizaremos nuestra discusión del enfoque procedural aquí. El siguiente enfoque será 
mucho más fácil para proveer persistencia de data, diseño flexible y pruebas 
de códigos usando objetos.


Enfoque orientado a objetos
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. ??? podría este párrafo hablar acerca de "creando  un objeto para
 manipular el registro" o "creando una clase para manipular el registro"?

Nuestra discusión del diseño orientado a objeto se introducirá en la `class` la cual
sirve para encapsular la data, y la programación para administrarla.

Nuestra clase principal será `RegistradorHuesped`. RegistradorHuesped, o otras clases se 
delegara, sabrán como administrar la data para el hotel.  Nosotros 
crearemos `instancias` de RegistradorHuesped para aplicar este conocimiento al 
negocio de llevar un hotel.

La experiencia ha demostrado que consolidando la programación y los requerimientos de data vía
objetos, nosotros culminaremos con un diseño el cual sea fácil de entender,
probar, y cambiar.

En cualquier caso, aquí tenemos los detalles de 
implementación de una clase `RegistradorHuesped`: ::

  >>> class RegistradorHuesped(object):
  ...
  ...     def registrar_cuarto(self, nombre, lugar):
  ...         huesped_id = obtener_proximo_id()
  ...         huespedes_db[huesped_id] = {
  ...         'nombre': nombre,
  ...         'lugar': lugar
  ...         }

En esta implementación, el objeto `registradorhuesped` (una instancia de
la clase `RegistradorHuesped`) se encarga del registro.  Así es como puedes 
usar la implementación actual: ::

  >>> registradorhuesped = RegistradorHuesped()
  >>> registradorhuesped.registrar_cuarto("Pedro", "Pérez")

Cualquier cambios de requisitos son inevitables en un proyecto real.  Considera
este caso, después de algún tiempo, un nuevo requisito se presenta:
los huéspedes también deben dar el número de teléfono, necesitarás cambiar el código.

Puedes cumplir este requisito añadiendo un argumento al método
`registrar_cuarto` el cual sera agregado al diccionario de valores: ::

  >>> class RegistradorHuesped(object):
  ...
  ...     def registrar_cuarto(self, nombre, lugar, telefono):
  ...         huesped_id = obtener_proximo_id()
  ...         huespedes_db[huesped_id] = {
  ...         'nombre': nombre,
  ...         'lugar': lugar,
  ...         'telefono': telefono
  ...         }

Además de migrar los datos al nuevo esquema, ahora tienes que cambiar
la forma de usar `RegistradorHuesped` en todas las llamadas.  Si puedes abstraer los detalles de un huesped en un objeto y usarlo para el
registro, los cambios en el código se pueden minimizar.
Ahora puede hacer cambios a los detalles del objeto huesped y las 
llamadas a RegistradorHuesped no necesitan cambiase.

La nueva implementación con el objeto huesped quedaría
así: ::

  >>> class RegistradorHuesped(object):
  ...
  ...     def registrar_cuarto(self, huesped):
  ...         huesped_id = obtener_proximo_id()
  ...         huespedes_db[huesped_id] = {
  ...         'nombre': huesped.nombre,
  ...         'lugar': huesped.lugar,
  ...         'telefono': huesped.telefono
  ...         }

Aun tendremos que cambiar el código a responder a los cambios de requerimientos.
El cambio de código con nuevos requisitos es inevitable, tu objetivo global es
poder minimizar esos cambios y hacerlo mantenibles.

.. note::

  Cuando programas, es importante sentirse con el coraje para hacer cambios sin
  miedo a dañar la aplicación.  La forma para obtener una retroalimentación inmediata
  es requerido vía pruebas automatizadas.  Con la escritura de buenas
  pruebas automatizadas (y un buen control de versiones) usted puede hacer grandes o
  pequeños cambios con impunidad.  Para más información sobre esta 
  filosofía de programación puedes leer el libro llamado `Extreme Programming Explained` 
  de Kent Beck.

Para introducir el objeto huesped, usted guarda algo ingresando.  Más que eso, la abstracción del objeto huesped ha hecho a su sistema
mucho más simple y fácil de entender.  Cuanto mejor se entienda mejor
se puede reestructurar y por tanto mejor se mantiene mejor el código.


El patrón adaptador
~~~~~~~~~~~~~~~~~~~

Como se ha dicho antes, en una aplicación real, el objeto registradorhuesped
puede tener funcionalidades de cancelación y/o actualización.  En el actual diseño, nosotros necesitaremos pasar el objeto huesped a registradorhuesped cada vez que llamamos métodos como, `cancelar_registro` y `actualizar_registro`.

..
    Puedes solucionar este problema guardando el 
    objeto huesped esta definido como un atributo: ::

Podemos evitar este requisito si nosotros pasamos el objeto huesped a
RegistradorHuesped.__init__(), haciéndolo como un atributo de la instancia. ::

  >>> class RegistradorHuespedNG(object):
  ...
  ...     def __init__(self, huesped):
  ...         self.huesped = huesped
  ...
  ...     def registrar_cuarto(self):
  ...         huesped= self.huesped
  ...         huesped_id = obtener_proximo_id()
  ...         huespedes_db[huesped_id] = {
  ...         'nombre': huesped.nombre,
  ...         'lugar': huesped.lugar,
  ...         'telefono': huesped.telefono
  ...         }

.. incluir este bit al frente de la sección `Adapters` cuando yo tengo 
    la cita equivalente desde el libro Patterns para iniciar la  
    sección `Interfaces`

    La solución a la que has llegado es un patrón de diseño común llamado, 
    `Adaptador`.  El libro `Gang of Four` [#patternbook]_ da esto como la 
    *intención* del Adaptador: ::

     "Convertir la interfaz de una clase en otra interfaz clientes 
     esperan.  El Adaptador permite a las clases trabajen juntos que no podría de otra manera 
     debido a interfaces incompatibles."

La solución que hemos alcanzado es un patrón bien conocido, el *adaptador*.
En general, un adaptador *contiene* un *adaptado*: ::

  >>> class Adaptador(object):
  ...
  ...     def __init__(self, adaptado):
  ...         self.adaptado = adaptado

Este patrón será útil en el tratamiento de los detalles de implementación
que dependerá de consideraciones tales como:

- Requerimientos del cliente muy cambiantes.
- Requerimientos de almacenamiento (ZODB, RDBM, XML ...)
- Diferentes tipos de formatos de salida para datos de texto (HTML, PDF, texto plano...) 
- Soporte a renderizar múltiples formatos de marcados (ReST, Markdown, Textile...) 

ZCA usas adaptadores y a *registro de componentes* para proveer la capacidad
para cambiar los detalles de implementación del código vía *configuración*.

Como veremos en la sección de adaptadores ZCA, la habilidad de 
configurar los detalles de implementación proveída una capacidad útil:

- la habilidad para seleccionar entre implementaciones
- la habilidad para agregar implementaciones como se necesite
- aumento de la reutilización de tanto heredados como código ZCA

Estas capacidades llevan al código que es flexible, escalable y
reutilizable. Hay un costo sin embargo, mantener el registro de componentes 
añade un nivel de complejidad a la aplicación.  Si una aplicación 
nunca requiera estas características, ZCA es innecesario.

Ahora estamos listos para comenzar nuestro estudio de la Arquitectura de componente 
Zope, comenzando con interfaces.


Interfaces
----------

Introducción
~~~~~~~~~~~~

El archivo README.txt [#readmes]_ en la ruta/al/zope/interface define 
las interfaces de la siguiente forma: ::

    Las Interfaces son objetos que especifica (documento) el comportamiento externo
    de los objetos que "provee" entonces.  Una interfaz especifica el comportamiento
    a través de:

    - Documentación informal en una doc string

    - Definiciones de Attribute

    - Invariantes, los cuales son condiciones que deben tener los objetos que 
      provee la interfaz

El libro clásico de ingeniería de software `Design Patterns` [#patternbook]_
por el `Gang of Four` recomienda que usted "Programe a una interfaz,
no a una implementación".  Definiendo una interfaz formal es de mucha ayuda en
entender un sistema.  Mas que todo, las interfaces unen a usted con todos los 
beneficios de la ZCA.

.. [#readmes] El árbol del código Zope tiene archivos README.txt muy completo el cual
    ofrece una hermosa documentación.
.. [#patternbook] http://en.wikipedia.org/wiki/Design_Patterns

Una interfaz especifica las características de un objeto, eso es
comportamiento, sus capacidades.  La interfaz describe *que* un
objeto puede hacer, aprender *como*, usted debe observar en la implementación.

Las metáforas comúnmente utilizados para interfaces son `contract` o `blueprint`,
los términos legales y de arquitectura para un conjunto de especificaciones.

En algunos lenguajes modernos de programación: Java, C#, VB.NET etc, las interfaces
son un aspecto explicito del lenguaje.  Debido a que Python carece
las interfaces, ZCA implementa entonces como una meta-clase para heredar.

Aquí esta un ejemplo clásico al estilo *hola mundo*: ::

  >>> class Anfitrion(object):
  ...
  ...     def buenosdias(self, nombre):
  ...         """Le dice buenos dias al huesped"""
  ...
  ...         return "¡Buenos días, %s!" % nombre

En la clase anterior, usted define un método `buenosdias`.  Si usted llama
al método `buenosdias` desde un objeto creado usando esta clase, esa
devolverá `¡Buenos días, ...!`: ::

  >>> anfitrion = Anfitrion()
  >>> anfitrion.buenosdias('Pedro')
  '¡Buenos días, Pedro!'

Aquí ``anfitrion`` es el actual objeto que su código utiliza.  Si usted quiere 
examinar los detalles de la implementación usted necesita acceder a la clase ``Anfitrion``,
así sea  vía el código fuente o una herramienta de documentación API [#api]_.

.. [#api] http://en.wikipedia.org/wiki/Application_programming_interface

Ahora iniciamos el uso de las interfaces ZCA.  Para la clase dada 
arriba usted puede especificar interfaz de la siguiente forma: ::

  >>> from zope.interface import Interface

  >>> class IAnfitrion(Interface):
  ...
  ...     def buenosdias(huesped):
  ...         """Le dice buenos días al huesped"""

Usted puede ver, la interfaz inherente de ``zope.interface.Interface``.
Este uso (o ¿abuso?) de la sentencias ``class`` Python es como la ZCA defines un
interfaz.  El prefijo ``I`` para el nombre de la interfaz es una convensión 
muy útil.


Declarando interfaces
~~~~~~~~~~~~~~~~~~~~~

Ya has visto como declarar una interfaz usando ``zope.interface`` en
la sección anterior.  En esta sección se explicarán los conceptos en
detalle.

Considera esta interfaz de ejemplo: ::

  >>> from zope.interface import Interface
  >>> from zope.interface import Attribute

  >>> class IAnfitrion(Interface):
  ...     """Un objeto anfitrion"""
  ...
  ...     nombre = Attribute("""Nombre del anfitrion""")
  ...
  ...     def buenosdias(huesped):
  ...         """Le dice buenos días al huesped"""

La interfaz, ``IAnfitrion`` tiene dos atributos, ``nombre`` y
``buenosdias``.  Recuerda que, al menos en Python, los métodos
también son atributos de clases.  El atributo ``nombre`` se define utilizando la clase ``zope.interface.Attribute``.  Cuando añades el atributo ``nombre`` a la interfaz ``IAnfitrion``, no especificas ningún valor inicial.
El propósito de definir el atributo ``nombre`` aquí es meramente para indicar que cualquier implementación de esta interfaz tendrá una atributo llamado ``nombre``.  En este caso, ¡ni siquiera dices el tipo que el atributo tiene que tener!.  Puedes pasar una cadena de documentación como primer argumento a
``Attribute``.

El otro atributo, ``buenosdias`` es un método definido usando
una definición de función.  Note que no hace falta ``self`` en las interfaces, porque ``self`` es un detalle de implementación de la clase.  Por ejemplo, un 
módulo puede implementar esta interfaz.  Si un módulo implementa esta 
interfaz, habrá un atributo ``nombre`` y una función ``buenosdias`` 
definida.  Y la función ``buenosdias`` aceptará un argumento.

Ahora verás como conectar `interfaz-clase-objeto`.  Así objeto es la cosa viva y real, los objetos son instancias de clases.  Y 
la interfaz es la definición real del objeto, por tanto las clases son sólo 
los detalles de implementación.  Es por esto por lo que debes programar contra una 
interfaz y no contra una implementación.

Ahora debe familiarizarse con dos términos más para entender otros conceptos.  El primero es `proveer` y el otro es `implementar`.
Los objetos proveen interfaces y las clases implementan interfaces.  En otras palabras, objetos proveen las interfaces que sus clases implementan.  En el ejemplo anterior ``anfitrion`` (objeto) provee ``IAnfitrion`` (interfaz) y ``Anfitrion`` (clase) implementa ``IAnfitrion`` (interfaz).  Un objeto puede proveer más de una interfaz y también una clase puede implementar más de una interfaz.  Los objetos también pueden proveer interfaces directamente, además
de lo que sus clases implementen.

.. note::

  Las clases son los detalles de implementación de los objetos.  En Python,
  las clases son objetos llamables, así que por qué otros objetos llamables no pueden 
  implementar una interfaz.  Sí, es posible.  Para cualquier `objeto 
  llamable` puedes declarar que produce objetos que proveen algunas 
  interfaces diciendo que el `objeto llamable` implementa 
  las interfaces.  Generalmente los `objetos llamables` son llamados 
  `fábricas`.  Como las funciones son objetos llamables, una función puede ser 
  la `implementadora` de una interfaz.


Implementando interfaces
~~~~~~~~~~~~~~~~~~~~~~~~

Para declarar que una clase implementa una interfaz en particular,
utiliza la función ``zope.interface.implements`` dentro de la sentencia ``class``.

Considera este ejemplo, aquí ``Anfitrion`` implementa ``IAnfitrion``: ::

  >>> from zope.interface import implements

  >>> class Anfitrion(object):
  ...
  ...     implements(IAnfitrion)
  ...
  ...     nombre = u''
  ...
  ...     def buenosdias(self, huesped):
  ...         """Le dice buenos días al huesped"""
  ...
  ...         return "¡Buenos días, %s!" % huesped

.. note::

    Si te preguntas como trabaja la función ``implements``, consulta 
    el mensaje del blog de James Henstridge 
    (http://blogs.gnome.org/jamesh/2005/09/08/python-class-advisors/) .
    En la sección del adaptador, verás una función ``adapts``, 
    que funciona de forma similar.

Como ``Anfitrion`` implementa ``IAnfitrion``, las instancias de
``Anfitrion`` proveen ``IAnfitrion``.  Hay unos cuantos métodos de utilidad que introspecciona las declaraciones.  La declaración se puede escribir fuera de la clase también.  Si 
no escribes ``interface.implements(IAnfitrion)`` en el ejemplo anterior,
entonces después de la sentencia ``class``, puedes escribir algo como: ::

  >>> from zope.interface import classImplements
  >>> classImplements(Anfitrion, IAnfitrion)


Ejemplo revisado
~~~~~~~~~~~~~~~~

Ahora volvemos a la aplicación de ejemplo.  Ahora veremos como
definir la interfaz del objeto registrador ::

  >>> from zope.interface import Interface

  >>> class IRegistrador(Interface):
  ...     """Un registrador registrará los detalles de un objeto"""
  ...
  ...     def registrar():
  ...         """Registrar detalles de un objeto"""
  ...

Aquí primero usted ha importado la clase ``Interface`` del módulo
``zope.interface``.  Si define una subclase de esta clase ``Interface``,
será una interfaz desde el punto de vista de la arquitectura de
componentes de Zope.  Una interfaz puede ser implementada, como ya
has visto, en una clase o cualquier otro objeto llamable.

La interfaz registradorhuesped definida aquí es ``IRegistrador``.  La cadena
de documentación de la interfaz da una idea del objeto.  Al definir un
método en la interfaz, has creado un contrato para el componente, en
el que dice que habrá un método con el mismo nombre disponible.  En
la definición del método en la interfaz, el primer argumento no debe
ser `self`, porque una interfaz nunca será instanciada ni sus métodos
serán llamados jamás.  En vez de eso, la sentencia ``class`` de la interfaz
meramente documenta qué métodos y atributos deben aparecer en
cualquier clase normal que diga que la implementa, y el parámetro
`self` es un detalle de implementación que no necesita ser
documentado.

Como sabes, una interfaz puede también especificar atributos
normales: ::

  >>> from zope.interface import Interface
  >>> from zope.interface import Attribute

  >>> class IHuesped(Interface):
  ...
  ...     nombre = Attribute("Nombre del huesped")
  ...     lugar = Attribute("Lugar del huesped")

En esta interfaz, el objeto huesped tiene dos atributos que se
especifican con documentación.  Una interfaz también puede especificar
atributos y métodos juntos.  Una interfaz puede ser implementada por
una clase, un módulo o cualquier otro objeto.  Por ejemplo una
función puede crear dinámicamente el componente y devolverlo, en
este caso la función es una implementadora de la interfaz.

Ahora ya sabes lo que es una interfaz y como definirla y usarla.  En
el próximo capítulo podrás ver como se usa una interfaz para definir
un componente adaptador.


Interfaces de marcado
~~~~~~~~~~~~~~~~~~~~~

Una interfaz se puede usar para declarar que un objeto en particular
pertenece a un tipo especial.  Un interfaz sin ningún atributo o método
se llama `interfaz de marcado`.

Aquí tenemos una `interfaz de marcado`::

  >>> from zope.interface import Interface

  >>> class IHuespedEspecial(Interface):
  ...     """Un huesped especial"""


Esta interfaz se puede usar para declarar que un objeto es un huesped
especial.


Invariantes
~~~~~~~~~~~

A veces le piden usar alguna regla para su componente que implica
a uno o más atributos normales.  A este tipo de reglas se les llama
`invariantes`.  Puedes usar ``zope.interface.invariant`` para
establecer `invariantes` para tus objetos en sus interfaces.

Considera un ejemplo sencillo, hay un objeto `persona`.  Una persona
tiene los atributos `nombre`, `email` y `telefono`.  ¿Cómo implementas
una regla de validación que diga que o bien el email o bien el
teléfono tienen que existir, pero no necesariamente los dos?

Lo primero es hacer un objeto llamable, bien una simple función o
bien una instancia llamable de una clase como esto: ::

  >>> def invariante_contactos(obj):
  ...
  ...     if not (obj.email or obj.telefono):
  ...         raise Exception(
  ...             "Al menos una información de contacto es obligatoria")

Ahora defines la interfaz del objeto `persona` de esta manera.  Utiliza la función ``zope.interface.invariant`` para establecer la
invariante: ::

  >>> from zope.interface import Interface
  >>> from zope.interface import Attribute
  >>> from zope.interface import invariant

  >>> class IPersona(Interface):
  ...
  ...     nombre = Attribute("Nombre")
  ...     email = Attribute("Direccion de email")
  ...     telefono = Attribute("Numero de telefono")
  ...
  ...     invariant(invariante_contactos)

Ahora usas el método `validateInvariants` de la interfaz para
validar: ::

  >>> from zope.interface import implements

  >>> class Persona(object):
  ...     implements(IPersona)
  ...
  ...     nombre = None
  ...     email = None
  ...     telefono = None

  >>> pedro = Persona()
  >>> pedro.email = u"pedro@algun.sitio.com"
  >>> IPersona.validateInvariants(pedro)
  >>> maria = Persona()
  >>> IPersona.validateInvariants(maria)
  Traceback (most recent call last):
  ...
  Exception: Al menos una información de contacto es obligatoria

Como puede ver el objeto `pedro` validó sin lanzar ninguna
excepción. Pero el objeto `maria` no validó la restricción de
la invariante, por lo que se lanzó la excepción.


Adaptadores
-----------


Implementación
~~~~~~~~~~~~~~

Esta sección describirá los adaptadores en detalles.  La arquitectura 
de componentes Zope, como usted noto, ayuda a especificar eficientemente uso de los objetos Python.
Los componentes Adaptador son uno de los componentes básicos usado por la 
arquitectura de componentes para el uso eficiente de objetos Python.  Los componentes 
Adaptador son objetos Python, pero con interfaz bien definida.

Para declarar una clase es un adaptador usa la función `adapts` definida en
el paquete ``zope.component``.  Aquí un nuevo adaptador `RegistradorHuespedNG` con la declaración explicita de la interfaz: ::

  >>> from zope.interface import implements
  >>> from zope.component import adapts

  >>> class RegistradorHuespedNG(object):
  ...
  ...     implements(IRegistrador)
  ...     adapts(IHuesped)
  ...
  ...     def __init__(self, huesped):
  ...         self.huesped = huesped
  ...
  ...     def registrar(self):
  ...         huesped= self.huesped
  ...         huesped_id = obtener_proximo_id()
  ...         huespedes_db[huesped_id] = {
  ...         'nombre': huesped.nombre,
  ...         'lugar': huesped.lugar,
  ...         'telefono': huesped.telefono
  ...         }


Lo que usted definió aquí es un `adaptador` para `IRegistrador`, el cual adapta
el objeto `IHuesped`.  La interfaz `IRegistrador` es implementada por la clase
`RegistradorHuespedNG`.  Entonces, una instancia de esta clase proveerá la 
interfaz `IRegistrador`.

::

  >>> class Huesped(object):
  ...
  ...     implements(IHuesped)
  ...
  ...     def __init__(self, nombre, lugar):
  ...         self.nombre = nombre
  ...         self.lugar = lugar

  >>> pedro = Huesped("Pedro", "España")
  >>> pedro_registradorhuesped = RegistradorHuespedNG(pedro)

  >>> IRegistrador.providedBy(pedro_registradorhuesped)
  True

El `RegistradorHuespedNG` es solo un adaptador creado, usted puede también crear otros adaptadores los cuales manipulen un registro diferente de huesped.


Registro
~~~~~~~~

Para usar este componente adaptador, usted tiene que registrar este en un 
registro de componente también conocido como site manager.  Un site manager
normalmente reside en un sitio.  Un sitio y site manager serán muy 
importante cuando desarrolla una aplicación Zope 3.  Por ahora sólo es 
necesario preocuparse acerca de global site y global site manager (o el 
registro de componentes).  Un global site manager estará en memoria, pero un 
local site manager es persistente.

Para registrar su componente, primero obtenga el global site manager: ::

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()
  >>> gsm.registerAdapter(RegistradorHuespedNG,
  ...                     (IHuesped,), IRegistrador, 'ng')

Para obtener el global site manager, usted tiene que llamar a 
la función ``getGlobalSiteManager`` disponible en el paquete 
``zope.component``.  En hecho, el global site manager esta disponible como un 
atributo (``globalSiteManager``) del paquete ``zope.component``.  Entonces,
usted puede directamente usar el atributo ``zope.component.globalSiteManager``.
Para registrar el adaptador en el componente, como usted puede ver en ejemplo anterior, use 
el método ``registerAdapter`` del registro de componente.  El primer argumento 
debe ser su clase adaptador / fábrica.  El segundo argumento es una tupla 
de los objetos `adaptados`, e.j., el objeto el cual usted esta adaptando.  En este 
ejemplo usted esta adaptando solamente el objeto `IHuesped`.  El tercer argumento es 
la interfaz implementada por el componente adaptador.  El cuarto 
argumento es opcional, que es el nombre de un adaptador particular.
Desde que usted dio un nombre para este adaptador , este es un `named adapter`.  Si el 
nombre no es dado, esa sera por defecto un cadena vacía ('').

En el registro anterior, usted ha dado la interfaz adaptada y la interfaz 
para ser proveída por el adaptador.  Desde usted ya ha dado 
esos detalles en la implementación adaptador, eso no es requerido para especificarlo 
otra vez.  En hecho, usted podría tener hecho el registro de la siguiente manera: ::

  >>> gsm.registerAdapter(RegistradorHuespedNG, name='ng')

Hay algunas viejas API para hacer registros, el usted debería avoid.
Las viejas funciones de la API inician con el prefijo `provide`, ej: ``provideAdapter``,
``provideUtility`` etc.  Mientras desarrollas una aplicación Zope 3 usted puede 
usar Zope configuration markup language (ZCML) para el registro de los 
componentes.  En Zope 3, los componentes local (persistent components) puede 
ser registrados desde la Zope Management Interface (ZMI) o usted puede hacerlo 
también de forma programada.

Usted registro `RegistradorHuespedNG` con un nombre `ng`.  Similarmente usted puede 
registrar otros adaptadores con diferentes nombres.  Si un componente es
registrado sin nombre, ese sera por defecto una cadena vacía.

.. note::

  Los local components son componentes persistentes pero los global components están 
  en memoria.  Los global components serán registrados basados en la 
  configuración de la aplicación.  Los local components son tomando a la memoria 
  desde la base de datos mientras inicia la aplicación.


Patrón de consulta
~~~~~~~~~~~~~~~~~~

Recuperar componentes registrados de registro de componentes se logra 
a través de dos funciones disponibles en paquete ``zope.component``.  Uno de 
ellos es ``getAdapter`` y el otro es ``queryAdapter``.  Ambos 
funciones acepta los mismo argumentos.  El ``getAdapter`` levantará 
un ``ComponentLookupError`` si la búsqueda de componente falló por otra parte 
``queryAdapter`` devolverá `None`.

Usted puede importar los métodos de la siguiente forma: ::

  >>> from zope.component import getAdapter
  >>> from zope.component import queryAdapter

En la sección previa usted tiene registrado un componente para el objeto 
huesped (adaptado) el cual provee la interfaz `IRegistrador` con el nombre 
como 'ng'.  En la primera sección de este capitulo, usted tiene creado un objeto 
huesped nombrado `pedro` .

Esto es como usted puede recuperar el componente el cual adaptas la interfaz del 
objeto `pedro` (`IHuesped`) y provee la interfaz `IRegistrador` también con el 
nombre 'ng'.  Aquí ambos ``getAdapter`` y ``queryAdapter`` trabaja
similarmente: ::

  >>> getAdapter(pedro, IRegistrador, 'ng') #doctest: +ELLIPSIS
  <RegistradorHuespedNG object at ...>
  >>> queryAdapter(pedro, IRegistrador, 'ng') #doctest: +ELLIPSIS
  <RegistradorHuespedNG object at ...>

Como usted puede ver, el primer argumento debería ser adaptado entonces, la 
interfaz la cual debería ser proveída por componente y por ultimo el nombre de 
componente adaptador.

Si usted trata para buscar el componente con un nombre no usado por 
el registro pero por lo mismo adaptado y la interfaz, la búsqueda fallará.
Aquí es como los dos métodos trabaja en cuyo caso: ::

  >>> getAdapter(pedro, IRegistrador, 'not-exists') #doctest: +ELLIPSIS
  Traceback (most recent call last):
  ...
  ComponentLookupError: ...
  >>> reg = queryAdapter(pedro,
  ...           IRegistrador, 'not-exists') #doctest: +ELLIPSIS
  >>> reg is None
  True

Usted puede ver anteriormente, el ``getAdapter`` lanzo una excepción ``ComponentLookupError``, 
pero ``queryAdapter`` devuelve `None` cuando la búsqueda fallo.

El tercer argumento, el nombre del registro, es opcional.  Si el 
tercer argumento no es dado ese sera por defecto una cadena vacía ('').
Puesto que no hay componente registrado con una cadena vacía, 
``getAdapter`` lanzará una excepción `` ComponentLookupError``.  Similarmente
``queryAdapter`` devolverá `None`, vea usted mismo como eso trabaja: ::

  >>> getAdapter(pedro, IRegistrador) #doctest: +ELLIPSIS
  Traceback (most recent call last):
  ...
  ComponentLookupError: ...
  >>> reg = queryAdapter(pedro, IRegistrador) #doctest: +ELLIPSIS
  >>> reg is None
  True

En esta sección usted ha aprendido a como registrar un simple adaptador y 
como recuperarlo desde un registro de componente.  Esos tipos de adaptadores son 
llamados single adapter, por que ese adaptas solamente un adaptado.  Si un 
adaptador adapta mas que un adaptado, entonces ese es llamado multi
adaptador.


Recuperar un adaptador usando una interfaz
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Los adaptadores puede ser directamente recuperados usando interfaces, pero eso solamente 
trabajara para adaptadores single sin nombre.  El primer argumento es el adaptado 
y el segundo argumento es un argumento de palabra clave.  Si la búsqueda del adaptador 
falla, el segundo argumento sera devuelto, por ejemplo: ::

  >>> IRegistrador(pedro, alternate='default-output')
  'default-output'

El nombre de la palabra clave puede ser omitido: ::

  >>> IRegistrador(pedro, 'default-output')
  'default-output'

Si el segundo argumento no es dado, ese lanzará una error de excepción `TypeError`: ::

  >>> IRegistrador(pedro) #doctest: +NORMALIZE_WHITESPACE +ELLIPSIS
  Traceback (most recent call last):
  ...
  TypeError: ('Could not adapt',
    <Huesped object at ...>,
    <InterfaceClass __builtin__.IRegistrador>)

Aquí `RegistradorHuespedNG` esta registrado sin nombre: ::

  >>> gsm.registerAdapter(RegistradorHuespedNG)

Ahora la búsqueda del adaptador debería ser exitosa: ::

  >>> IRegistrador(pedro, 'default-output') #doctest: +ELLIPSIS
  <RegistradorHuespedNG object at ...>

Para casos simples, usted podría usar la interfaz para obtener los componentes adaptador.


Patrón de Adaptador
~~~~~~~~~~~~~~~~~~~

El concepto adaptador en la Zope Component Architecture y los clásicos
`adapter pattern` como son descritos en el libro Design Patterns son muy 
similares.  Pero el intento del adaptador ZCA usado es mas amplio que el 
`adapter pattern` en si mismo.  El intento de `adapter pattern` es para 
convertir la interfaz de una clase dentro de otro interfaz de clientes 
esperar.  Esto permite a las clases trabajar juntos las cuales no podría de otra manera 
hacerlo porque las interfaces son incompatibles.  Pero la sección `motivation` 
del libro Design Patterns, Gang of Four dice: "Often the adapter is responsible
for functionality the adapted class doesn't provide" en Español dice "A menudo, el adaptador es responsable 
por la funcionalidad de la clase adaptada no sea proporciona".  El adaptador ZCA tiene 
mas focos en agregar funcionalidades que crear una nueva interfaz para 
un objeto que fue adaptado (adaptado).  El adaptador ZCA deja adaptar clases extendiendo 
funcionalidad agregando métodos.  (Podría ser interesante una nota 
que el `Adapter` fue conocido como `Feature` en estados tempranos del diseño 
de la ZCA. ) [#feature]_

.. [#feature] Hilo de discusión sobre el renombrar de `Feature` a `Adapter`:
   http://mail.zope.org/pipermail/zope3-dev/2001-December/000008.html

En párrafo anterior tiene una cita desde el libro Gang of Four, ese finaliza de la siguiente 
forma: " ...adapted class doesn't provide".  Pero en la próxima sentencia yo 
usado "objeto adaptado" en vez de "clase adaptada", por que el libro Gang of Four 
describes sobre dos variantes de adaptadores basado en implementaciones.
El primero es llamado `clase adaptador` y el otro es llamado 
`objeto adaptador`.  Una clase adaptador usa herencia múltiple para adaptar 
una interfaz a otra, y por otra parte un objeto adaptador confía 
en la composición del objeto.  El adaptador ZCA sigue el patrón objeto adaptador, 
el cual usa delegación como un mecanismo para la composición.  El segundo principio 
del diseño orientado a objeto del libro Gang of Four va de la siguiente manera: "Favor
object composition over class inheritance".  Para mas detalles acerca de 
este tema por favor, lea el libro Design Patterns.

La mayor atracción de los adaptadores ZCA  son las interfaz explicita para 
los componentes y el registro de componente.  Los componentes adaptador ZCA son 
registrado en el registro de componente y es observado por los objetos clientes usando 
la interfaz y el nombre cuando es requerido.


Utilidad
--------


Introducción
~~~~~~~~~~~~

Ahora ya conoce el concepto de interfaz, adaptador y registro de componente.
A veces podría ser útil para registrar un objeto el cual no esta 
adaptando ninguna cosa.  Conexión de base de datos, parsear XML, objeto que devuelven 
identificadores únicos etc. son ejemplos de esos tipos de objetos.  Esos tipos de 
componentes proveídos por la ZCA son llamados componentes ``utility``.

Las utilidades son solo objetos que provee una interfaz y que eso son 
observado por una interfaz y un nombre.  Este aprovecha crear un global 
registry para cuales instancias puede ser registradas y accedidas por 
diferente partes de su aplicación, sin necesidad de pasar las 
instancias alrededor como parámetros.

Usted no necesita registrar todos las instancias componente así.  Solamente 
registra componentes los cuales usted quiere hacer reemplazable.


Utilidad simple
~~~~~~~~~~~~~~~

Una utilidad puede ser registrada con un nombre o sin un nombre.  Una utilidad 
registrada con un nombre es llamada *named utility*, el cual usted vera en 
la próxima sección.  Antes de implementar la utilidad, como usualmente, define
esa interfaz.  Aquí una interfaz `saludador`: ::

  >>> from zope.interface import Interface
  >>> from zope.interface import implements

  >>> class ISaludador(Interface):
  ...
  ...     def saludar(nombre):
  ...         """Decir hola"""

Como un adaptador una utilidad podría tener mas que una implementación.  Aquí 
es una posible implementación la interfaz anterior: ::

  >>> class Saludador(object):
  ...
  ...     implements(ISaludador)
  ...
  ...     def saludar(self, nombre):
  ...         return "Hola" + nombre

La actual utilidad sera una instancia de esta clase.  Para usar esta 
utilidad, usted tiene que registrarlo, después usted puede consultarlo usando la API 
de ZCA.  Usted puede registrar una instancia de esta clase (`utility`) usando 
``registerUtility``: ::

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()

  >>> saludar = Saludador()
  >>> gsm.registerUtility(saludar, ISaludador)

En este ejemplo usted registro la utilidad como proveyendo la interfaz 
`ISaludador`.  Usted puede observar la interfaz bien sea con `queryUtility`
o `getUtility`: ::

  >>> from zope.component import queryUtility
  >>> from zope.component import getUtility

  >>> queryUtility(ISaludador).saludar('Pedro')
  'Hola Pedro'

  >>> getUtility(ISaludador).saludar('Pedro')
  'Hola Pedro'

Como usted puede ver, los adaptadores como clases normalmente, pero las utilidades son 
instancias normalmente de clases.  Solamente una vez usted creando la 
instancia de una clase utilidad, pero las instancias adaptador son creadas dinámicamente 
cada vez que se consulta para él.


Utilidad con nombre
~~~~~~~~~~~~~~~~~~~

Cuando usted registra un componente utilidad, como adaptador, usted puede usar un 
nombre.  Como se menciono en la sección previa, una utilidad registrada con 
un nombre particular que es llamado named utility.

Esto es como usted puede registrar la utilidad `saludador` con un nombre: ::

  >>> saludar = Saludador()
  >>> gsm.registerUtility(saludar, ISaludador, 'new')

En este ejemplo usted ha registrado la utilidad con un nombre como proveyendo 
la interfaz `ISaludador`.  Usted puede observar la interfaz bien sea con 
`queryUtility` o `getUtility`: ::

  >>> from zope.component import queryUtility
  >>> from zope.component import getUtility

  >>> queryUtility(ISaludador, 'new').saludar('Juan')
  'Hola Juan'

  >>> getUtility(ISaludador, 'new').saludar('Juan')
  'Hola Juan'

Como usted puede ver aquí, mientras consultas usted tiene usar el `name` como 
el segundo argumento.

Llamando la función `getUtility` sin un nombre (segundo argumento) es
equivalente para llamar con una cadena vacía como el nombre.  Por que, el 
valor por defecto para el segundo (palabra clave) argumento es una cadena vacía.  Entonces,
el mecanismo observará el componente tratará de buscar el componente con el nombre como 
cadena vacía, y ese fallará.  Cuando la búsqueda de componente falla ese 
levantará una excepción ``ComponentLookupError``.  Recuerde, eso no 
devolverá algún componente aleatorio registrado con algún otros nombre.  Las 
funciones adaptador observará `getAdapter` y `queryAdapter` también trabaja
similarmente.


Fábrica
~~~~~~~

Una ``Factory`` es un componente utilidad el cual provee interfaz 
``IFactory``.

Para crear una fábrica, primero define la interfaz del objeto: ::

  >>> from zope.interface import Attribute
  >>> from zope.interface import Interface
  >>> from zope.interface import implements

  >>> class IBaseDatos(Interface):
  ...
  ...     def obtenerConexion():
  ...         """Devuelve el objeto conexion"""

Aquí es implementación falsa de la interfaz `IBaseDatos`: ::

  >>> class FakeDb(object):
  ...
  ...     implements(IBaseDatos)
  ...
  ...     def obtenerConexion(self):
  ...         return "conexion"

Usted puede crear un fábrica usando ``zope.component.factory.Factory``: ::

  >>> from zope.component.factory import Factory

  >>> fabrica = Factory(FakeDb, 'FakeDb')

Usted puede registrarlo de esta forma: ::

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()

  >>> from zope.component.interfaces import IFactory
  >>> gsm.registerUtility(fabrica, IFactory, 'fakedb')

Para usar esta fábrica usted tal vez pueda hacerlo de esta forma: ::

  >>> from zope.component import queryUtility
  >>> queryUtility(IFactory, 'fakedb')() #doctest: +ELLIPSIS
  <FakeDb object at ...>

Esto es un acceso para usar la fábrica: ::

  >>> from zope.component import createObject
  >>> createObject('fakedb') #doctest: +ELLIPSIS
  <FakeDb object at ...>


Adaptadores avanzados
---------------------

Es capitulo discute algunos adaptadores avanzados como multi adaptador,
adaptador y manipulador de subscripción.


Multi adaptador
~~~~~~~~~~~~~~~

Un simple adaptador normalmente adaptas solamente un objeto, pero un adaptador quizás 
adapta más que un objeto.  Si un adaptador adapta mas que un 
objetos, es es llamado `multi-adaptador`.

::

  >>> from zope.interface import Interface
  >>> from zope.interface import implements
  >>> from zope.component import adapts

  >>> class IAdaptadoUno(Interface):
  ...     pass

  >>> class IAdaptadoDos(Interface):
  ...     pass

  >>> class IFuncionalidad(Interface):
  ...     pass

  >>> class MiFuncionalidad(object):
  ...     implements(IFuncionalidad)
  ...     adapts(IAdaptadoUno, IAdaptadoDos)
  ...
  ...     def __init__(self, uno, dos):
  ...         self.uno = uno
  ...         self.dos = dos

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()

  >>> gsm.registerAdapter(MiFuncionalidad)

  >>> class Uno(object):
  ...     implements(IAdaptadoUno)

  >>> class Dos(object):
  ...     implements(IAdaptadoDos)

  >>> uno = Uno()
  >>> dos = Dos()

  >>> from zope.component import getMultiAdapter

  >>> getMultiAdapter((uno,dos), IFuncionalidad) #doctest: +ELLIPSIS
  <MiFuncionalidad object at ...>

  >>> mifuncionalidad = getMultiAdapter((uno,dos), IFuncionalidad)
  >>> mifuncionalidad.uno #doctest: +ELLIPSIS
  <Uno object at ...>
  >>> mifuncionalidad.dos #doctest: +ELLIPSIS
  <Dos object at ...>


Adaptador de subscripción
~~~~~~~~~~~~~~~~~~~~~~~~~

A diferencia de los adaptadores regulares, los adaptadores de subscripción son usado cuando nosotros queremos 
todos los adaptadores que adapta un objeto a una particular interfaz.
Adaptador de subscripción es también conocido como `subscriber`.

Considere un  problema de validación.  Nosotros tenemos objetos y queremos evaluar 
si cumplen algún tipo de estándar.  Nosotros definimos una interfaz 
validación::

  >>> from zope.interface import Interface
  >>> from zope.interface import Attribute
  >>> from zope.interface import implements

  >>> class IValidar(Interface):
  ...
  ...     def validar(ob):
  ...         """Determine si el objeto es valido
  ...
  ...         Devuelve una cadena describiendo un problema de validación.
  ...         Una cadena vacía es devuelta a indicar que el 
  ...         objeto es valido.
  ...         """

Quizás nosotros tenemos documentos: ::

  >>> class IDocumento(Interface):
  ...
  ...     resumen = Attribute("Resumen del Documento")
  ...     cuerpo = Attribute("Texto del Documento")

  >>> class Documento(object):
  ...
  ...     implements(IDocumento)
  ...
  ...     def __init__(self, resumen, cuerpo):
  ...         self.resumen, self.cuerpo = resumen, cuerpo

Ahora nosotros quizás queremos especificar varios reglas de validación para 
los documentos. Por ejemplo, nosotros podríamos que el resumen sea una simple 
linea: ::

  >>> from zope.component import adapts

  >>> class ResumenLineaSimple:
  ...
  ...     adapts(IDocumento)
  ...     implements(IValidar)
  ...
  ...     def __init__(self, doc):
  ...         self.doc = doc
  ...
  ...     def validar(self):
  ...         if '\n' in self.doc.resumen:
  ...             return 'El resumen debe solamente tener una linea'
  ...         else:
  ...             return ''

O nosotros podríamos requerimos que el cuerpo sea al menos de 1000 caracteres de tamaño: ::

  >>> class LongitudAdecuada(object):
  ...
  ...     adapts(IDocumento)
  ...     implements(IValidar)
  ...
  ...     def __init__(self, doc):
  ...         self.doc = doc
  ...
  ...     def validar(self):
  ...         if len(self.doc.cuerpo) < 1000:
  ...             return 'el cuerpo del documento es muy corto'
  ...         else:
  ...             return ''

Podemos registrar esos como adaptadores de subscripción: ::

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()

  >>> gsm.registerSubscriptionAdapter(ResumenLineaSimple)
  >>> gsm.registerSubscriptionAdapter(LongitudAdecuada)

Podemos usar los subscribers para validar los objetos: ::

  >>> from zope.component import subscribers

  >>> doc = Documento("Un\nDocumento", "blah")
  >>> [adaptador.validar()
  ...  for adaptador in subscribers([doc], IValidar)
  ...  if adaptador.validar()]
  ['El resumen debe solamente tener una linea', 'El cuerpo del documento es muy corto']

  >>> doc = Documento("Un\nDocumento", "blah" * 1000)
  >>> [adaptador.validar()
  ...  for adaptador in subscribers([doc], IValidar)
  ...  if adaptador.validar()]
  ['El resumen debe solamente tener una linea']

  >>> doc = Documento("Un Documento", "blah")
  >>> [adaptador.validar()
  ...  for adaptador in subscribers([doc], IValidar)
  ...  if adaptador.validar()]
  ['El cuerpo del documento es muy corto']


Manejador
~~~~~~~~~

Los Manejador son fábricas de adaptadores de subscripción que no produce 
nada.  Lo hacen todo su trabajo cuando se le llama.  Los Manejador son 
típicamente usado para manejar eventos.  Los Manejador son también conocido como suscriptores de 
evento o adaptadores de subscripción de evento.

Los suscriptores de evento son diferentes de otros adaptadores de subscripción en 
que el llamador de los suscriptores de eventos no espera interactuar con 
cualquier manera directa.  Por ejemplo, un editor de evento no 
esperar para obtener cualquier valor de retorno.  Por que los suscriptores no necesitan 
proveer una API a sus llamadores, eso es más natural al definir entonces 
con funciones, más bien que clases.  Por ejemplo, en un 
sistema de gestión de documentos, nosotros podríamos querer registrar las fechas de creación para 
los documentos: ::

  >>> import datetime

  >>> def documentoCreado(evento):
  ...     evento.doc.creado = datetime.datetime.utcnow()

En este ejemplo, tenemos una función que toma un evento y ejecuta 
algún proceso.  Eso actualmente no devuelve nada.  Este es un 
caso especial de un adaptador de subscripción que adapta un evento a 
nada.  Todo el trabajo es hecho cuando el adaptador "fábrica" es
llamado.  Llamamos a los suscriptores que actualmente no crea ningún 
"manejador".  Esos son APIs especial para el registro y llamadas.

Para registrar el subscriptor anterior, definimos un evento del documento creado: ::

  >>> from zope.interface import Interface
  >>> from zope.interface import Attribute
  >>> from zope.interface import implements

  >>> class IDocumentoCreado(Interface):
  ...
  ...     doc = Attribute("El documento que fue creado")

  >>> class DocumentoCreado(object):
  ...
  ...     implements(IDocumentoCreado)
  ...
  ...     def __init__(self, doc):
  ...         self.doc = doc

También cambiaremos nuestra definición de manejador a: ::

  >>> def documentoCreado(evento):
  ...     evento.doc.creado = datetime.datetime.utcnow()

  >>> from zope.component import adapter

  >>> @adapter(IDocumentoCreado)
  ... def documentoCreado(evento):
  ...     evento.doc.creado = datetime.datetime.utcnow()

Esto marca al manejador como un adaptador de eventos `IDocumentoCreado`.

Ahora registramos el manejador: ::

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()

  >>> gsm.registerHandler(documentoCreado)

Ahora, podemos crear un evento y usar la función `handle` para llamar 
a los manejadores registrados por el evento: ::

  >>> from zope.component import handle

  >>> handle(documentoCreado(doc))
  >>> doc.creado.__class__.__name__
  'datetime'


Uso de la ZCA en Zope
---------------------

La Arquitectura de Componentes de Zope es usada tanto en Zope 3 y Zope 2.  Este 
capitulo ira a través del uso del ZCA en Zope.


ZCML
~~~~

El **Zope Configuration Markup Language (ZCML)** es un sistema de configuración 
basado en XML para el registro de componentes.  Así, en lugar de 
utilizar la API de Python para el registro , usted puede usar ZCML.  Pero el uso de ZCML,
desafortunadamente, usted requerirá instalar mas dependencias de 
paquetes.

Para instalar esos paquetes: ::

  $ easy_install "zope.component [zcml]"

Para registrar un adaptador: ::

  <configure xmlns="http://namespaces.zope.org/zope">

  <adapter
      factory=".empresa.SalarioEmpleado"
      provides=".interfaces.ISalario"
      for=".interfaces.IEmpleado"
      />

Los atributos `provides` y `for` son opcionales, siempre y cuando tenga
declarado en la implementación: ::

  <configure xmlns="http://namespaces.zope.org/zope">

  <adapter
      factory=".empresa.SalarioEmpleado"
      />

Si usted quiere registrar el componente como el named adapter, usted puede dar un 
atributo `name`: ::


  <configure xmlns="http://namespaces.zope.org/zope">

  <adapter
      factory=".empresa.SalarioEmpleado"
      name="salario"
      />

Las utilidades son también registradas similarmente.

Para registrar una utilidad: ::

  <configure xmlns="http://namespaces.zope.org/zope">

  <utility
      component=".basedatos.conexion"
      provides=".interfaces.IConexion"
      />

El atributo `provides` es opcional, siempre y cuando usted tenga declarado en 
la implementación: ::

  <configure xmlns="http://namespaces.zope.org/zope">

  <utility
      component=".basedatos.conexion"
      />

Si usted quiere registrar el componente como named utility, usted puede dar un 
atributo `name`: :: 


  <configure xmlns="http://namespaces.zope.org/zope">

  <utility
      component=".basedatos.conexion"
      name="Conexion de Base de datos"
      />

En lugar de directamente usar el componente, usted puede también dar una fábrica: ::

  <configure xmlns="http://namespaces.zope.org/zope">

  <utility
      factory=".basedatos.Conexion"
      />


Sobrescrituras
~~~~~~~~~~~~~~

Cuando usted registra componentes usando API Python (métodos ``register*``),
el último componente registrado remplazará el componente registrado 
previamente, si ambos son registrados con el mismo tipo de argumentos.  Por 
ejemplo, considere este ejemplo: ::

  >>> from zope.interface import Attribute
  >>> from zope.interface import Interface

  >>> class IA(Interface):
  ...     pass

  >>> class IP(Interface):
  ...     pass

  >>> from zope.interface import implements
  >>> from zope.component import adapts

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()

  >>> class AP(object):
  ...
  ...     implements(IP)
  ...     adapts(IA)
  ...
  ...     def __init__(self, context):
  ...         self.context = context

  >>> class AP2(object):
  ...
  ...     implements(IP)
  ...     adapts(IA)
  ...
  ...     def __init__(self, context):
  ...         self.context = context

  >>> class A(object):
  ...
  ...     implements(IA)

  >>> a = A()
  >>> ap = AP(a)

  >>> gsm.registerAdapter(AP)

  >>> getAdapter(a, IP) #doctest: +ELLIPSIS
  <AP object at ...>

Si usted registra otro adaptador, el existente sera remplazado: ::

  >>> gsm.registerAdapter(AP2)

  >>> getAdapter(a, IP) #doctest: +ELLIPSIS
  <AP2 object at ...>

Pero cuando registramos componentes usando ZCML, el segundo registro
lanzará un error de conflicto.  Es es una pista para usted, de lo contrario existe 
es una oportunidad para sobrescribir el registro por error.  Esto puede conducir a 
que sea difícil seguir errores en su sistema.  Entonces, usando ZCML es una ganancia para la 
aplicación.

A veces usted requerirá sobrescribir registros existentes.
ZCML provee la directiva ``includeOverrides`` para esto.  Usando esto,
usted puede escribir su sobre-escritura en un archivo separado: ::

  <includeOverrides file="overrides.zcml" />


NameChooser
~~~~~~~~~~~

Ubicación: `zope.app.container.contained.NameChooser`

Este es un adaptador para seleccionar un nombre único para un objeto dentro de un 
contenedor.

El registro del adaptador es algo como esto: ::

  <adapter
      provides=".interfaces.INameChooser"
      for="zope.app.container.interfaces.IWriteContainer"
      factory=".contained.NameChooser"
      />

Desde el registro, usted puede ver que el adaptado es un 
``IWriteContainer`` y el adaptador provee ``INameChooser``.

El adaptador provee una funcionalidad muy conveniente para programadores 
Zope.  Las principales implementaciones de ``IWriteContainer`` en
Zope 3 son ``zope.app.container.BTreeContainer`` y 
``zope.app.folder.Folder``.  Normalmente se le heredó desde 
esas implementaciones para crear su propio contendedor de clases.
Supongamos que no hay interfaz llamada ``INameChooser`` y 
adaptador, entonces usted requerirá implementar esta funcionalidad 
para cada implementaciones separadamente.


LocationPhysicallyLocatable
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Ubicación:
``zope.location.traversing.LocationPhysicallyLocatable``

Este adaptador es frecuentemente usado en aplicaciones Zope 3, pero 
normalmente eso es llamado a través de una API en ``zope.traversing.api``.
(Algún código antiguo incluso usa funciones ``zope.app.zapi``, el cual es 
otra ves uno indirecto más)

El registro del adaptador es algo como esto: ::

  <adapter
      factory="zope.location.traversing.LocationPhysicallyLocatable"
      />

La interfaz proveída y la interfaz adaptada es dada en la 
implementación.

Aquí es el inicio de la implementación::

  class LocationPhysicallyLocatable(object):
      """Proporcionar información sobre la ubicación de los objetos
      """
      zope.component.adapts(ILocation)
      zope.interface.implements(IPhysicallyLocatable)
      ...

Normalmente, casi siempre todos los objetos persistente en una aplicación Zope 3 
serán proveídos por la interfaz ``ILocation``.  Esta interfaz
tiene solamente dos atributos, ``__parent__`` y ``__name__``.  El 
``__parent__`` es el padre de la jerarquía de ubicación.  Y 
``__name__`` es el nombre con el padre.

La interfaz ``IPhysicallyLocatable`` tiene cuatro métodos:
``getRoot``, ``getPath``, ``getName``, y ``getNearestSite``.

  - La función ``getRoot`` devuelve el objeto raíz físico.

  - La función ``getPath`` devuelve el ruta física al objeto como una
    cadena.

  - ``getName`` devuelve el ultimo segmento de la ruta física.

  - ``getNearestSite`` devuelve el sitio, el objeto es contenido
    en el.  Si el objeto es un sitio, el objeto en si mismo es devuelto.

Si usted aprende Zope 3, usted puede ver que esos son las cosas 
importante las cuales usted requiere muy a menudo.  Para entender la belleza 
de este sistema , usted debe ver como Zope 2 actualmente obtiene el raíz 
físico y como ese es implementado.  Allí hay un método llamado 
``getPhysicalRoot`` virtualmente para todos los contenedores objetos.


DefaultSized
~~~~~~~~~~~~

Ubicación: ``zope.size.DefaultSized``

Este adaptador es solo una implementación por defecto de la interfaz ``ISized``.
Este adaptador es registrado por todos los tipos de objetos.  Si usted quiere 
registrar este esta adaptador para una interfaz particular, entonces tiene que 
sobrescribir este registro para su implementación.

El registro del adaptador es algo como esto: ::

  <adapter
      for="*"
      factory="zope.size.DefaultSized"
      provides="zope.size.interfaces.ISized"
      permission="zope.View"
      />

Como usted puede ver, la interfaz  adaptada es `*`, entonces eso puede adaptar a cualquier tipo 
de objetos.

El ``ITamano`` es una interfaz simple con dos métodos contratados: ::

  class ITamano(Interface):

      def ordenarPorTamano():
          """Devuelve una tupla (basic_unit, amount)

          Se utiliza para clasificar entre los diferentes tipos de objetos de tamaño.
          'amount' sólo necesita ser clasificable entre las cosas que comparten 
          la misma unidad básica."""

      def mostrarPorTamano():
          """Devuelve una cadena dando el tamaño.
          """

Usted puede ver otro adaptador ``ITamano`` registrado para ``IZPTPage`` en
el paquete ``zope.app.zptpage``.


ZopeVersionUtility
~~~~~~~~~~~~~~~~~~

Ubicación: ``zope.app.applicationcontrol.ZopeVersionUtility``

Esta utilidad da la versión del servidor Zope ejecutando.

El registro va algo así: ::

  <utility
      component=".zopeversion.ZopeVersionUtility"
      provides=".interfaces.IZopeVersion" />

La interfaz proveída, ``IZopeVersion``, tiene solamente un método nombrado 
``getZopeVersion``.  Este método devuelve una cadena que contienen la versión 
de Zope (posiblemente incluyendo información de SVN).

La implementación por defecto, ``ZopeVersionUtility``, obtiene la información de la versión 
desde un archivo ``version.txt`` en el directorio `zope/app`.  Si Zope esta 
ejecutando desde una comprobación subversion, eso mostrará el ultimo número de versión 
de la revisión.  Si none de arriba trabaja ese se define a:
`Development/Unknown`.


Caso de estudio
---------------

.. note::

  Este capitulo no esta completado.  ¡Por favor, envíe sus sugerencias!

Introducción
~~~~~~~~~~~~

Este capitulo demuestra la creación de una aplicación escritorio usando librería PyGTK 
GUI y la ZCA.  Esta aplicación también usa dos diferentes 
tipos de mecanismos de persistencia de data, una base de datos objeto (ZODB) & y 
otro base de datos relacional (SQLite).  Como siempre, prácticamente, solamente un 
almacenamiento puede ser usado para una instalación particular.  La razón para 
usar dos diferente mecanismos persistencia es para demostrar como 
usar la ZCA  para pegar los componentes.  Mayormente del código en esta 
aplicación es relacionada a PyGTK.

Como la aplicación crece usted quizás use los componentes ZCA donde sea 
quiera habilitar el mecanismo de plugin o extensibilidad.  Uso la llanura objetos Python directamente 
donde usted no requiere el mecanismo de plugin o extensibilidad.

Allí no hay diferencia en usar la ZCA para web o aplicaciones de escritorio o para cualquier otro 
tipo de aplicación o framework.  Es es mejor para seguir una 
convención para la ubicación desde donde usted esta yendo a registrar 
componentes.  Esta aplicación use una convención, el cual puede ser extendido 
colocando el registro de componentes similares en módulos separado y 
luego importar entonces desde el módulo de registro principal.  En esta aplicación
el módulo de registro principal del componente es `register.py`.

El código fuente de esta aplicación puede ser descargado desde la dirección URL:
http://www.muthukadan.net/downloads/zcalib.tar.bz2


Casos de uso
~~~~~~~~~~~~

La aplicación que vamos a discutir aquí hay una sistema gestión de 
bibliotecas con características mínimas.  Los requisitos se pueden resumir como 
esto:

  - Agregar miembros con un único número y nombre.

  - Agregar registros con código de barra, autor & título

  - Emitir libros

  - Devolver libros


La aplicación puede ser diseñado de tal manera que las principales características pueden 
puede acceder desde una sola ventana.  La ventana principal para acceder a todos 
esas características pueden ser diseñada como este:

.. image:: mainwindow.png
   :align: center

Desde la ventana de gestión de miembro, el usuario debería tener la habilidad de administrar miembros.  Entonces,
el miembro agrega la ventana debería tener los botones *agregar*, *actualizar* y 
*eliminar*:

.. image:: memberwindow.png
   :align: center

Desde la ventana catalogo, el usuario puede *agregar*, *editar* y *eliminar* libros:

.. image:: catalogwindow.png
   :align: center

La ventana de la circulación debe tener la facilidad de emitir y
devolver los libros:

.. image:: circulationwindow.png
   :align: center


Descripción general del código PyGTK
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Como se puede ver en el código, la mayoría del código están relacionados con PyGTK.
La estructura de código es muy similar para las diferentes ventanas.  Las ventana 
de esta aplicación son diseñadas usando Glade GUI builder.  Usted debe 
dar nombres apropiado para los widgets usted esta yendo a usar desde el código.  En la 
ventana anterior, todas las entradas del menú tiene nombres como: circulación, catalogo,
miembro, salir & acerca de.

El objeto ``gtk.glade.XML`` es usado para parsear el archivo glade, esto 
creará los objetos widget GUI.  Esto es como parsear y acceder a los objetos: ::

  import gtk.glade
  xmlobj = gtk.glade.XML('/path/to/file.glade')
  widget = xmlobj.get_widget('widget_name')

En el archivo ``mainwindow.py``, usted puede ver el código como este: ::

  curdir = os.path.abspath(os.path.dirname(__file__))
  xml = os.path.join(curdir, 'glade', 'mainwindow.glade')
  xmlobj = gtk.glade.XML(xml)

  self.mainwindow = xmlobj.get_widget('mainwindow')

El nombre del widget de la ventana principal es `mainwindow`.  Similarmente, otros 
widgets se recuperan por debajo de ese: ::

  circulation = xmlobj.get_widget('circulation')
  member = xmlobj.get_widget('member')
  quit = xmlobj.get_widget('quit')
  catalog = xmlobj.get_widget('catalog')
  about = xmlobj.get_widget('about')

Entonces, esos widgets son conectados para algunos eventos: ::

  self.mainwindow.connect('delete_event', self.delete_event)
  quit.connect('activate', self.delete_event)
  circulation.connect('activate', self.on_circulation_activate)
  member.connect('activate', self.on_member_activate)
  catalog.connect('activate', self.on_catalog_activate)
  about.connect('activate', self.on_about_activate)

El `delete_event` es el evento cuando la ventana esta cerrando usando el botón 
de cerrar ventana.  El evento `activate` evento se emite cuando el menú es 
seleccionado.  Los widgets se conectan a algunas funciones de devolución de llamada para
algunos eventos.

Se puede ver en el código anterior que, la ventana principal está conectado al 
método `on_delete_event` para `delete_event`.  El widget `quit` es 
también conectado al mismo método para el evento `activate`: ::

    def on_delete_event(self, *args):
        gtk.main_quit()

La función de devolución de llamada solo llama la función `main_quit`


El código
~~~~~~~~~

Este es el archivo `zcalib.py`: ::

  import registry
  import mainwindow

  if __name__ == '__main__':
      registry.initialize()
      try:
          mainwindow.main()
      except KeyboardInterrupt:
          import sys
          sys.exit(1)

Aquí, dos módulos importados `registry` y `mainwindow`.  Entonces,
el registro es inicializado y la función `main` de mainwindow es llamada.
Si el usuario esta tratando de salir de la aplicación usando `Ctrl+C`, el sistema saldrá 
normalmente, eso es por que nosotros captamos la excepción `KeyboardInterrupt`.

Este es el archivo `registry.py`: ::

  import sys
  from zope.component import getGlobalSiteManager

  from interfaces import IMember
  from interfaces import IBook
  from interfaces import ICirculation
  from interfaces import IDbOperation


  def initialize_rdb():
      from interfaces import IRelationalDatabase
      from relationaldatabase import RelationalDatabase
      from member import MemberRDbOperation
      from catalog import BookRDbOperation
      from circulation import CirculationRDbOperation

      gsm = getGlobalSiteManager()
      db = RelationalDatabase()
      gsm.registerUtility(db, IRelationalDatabase)

      gsm.registerAdapter(MemberRDbOperation,
                          (IMember,),
                          IDbOperation)

      gsm.registerAdapter(BookRDbOperation,
                          (IBook,),
                          IDbOperation)

      gsm.registerAdapter(CirculationRDbOperation,
                          (ICirculation,),
                          IDbOperation)

  def initialize_odb():
      from interfaces import IObjectDatabase
      from objectdatabase import ObjectDatabase
      from member import MemberODbOperation
      from catalog import BookODbOperation
      from circulation import CirculationODbOperation

      gsm = getGlobalSiteManager()
      db = ObjectDatabase()
      gsm.registerUtility(db, IObjectDatabase)

      gsm.registerAdapter(MemberODbOperation,
                          (IMember,),
                          IDbOperation)

      gsm.registerAdapter(BookODbOperation,
                          (IBook,),
                          IDbOperation)

      gsm.registerAdapter(CirculationODbOperation,
                          (ICirculation,),
                          IDbOperation)

  def check_use_relational_db():
      use_rdb = False
      try:
          arg = sys.argv[1]
          if arg == '-r':
              return True
      except IndexError:
          pass
      return use_rdb

  def initialize():
      use_rdb = check_use_relational_db()
      if use_rdb:
          initialize_rdb()
      else:
          initialize_odb()

Ver en la función `initialize` en el cual estamos llamando desde el módulo 
principal, `zcalib.py`.  La función `initialize` primero comprueba cual base de datos 
usar, base de datos relacional (DBR) o base de datos objeto (BDO) y esto 
esta hecho en función `check_use_relational_db`.  Si la opción `-r`
es dada en linea de comando, eso llamará `initialize_rdb` 
de otra manera, `initialize_odb`.  Si la función BDR es llamada, esa 
instalara todos los componentes relacionados a BDR.  Y por otra parte, si la función 
BDO es llamada, esa instalara todos los componentes relacionados a BDO.

Aquí es el archivo `mainwindow.py`: ::

  import os
  import gtk
  import gtk.glade

  from circulationwindow import circulationwindow
  from catalogwindow import catalogwindow
  from memberwindow import memberwindow

  class MainWindow(object):

      def __init__(self):
          curdir = os.path.abspath(os.path.dirname(__file__))
          xml = os.path.join(curdir, 'glade', 'mainwindow.glade')
          xmlobj = gtk.glade.XML(xml)

          self.mainwindow = xmlobj.get_widget('mainwindow')
          circulation = xmlobj.get_widget('circulation')
          member = xmlobj.get_widget('member')
          quit = xmlobj.get_widget('quit')
          catalog = xmlobj.get_widget('catalog')
          about = xmlobj.get_widget('about')

          self.mainwindow.connect('delete_event', self.delete_event)
          quit.connect('activate', self.delete_event)

          circulation.connect('activate', self.on_circulation_activate)
          member.connect('activate', self.on_member_activate)
          catalog.connect('activate', self.on_catalog_activate)
          about.connect('activate', self.on_about_activate)

      def delete_event(self, *args):
          gtk.main_quit()

      def on_circulation_activate(self, *args):
          circulationwindow.show_all()

      def on_member_activate(self, *args):
          memberwindow.show_all()

      def on_catalog_activate(self, *args):
          catalogwindow.show_all()

      def on_about_activate(self, *args):
          pass

      def run(self):
          self.mainwindow.show_all()

  def main():
      mainwindow = MainWindow()
      mainwindow.run()
      gtk.main()


La función `main` aquí crear una instancia de clase `MainWindow`,
el cual inicializará todos los widgets.

Aquí es el archivo `memberwindow.py`::

  import os
  import gtk
  import gtk.glade

  from zope.component import getAdapter

  from components import Member
  from interfaces import IDbOperation


  class MemberWindow(object):

      def __init__(self):
          curdir = os.path.abspath(os.path.dirname(__file__))
          xml = os.path.join(curdir, 'glade', 'memberwindow.glade')
          xmlobj = gtk.glade.XML(xml)

          self.memberwindow = xmlobj.get_widget('memberwindow')
          self.number = xmlobj.get_widget('number')
          self.name = xmlobj.get_widget('name')
          add = xmlobj.get_widget('add')
          update = xmlobj.get_widget('update')
          delete = xmlobj.get_widget('delete')
          close = xmlobj.get_widget('close')
          self.treeview = xmlobj.get_widget('treeview')

          self.memberwindow.connect('delete_event', self.on_delete_event)
          add.connect('clicked', self.on_add_clicked)
          update.connect('clicked', self.on_update_clicked)
          delete.connect('clicked', self.on_delete_clicked)
          close.connect('clicked', self.on_delete_event)

          self.initialize_list()

      def show_all(self):
          self.populate_list_store()
          self.memberwindow.show_all()

      def populate_list_store(self):
          self.list_store.clear()
          member = Member()
          memberdboperation = getAdapter(member, IDbOperation)
          members = memberdboperation.get()
          for member in members:
              number = member.number
              name = member.name
              self.list_store.append((member, number, name,))

      def on_delete_event(self, *args):
          self.memberwindow.hide()
          return True

      def initialize_list(self):
          self.list_store = gtk.ListStore(object, str, str)
          self.treeview.set_model(self.list_store)
          tvcolumn = gtk.TreeViewColumn('Member Number')
          self.treeview.append_column(tvcolumn)

          cell = gtk.CellRendererText()
          tvcolumn.pack_start(cell, True)
          tvcolumn.add_attribute(cell, 'text', 1)

          tvcolumn = gtk.TreeViewColumn('Member Name')
          self.treeview.append_column(tvcolumn)

          cell = gtk.CellRendererText()
          tvcolumn.pack_start(cell, True)
          tvcolumn.add_attribute(cell, 'text', 2)

      def on_add_clicked(self, *args):
          number = self.number.get_text()
          name = self.name.get_text()
          member = Member()
          member.number = number
          member.name = name
          self.add(member)
          self.list_store.append((member, number, name,))

      def add(self, member):
          memberdboperation = getAdapter(member, IDbOperation)
          memberdboperation.add()

      def on_update_clicked(self, *args):
          number = self.number.get_text()
          name = self.name.get_text()
          treeselection = self.treeview.get_selection()
          model, iter = treeselection.get_selected()
          if not iter:
              return
          member = self.list_store.get_value(iter, 0)
          member.number = number
          member.name = name
          self.update(member)
          self.list_store.set(iter, 1, number, 2, name)

      def update(self, member):
          memberdboperation = getAdapter(member, IDbOperation)
          memberdboperation.update()

      def on_delete_clicked(self, *args):
          treeselection = self.treeview.get_selection()
          model, iter = treeselection.get_selected()
          if not iter:
              return
          member = self.list_store.get_value(iter, 0)
          self.delete(member)
          self.list_store.remove(iter)

      def delete(self, member):
          memberdboperation = getAdapter(member, IDbOperation)
          memberdboperation.delete()

  memberwindow = MemberWindow()

Aquí es el archivo `components.py`: ::

  from zope.interface import implements

  from interfaces import IBook
  from interfaces import IMember
  from interfaces import ICirculation

  class Book(object):

      implements(IBook)

      barcode = ""
      title = ""
      author = ""

  class Member(object):

      implements(IMember)

      number = ""
      name = ""

  class Circulation(object):

      implements(ICirculation)

      book = Book()
      member = Member()

Aquí es el archivo `interfaces.py`: ::

  from zope.interface import Interface
  from zope.interface import Attribute


  class IBook(Interface):

      barcode = Attribute("Barcode")
      author = Attribute("Author of book")
      title = Attribute("Title of book")


  class IMember(Interface):

      number = Attribute("ID number")
      name = Attribute("Name of member")


  class ICirculation(Interface):

      book = Attribute("A book")
      member = Attribute("A member")


  class IRelationalDatabase(Interface):

      def commit():
          pass

      def rollback():
          pass

      def cursor():
          pass

      def get_next_id():
          pass


  class IObjectDatabase(Interface):

      def commit():
          pass

      def rollback():
          pass

      def container():
          pass

      def get_next_id():
          pass


  class IDbOperation(Interface):

      def get():
          pass

      def add():
          pass

      def update():
          pass

      def delete():
          pass

Aquí es el archivo `member.py`: ::

  from zope.interface import implements
  from zope.component import getUtility
  from zope.component import adapts

  from components import Member

  from interfaces import IRelationalDatabase
  from interfaces import IObjectDatabase
  from interfaces import IMember
  from interfaces import IDbOperation


  class MemberRDbOperation(object):

      implements(IDbOperation)
      adapts(IMember)

      def __init__(self, member):
          self.member = member

      def get(self):
          db = getUtility(IRelationalDatabase)
          cr = db.cursor()
          number = self.member.number
          if number:
              cr.execute("""SELECT
                              id,
                              number,
                              name
                            FROM members
                            WHERE number = ?""",
                         (number,))
          else:
              cr.execute("""SELECT
                              id,
                              number,
                              name
                            FROM members""")
          rst = cr.fetchall()
          cr.close()
          members = []
          for record in rst:
              id = record['id']
              number = record['number']
              name = record['name']
              member = Member()
              member.id = id
              member.number = number
              member.name = name
              members.append(member)
          return members

      def add(self):
          db = getUtility(IRelationalDatabase)
          cr = db.cursor()
          next_id = db.get_next_id("members")
          number = self.member.number
          name = self.member.name
          cr.execute("""INSERT INTO members
                          (id, number, name)
                        VALUES (?, ?, ?)""",
                     (next_id, number, name))
          cr.close()
          db.commit()
          self.member.id = next_id

      def update(self):
          db = getUtility(IRelationalDatabase)
          cr = db.cursor()
          number = self.member.number
          name = self.member.name
          id = self.member.id
          cr.execute("""UPDATE members
                          SET
                             number = ?,
                             name = ?
                        WHERE id = ?""",
                     (number, name, id))
          cr.close()
          db.commit()

      def delete(self):
          db = getUtility(IRelationalDatabase)
          cr = db.cursor()
          id = self.member.id
          cr.execute("""DELETE FROM members
                        WHERE id = ?""",
                     (id,))
          cr.close()
          db.commit()


  class MemberODbOperation(object):

      implements(IDbOperation)
      adapts(IMember)

      def __init__(self, member):
          self.member = member

      def get(self):
          db = getUtility(IObjectDatabase)
          zcalibdb = db.container()
          members = zcalibdb['members']
          return members.values()

      def add(self):
          db = getUtility(IObjectDatabase)
          zcalibdb = db.container()
          members = zcalibdb['members']
          number = self.member.number
          if number in [x.number for x in members.values()]:
              db.rollback()
              raise Exception("Duplicate key")
          next_id = db.get_next_id('members')
          self.member.id = next_id
          members[next_id] = self.member
          db.commit()

      def update(self):
          db = getUtility(IObjectDatabase)
          zcalibdb = db.container()
          members = zcalibdb['members']
          id = self.member.id
          members[id] = self.member
          db.commit()

      def delete(self):
          db = getUtility(IObjectDatabase)
          zcalibdb = db.container()
          members = zcalibdb['members']
          id = self.member.id
          del members[id]
          db.commit()


PySQLite
~~~~~~~~

ZODB
~~~~

Conclusiones
~~~~~~~~~~~~

Referencia
----------


adaptedBy
~~~~~~~~~

Esta función ayuda a buscar las interfaces adaptadas.

 - Ubicación: ``zope.component``

 - Firma: `adaptedBy(object)`

Ejemplo: ::

  >>> from zope.interface import implements
  >>> from zope.component import adapts
  >>> from zope.component import adaptedBy

  >>> class RegistradorHuespedNG(object):
  ...
  ...     implements(IRegistrador)
  ...     adapts(IHuesped)
  ...
  ...     def __init__(self, huesped):
  ...         self.huesped = huesped

  >>> adaptedBy(RegistradorHuespedNG)
  (<InterfaceClass __builtin__.IHuesped>,)


adapter
~~~~~~~

Los adaptadores puede ser cualquier objeto llamable, usted puede usar el decorador `adapter` 
para declarar que un objeto llamable adapta algunas interfaces (o 
clases)

 - Ubicación: ``zope.component``

 - Firma: `adapter(*interfaces)`

Ejemplo: ::

  >>> from zope.interface import Attribute
  >>> from zope.interface import Interface
  >>> from zope.interface import implementer
  >>> from zope.component import adapter
  >>> from zope.interface import implements

  >>> class ITrabajo(Interface):
  ...     """Un trabajo"""

  >>> class Trabajo(object):
  ...     implements(ITrabajo)

  >>> class IPersona(Interface):
  ...
  ...     nombre = Attribute("Nombre")
  ...     trabajo = Attribute("Trabajo")

  >>> class Persona(object):
  ...     implements(IPersona)
  ...
  ...     nombre = None
  ...     trabajo = None

  >>> @implementer(ITrabajo)
  ... @adapter(IPersona)
  ... def trabajoPersona(persona):
  ...     return persona.trabajo

  >>> pedro = Persona()
  >>> pedro.nombre = "Pedro"
  >>> pedro.trabajo = Trabajo()
  >>> trabajoPersona(pedro) #doctest: +ELLIPSIS
  <Trabajo object at ...>


adapts
~~~~~~

Esta función ayuda a declarar las clases adaptador.

 - Ubicación: ``zope.component``

 - Firma: `adapts(*interfaces)`

Ejemplo: ::

  >>> from zope.interface import implements
  >>> from zope.component import adapts

  >>> class RegistradorHuespedNG(object):
  ...
  ...     implements(IRegistrador)
  ...     adapts(IHuesped)
  ...
  ...     def __init__(self, huesped):
  ...         self.huesped = huesped
  ...
  ...     def registrar(self):
  ...         huesped_id = obtener_proximo_id()
  ...         huespedes_db[huesped_id] = {
  ...         'nombre': huesped.nombre,
  ...         'lugar': huesped.lugar,
  ...         'telefono': huesped.telefono
  ...         }


alsoProvides
~~~~~~~~~~~~

Declara interfaces declaradas directamente para un objeto.  Los argumentos 
después del objeto son uno o más interfaces.  Las interfaces dadas son 
agregada a las interfaces previamente declaradas por el objeto.

 - Ubicación: ``zope.interface``

 - Firma: `alsoProvides(object, *interfaces)`

Ejemplo: ::

  >>> from zope.interface import Attribute
  >>> from zope.interface import Interface
  >>> from zope.interface import implements
  >>> from zope.interface import alsoProvides

  >>> class IPersona(Interface):
  ...
  ...     nombre = Attribute("Nombre de persona")

  >>> class IEstudiante(Interface):
  ...
  ...     colegio = Attribute("Nombre de colegio")

  >>> class Persona(object):
  ...
  ...     implements(IRegistrador)
  ...     nombre = u""

  >>> pedro = Persona()
  >>> pedro.nombre = "Pedro"
  >>> pedro.colegio = "Nuevo Colegio"
  >>> alsoProvides(pedro, IEstudiante)

  Usted puede probar con esto: ::

  >>> from zope.interface import providedBy
  >>> IEstudiante in providedBy(pedro)
  True


Atributo
~~~~~~~~

Usando esta clase, usted puede definir atributos normales en una interfaz.

 - Ubicación: ``zope.interface``

 - Firma: `Attribute(name, doc='')`

 - Ver también: `Interface`_

Ejemplo: ::

  >>> from zope.interface import Attribute
  >>> from zope.interface import Interface

  >>> class IPersona(Interface):
  ...
  ...     nombre = Attribute("Nombre de persona")
  ...     email = Attribute("Direccion de email")


classImplements
~~~~~~~~~~~~~~~

Declara interfaces adicionales implementadas por instancias de una clase.
Los argumentos después de la clase son uno o más interfaces  Las 
interfaces dadas son agregadas a cualquier interfaces previamente declaradas.

 - Ubicación: ``zope.interface``

 - Firma: `classImplements(cls, *interfaces)`

Ejemplo: ::

  >>> from zope.interface import Attribute
  >>> from zope.interface import Interface
  >>> from zope.interface import implements
  >>> from zope.interface import classImplements

  >>> class IPersona(Interface):
  ...
  ...     nombre = Attribute("Nombre de persona")

  >>> class IEstudiante(Interface):
  ...
  ...     colegio = Attribute("Nombre de colegio")

  >>> class Persona(object):
  ...
  ...     implements(IRegistrador)
  ...     nombre = u""
  ...     colegio = u""

  >>> classImplements(Persona, IStudent)
  >>> pedro = Persona()
  >>> pedro.nombre = "Pedro"
  >>> pedro.colegio = "Nuevo Colegio"

  Usted puede probar con esto: ::

  >>> from zope.interface import providedBy
  >>> IEstudiante in providedBy(pedro)
  True


classImplementsOnly
~~~~~~~~~~~~~~~~~~~

Declara solamente interfaces implementadas por instancias de una clase.  Los 
argumentos después de la clase son uno o más interfaces  Las interfaces 
dadas remplazan cualquier declaraciones previas.

 - Ubicación: ``zope.interface``

 - Firma: `classImplementsOnly(cls, *interfaces)`

Ejemplo: ::

  >>> from zope.interface import Attribute
  >>> from zope.interface import Interface
  >>> from zope.interface import implements
  >>> from zope.interface import classImplementsOnly

  >>> class IPersona(Interface):
  ...
  ...     nombre = Attribute("Nombre de persona")

  >>> class IEstudiante(Interface):
  ...
  ...     colegio = Attribute("Nombre de colegio")

  >>> class Persona(object):
  ...
  ...     implements(IPersona)
  ...     colegio = u""

  >>> classImplementsOnly(Persona, IEstudiante)
  >>> pedro = Persona()
  >>> pedro.colegio = "Nuevo Colegio"

  Usted puede probar con esto: ::

  >>> from zope.interface import providedBy
  >>> IPersona in providedBy(pedro)
  False
  >>> IEstudiante in providedBy(pedro)
  True


classProvides
~~~~~~~~~~~~~

Normalmente si una clase implementa una interfaz particular, la instancia de 
esa clase proveerá  la interfaz implementada por esa clase.  Pero 
si usted quiere una clase que sea proveída por una interfaz, usted puede declararlo 
usando función ``classProvides``.

 - Ubicación: ``zope.interface``

 - Firma: `classProvides(*interfaces)`

Ejemplo: ::

  >>> from zope.interface import Attribute
  >>> from zope.interface import Interface
  >>> from zope.interface import classProvides

  >>> class IPersona(Interface):
  ...
  ...     nombre = Attribute("Nombre de persona")

  >>> class Persona(object):
  ...
  ...     classProvides(IPersona)
  ...     nombre = u"Pedro"

  Usted puede probar con esto: ::

  >>> from zope.interface import providedBy
  >>> IPersona in providedBy(Persona)
  True


ComponentLookupError
~~~~~~~~~~~~~~~~~~~~

Esta es la excepción lanzada cuando una búsqueda de componente falla.

Ejemplo: ::

  >>> class IPersona(Interface):
  ...
  ...     nombre = Attribute("Nombre de persona")

  >>> persona = object()
  >>> getAdapter(persona, IPersona, 'not-exists') #doctest: +ELLIPSIS
  Traceback (most recent call last):
  ...
  ComponentLookupError: ...


createObject
~~~~~~~~~~~~

Crear un objeto usando una fábrica.

Busca la fábrica nombrada en el actual sitio y llama ese con los 
argumentos dados.  Si una coincidencia de búsqueda de fábrica no es encontrada lanza 
una error de excepción ``ComponentLookupError``.  Devuelve el objeto creado.

Un argumento palabras de clave de contexto puede ser proveído para causar que la fábrica 
busque en otra ubicación en el sitio actual.  (Por supuesto, esto 
significa que eso es imposible para pasar un argumento clave valor nombrado "context"
a la fábrica.

 - Ubicación: ``zope.component``

 - Firma: `createObject(factory_name, *args, **kwargs)`

Ejemplo: ::

  >>> from zope.interface import Attribute
  >>> from zope.interface import Interface
  >>> from zope.interface import implements

  >>> class IBaseDatos(Interface):
  ...
  ...     def obtenerConexion():
  ...         """Devuelve el objeto conexion"""

  >>> class FakeDb(object):
  ...
  ...     implements(IBaseDatos)
  ...
  ...     def obtenerConexion(self):
  ...         return "conexion"

  >>> from zope.component.factory import Factory

  >>> fabrica = Factory(FakeDb, 'FakeDb')

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()

  >>> from zope.component.interfaces import IFactory
  >>> gsm.registerUtility(fabrica, IFactory, 'fakedb')

  >>> from zope.component import createObject
  >>> createObject('fakedb') #doctest: +ELLIPSIS
  <FakeDb object at ...>


Declaration
~~~~~~~~~~~

No necesita usarlo directamente.


directlyProvidedBy
~~~~~~~~~~~~~~~~~~

Esta función devolverá las interfaces directamente proveída por el 
objeto dado.

 - Ubicación: ``zope.interface``

 - Firma: `directlyProvidedBy(object)`

Ejemplo: ::

  >>> from zope.interface import Attribute
  >>> from zope.interface import Interface

  >>> class IPersona(Interface):
  ...
  ...     nombre = Attribute("Nombre de persona")

  >>> class IEstudiante(Interface):
  ...
  ...     colegio = Attribute("Nombre de colegio")

  >>> class IPersonaInteligente(Interface):
  ...     pass

  >>> class Persona(object):
  ...
  ...     implements(IPersona)
  ...     nombre = u""

  >>> pedro = Persona()
  >>> pedro.nombre = u"Pedro"
  >>> pedro.colegio = "Nuevo Colegio"
  >>> alsoProvides(pedro, IPersonaInteligente, IEstudiante)

  >>> from zope.interface import directlyProvidedBy

  >>> pedro_dp = directlyProvidedBy(pedro)
  >>> IPersona in pedro_dp.interfaces()
  False
  >>> IEstudiante in pedro_dp.interfaces()
  True
  >>> IPersonaInteligente in pedro_dp.interfaces()
  True


directlyProvides
~~~~~~~~~~~~~~~~

Declara interfaces declaradas directamente para un objeto.  Los argumentos 
después del objeto son uno o más interfaces.  Las interfaces dadas 
remplaza las interfaces previamente declaradas por el objeto.

 - Ubicación: ``zope.interface``

 - Firma: `directlyProvides(object, *interfaces)`

Ejemplo: ::

  >>> from zope.interface import Attribute
  >>> from zope.interface import Interface

  >>> class IPersona(Interface):
  ...
  ...     nombre = Attribute("Nombre de persona")

  >>> class IEstudiante(Interface):
  ...
  ...     colegio = Attribute("Nombre de colegio")

  >>> class IPersonaInteligente(Interface):
  ...     pass

  >>> class Persona(object):
  ...
  ...     implements(IPersona)
  ...     nombre = u""

  >>> pedro = Persona()
  >>> pedro.nombre = u"Pedro"
  >>> pedro.colegio = "Nuevo Colegio"
  >>> alsoProvides(pedro, IPersonaInteligente, IEstudiante)

  >>> from zope.interface import directlyProvidedBy

  >>> pedro_dp = directlyProvidedBy(pedro)
  >>> IPersonaInteligente in pedro_dp.interfaces()
  True
  >>> IPersona in pedro_dp.interfaces()
  False
  >>> IEstudiante in pedro_dp.interfaces()
  True
  >>> from zope.interface import providedBy

  >>> IPersonaInteligente in providedBy(pedro)
  True

  >>> from zope.interface import directlyProvides
  >>> directlyProvides(pedro, IEstudiante)

  >>> pedro_dp = directlyProvidedBy(pedro)
  >>> IPersonaInteligente in pedro_dp.interfaces()
  False
  >>> IPersona in pedro_dp.interfaces()
  False
  >>> IEstudiante in pedro_dp.interfaces()
  True

  >>> IPersonaInteligente in providedBy(pedro)
  False


getAdapter
~~~~~~~~~~

Obtiene un named adapter a una interfaz para un objeto.  Devuelve un adaptador
que puede adaptar un objeto a una interfaz.  Si una coincidencia de la búsqueda de adaptador no se 
encontró, se dispara una excepción de error``ComponentLookupError``.

 - Ubicación: ``zope.interface``

 - Firma: `getAdapter(object, interface=Interface, name=u'', context=None)`

Ejemplo: ::

  >>> from zope.interface import Attribute
  >>> from zope.interface import Interface

  >>> class IRegistrador(Interface):
  ...     """Un registrador registrará los detalles de un objeto"""
  ...
  ...     def registrar():
  ...         """Registrar detalles de un objeto"""
  ...

  >>> from zope.interface import implements
  >>> from zope.component import adapts

  >>> class RegistradorHuespedNG(object):
  ...
  ...     implements(IRegistrador)
  ...     adapts(IHuesped)
  ...
  ...     def __init__(self, huesped):
  ...         self.huesped = huesped
  ...
  ...     def registrar(self):
  ...         huesped_id = obtener_proximo_id()
  ...         huespedes_db[huesped_id] = {
  ...         'nombre': huesped.nombre,
  ...         'lugar': huesped.lugar,
  ...         'telefono': huesped.telefono
  ...         }

  >>> class Huesped(object):
  ...
  ...     implements(IHuesped)
  ...
  ...     def __init__(self, nombre, lugar):
  ...         self.nombre = nombre
  ...         self.lugar = lugar

  >>> pedro = Huesped("Pedro", "España")
  >>> pedro_registradorhuesped = RegistradorHuespedNG(pedro)

  >>> IRegistrador.providedBy(pedro_registradorhuesped)
  True

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()
  >>> gsm.registerAdapter(RegistradorHuespedNG,
  ...                     (IHuesped,), IRegistrador, 'ng')

  >>> getAdapter(pedro, IRegistrador, 'ng') #doctest: +ELLIPSIS
  <RegistradorHuespedNG object at ...>


getAdapterInContext
~~~~~~~~~~~~~~~~~~~

En vez de esta función, use el argumento `context` de la función 
`getAdapter`_.

 - Ubicación: ``zope.component``

 - Firma: `getAdapterInContext(object, interface, context)`

 - Ver también: `queryAdapterInContext`_

Ejemplo: ::

  >>> from zope.component.globalregistry import BaseGlobalComponents
  >>> from zope.component import IComponentLookup
  >>> sm = BaseGlobalComponents()

  >>> class Context(object):
  ...     def __init__(self, sm):
  ...         self.sm = sm
  ...     def __conform__(self, interface):
  ...         if interface.isOrExtends(IComponentLookup):
  ...             return self.sm

  >>> context = Context(sm)

  >>> from zope.interface import Attribute
  >>> from zope.interface import Interface

  >>> class IRegistrador(Interface):
  ...     """Un registrador registrará los detalles de un objeto"""
  ...
  ...     def registrar():
  ...         """Registrar detalles de un objeto"""
  ...

  >>> from zope.interface import implements
  >>> from zope.component import adapts

  >>> class RegistradorHuespedNG(object):
  ...
  ...     implements(IRegistrador)
  ...     adapts(IHuesped)
  ...
  ...     def __init__(self, huesped):
  ...         self.huesped = huesped
  ...
  ...     def registrar(self):
  ...         huesped_id = obtener_proximo_id()
  ...         huespedes_db[huesped_id] = {
  ...         'nombre': huesped.nombre,
  ...         'lugar': huesped.lugar,
  ...         'telefono': huesped.telefono
  ...         }

  >>> class Huesped(object):
  ...
  ...     implements(IHuesped)
  ...
  ...     def __init__(self, nombre, lugar):
  ...         self.nombre = nombre
  ...         self.lugar = lugar

  >>> pedro = Huesped("Pedro", "España")
  >>> pedro_registradorhuesped = RegistradorHuespedNG(pedro)

  >>> IRegistrador.providedBy(pedro_registradorhuesped)
  True

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()
  >>> sm.registerAdapter(RegistradorHuespedNG,
  ...                     (IHuesped,), IRegistrador)

  >>> from zope.component import getAdapterInContext

  >>> getAdapterInContext(pedro, IRegistrador, sm) #doctest: +ELLIPSIS
  <RegistradorHuespedNG object at ...>


getAdapters
~~~~~~~~~~~

Busca por todas las coincidencias de los adaptadores para una interfaz proveída por los objetos.
Devuelve una lista de adaptadores que coinciden. Si un adaptador es nombrado, solamente el 
adaptador mas especifico de un nombre dado es devuelto.

 - Ubicación: ``zope.component``

 - Firma: `getAdapters(objects, provided, context=None)`

Ejemplo: ::

  >>> from zope.interface import implements
  >>> from zope.component import adapts

  >>> class RegistradorHuespedNG(object):
  ...
  ...     implements(IRegistrador)
  ...     adapts(IHuesped)
  ...
  ...     def __init__(self, huesped):
  ...         self.huesped = huesped
  ...
  ...     def registrar(self):
  ...         huesped_id = obtener_proximo_id()
  ...         huespedes_db[huesped_id] = {
  ...         'nombre': huesped.nombre,
  ...         'lugar': huesped.lugar,
  ...         'telefono': huesped.telefono
  ...         }

  >>> pedro = Huesped("Pedro", "España")
  >>> pedro_registradorhuesped = RegistradorHuespedNG(pedro)

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()

  >>> gsm.registerAdapter(RegistradorHuespedNG, name='ng')

  >>> from zope.component import getAdapters
  >>> list(getAdapters((jack,), IRegistrador)) #doctest: +ELLIPSIS
  [(u'ng', <RegistradorHuespedNG object at ...>)]


getAllUtilitiesRegisteredFor
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Devuelve todos las utilidades registradas para una interfaz.  Este incluye 
utilidades sobrescritura.  El valor devuelto es un iterable de instancias 
de utilidad.

 - Ubicación: ``zope.component``

 - Firma: `getAllUtilitiesRegisteredFor(interface)`

Ejemplo: ::

  >>> from zope.interface import Interface
  >>> from zope.interface import implements

  >>> class ISaludador(Interface):
  ...     def saludar(nombre):
  ...         "decir hola"

  >>> class Saludador(object):
  ...
  ...     implements(ISaludador)
  ...
  ...     def saludar(self, nombre):
  ...         print "Hola", nombre

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()

  >>> saludar = Saludador()
  >>> gsm.registerUtility(saludar, ISaludador)

  >>> from zope.component import getAllUtilitiesRegisteredFor

  >>> getAllUtilitiesRegisteredFor(ISaludador) #doctest: +ELLIPSIS
  [<Saludador object at ...>]


getFactoriesFor
~~~~~~~~~~~~~~~

Devuelve una tupla(name, factory) de las fábricas registradas que crean 
objetos el cual implementa la interfaz dada.

 - Ubicación: ``zope.component``

 - Firma: `getFactoriesFor(interface, context=None)`

Ejemplo: ::

  >>> from zope.interface import Attribute
  >>> from zope.interface import Interface
  >>> from zope.interface import implements

  >>> class IBaseDatos(Interface):
  ...
  ...     def obtenerConexion():
  ...         """Devuelve el objeto conexion"""

  >>> class FakeDb(object):
  ...
  ...     implements(IBaseDatos)
  ...
  ...     def obtenerConexion(self):
  ...         return "conexion"

  >>> from zope.component.factory import Factory

  >>> fabrica = Factory(FakeDb, 'FakeDb')

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()

  >>> from zope.component.interfaces import IFactory
  >>> gsm.registerUtility(fabrica, IFactory, 'fakedb')

  >>> from zope.component import getFactoriesFor

  >>> list(getFactoriesFor(IBaseDatos))
  [(u'fakedb', <Factory for <class 'FakeDb'>>)]


getFactoryInterfaces
~~~~~~~~~~~~~~~~~~~~

Obtiene las interfaces implementada por una fábrica.  Busca la fábrica del 
nombre dado que esta cercano al contexto, y devuelve la interfaz 
o la tupla de la interfaz que las instancias objeto creadas por la named factory
se implementará.

 - Ubicación: ``zope.component``

 - Firma: `getFactoryInterfaces(name, context=None)`

Ejemplo: ::

  >>> from zope.interface import Attribute
  >>> from zope.interface import Interface
  >>> from zope.interface import implements

  >>> class IBaseDatos(Interface):
  ...
  ...     def obtenerConexion():
  ...         """Devuelve el objeto conexion"""

  >>> class FakeDb(object):
  ...
  ...     implements(IBaseDatos)
  ...
  ...     def obtenerConexion(self):
  ...         return "conexion"

  >>> from zope.component.factory import Factory

  >>> fabrica = Factory(FakeDb, 'FakeDb')

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()

  >>> from zope.component.interfaces import IFactory
  >>> gsm.registerUtility(fabrica, IFactory, 'fakedb')

  >>> from zope.component import getFactoryInterfaces

  >>> getFactoryInterfaces('fakedb')
  <implementedBy __builtin__.FakeDb>


getGlobalSiteManager
~~~~~~~~~~~~~~~~~~~~

Devuelve el global site manager.  Esta función nunca debería falla y 
siempre devuelve un objeto que provee `IGlobalSiteManager`

 - Ubicación: ``zope.component``

 - Firma: `getGlobalSiteManager()`

Ejemplo: ::

  >>> from zope.component import getGlobalSiteManager
  >>> from zope.component import globalSiteManager
  >>> gsm = getGlobalSiteManager()
  >>> gsm is globalSiteManager
  True


getMultiAdapter
~~~~~~~~~~~~~~~

Buscar un multi-adaptador a una interfaz para un objeto.  Devuelve un 
multi-adaptador que puede adaptar objetos a interfaz.  Si un coincidencia de búsqueda de 
adaptador no fue encontrado, lanzará un ``ComponentLookupError``.  El nombre 
consiste de una cadena vacía es reservada para adaptadores sin nombrar (unnamed). Los 
métodos adaptadores sin nombrar muy a menudo llaman a los métodos adaptadores nombrados con 
una cadena vacía por un nombre.

 - Ubicación: ``zope.component``

 - Firma: `getMultiAdapter(objects, interface=Interface, name='',
   context=None)`

 - Ver también: `queryMultiAdapter`_

Ejemplo: ::

  >>> from zope.interface import Interface
  >>> from zope.interface import implements
  >>> from zope.component import adapts

  >>> class IAdaptadoUno(Interface):
  ...     pass

  >>> class IAdaptadoDos(Interface):
  ...     pass

  >>> class IFuncionalidad(Interface):
  ...     pass

  >>> class MiFuncionalidad(object):
  ...     implements(IFuncionalidad)
  ...     adapts(IAdaptadoUno, IAdaptadoDos)
  ...
  ...     def __init__(self, uno, dos):
  ...         self.uno = uno
  ...         self.dos = dos

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()

  >>> gsm.registerAdapter(MiFuncionalidad)

  >>> class Uno(object):
  ...     implements(IAdaptadoUno)

  >>> class Dos(object):
  ...     implements(IAdaptadoDos)

  >>> uno = Uno()
  >>> dos = Dos()

  >>> from zope.component import getMultiAdapter

  >>> getMultiAdapter((uno,dos), IFuncionalidad) #doctest: +ELLIPSIS
  <MiFuncionalidad object at ...>

  >>> mifuncionalidad = getMultiAdapter((uno,dos), IFuncionalidad)
  >>> mifuncionalidad.uno #doctest: +ELLIPSIS
  <Uno object at ...>
  >>> mifuncionalidad.dos #doctest: +ELLIPSIS
  <Dos object at ...>


getSiteManager
~~~~~~~~~~~~~~

Obtiene los cercanos site manager en el contexto dado.  Si `context` es 
`None`, devuelve el global site manager.  Si el `context` no es 
`None`, es esperado que un adaptador desde el `context` a 
`IComponentLookup` pueda ser encontrado.  So no se encuentran adaptador, una 
excepción `ComponentLookupError` es lanzada.

 - Ubicación: ``zope.component``

 - Firma: `getSiteManager(context=None)`

Ejemplo 1::

  >>> from zope.component.globalregistry import BaseGlobalComponents
  >>> from zope.component import IComponentLookup
  >>> sm = BaseGlobalComponents()

  >>> class Context(object):
  ...     def __init__(self, sm):
  ...         self.sm = sm
  ...     def __conform__(self, interface):
  ...         if interface.isOrExtends(IComponentLookup):
  ...             return self.sm

  >>> context = Context(sm)

  >>> from zope.component import getSiteManager

  >>> lsm = getSiteManager(context)
  >>> lsm is sm
  True

Ejemplo 2: ::

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()

  >>> sm = getSiteManager()
  >>> gsm is sm
  True


getUtilitiesFor
~~~~~~~~~~~~~~~

Buscar las utilidades registradas que provee una interfaz.  Devuelve 
un iterable de pares utilidad-nombre.

 - Ubicación: ``zope.component``

 - Firma: `getUtilitiesFor(interface)`

Ejemplo: ::

  >>> from zope.interface import Interface
  >>> from zope.interface import implements

  >>> class ISaludador(Interface):
  ...     def saludar(nombre):
  ...         "decir hola"

  >>> class Saludador(object):
  ...
  ...     implements(ISaludador)
  ...
  ...     def saludar(self, nombre):
  ...         print "Hola", nombre

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()

  >>> saludar = Saludador()
  >>> gsm.registerUtility(saludar, ISaludador)

  >>> from zope.component import getUtilitiesFor

  >>> list(getUtilitiesFor(ISaludador)) #doctest: +ELLIPSIS
  [(u'', <Saludador object at ...>)]


getUtility
~~~~~~~~~~

Obtiene la utilidad que provee interfaz.  Devuelve la utilidad cercana 
al contexto que implementa la interfaz especificada.  Si uno no fue 
encontrado, lanza una excepción de error ``ComponentLookupError``.

 - Ubicación: ``zope.component``

 - Firma: `getUtility(interface, name='', context=None)`

Ejemplo: ::

  >>> from zope.interface import Interface
  >>> from zope.interface import implements

  >>> class ISaludador(Interface):
  ...     def saludar(nombre):
  ...         "decir hola"

  >>> class Saludador(object):
  ...
  ...     implements(ISaludador)
  ...
  ...     def saludar(self, nombre):
  ...         return "Hola" + nombre

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()

  >>> saludar = Saludador()
  >>> gsm.registerUtility(saludar, ISaludador)

  >>> from zope.component import getUtility

  >>> getUtility(ISaludador).saludar('Pedro')
  'Hola Pedro'


handle
~~~~~~

Llama a todos los manipuladores por los objetos dados.  Los manipuladores son 
fábricas de adaptadores de subscripción que no produce nada.  Ellos hacen 
todos sus trabajo cuando son llamadas.  Los manipuladores son típicamente usado para manipular 
eventos.

 - Ubicación: ``zope.component``

 - Firma: `handle(*objects)`

Ejemplo: ::

  >>> import datetime

  >>> def documentoCreado(evento):
  ...     evento.doc.creado = datetime.datetime.utcnow()

  >>> from zope.interface import Interface
  >>> from zope.interface import Attribute
  >>> from zope.interface import implements

  >>> class IDocumentoCreado(Interface):
  ...     doc = Attribute("El documento que fue creado")

  >>> class DocumentoCreado(object):
  ...     implements(IDocumentoCreado)
  ...
  ...     def __init__(self, doc):
  ...         self.doc = doc


  >>> def documentoCreado(evento):
  ...     evento.doc.creado = datetime.datetime.utcnow()

  >>> from zope.component import adapter

  >>> @adapter(IDocumentoCreado)
  ... def documentoCreado(evento):
  ...     evento.doc.creado = datetime.datetime.utcnow()


  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()

  >>> gsm.registerHandler(documentoCreado)

  >>> from zope.component import handle

  >>> handle(documentoCreado(doc))
  >>> doc.creado.__class__.__name__
  'datetime'


implementedBy
~~~~~~~~~~~~~

Devuelven las interfaces implementados para una instancia de clase.

 - Ubicación: ``zope.interface``

 - Firma: `implementedBy(class_)`

Ejemplo 1::

  >>> from zope.interface import Interface
  >>> from zope.interface import implements

  >>> class ISaludador(Interface):
  ...     def saludar(nombre):
  ...         "decir hola"

  >>> class Saludador(object):
  ...
  ...     implements(ISaludador)
  ...
  ...     def saludar(self, nombre):
  ...         print "Hola", nombre

  >>> from zope.interface import implementedBy
  >>> implementedBy(Saludador)
  <implementedBy __builtin__.Greeter>

Ejemplo 2: ::

  >>> from zope.interface import Attribute
  >>> from zope.interface import Interface
  >>> from zope.interface import implements

  >>> class IPersona(Interface):
  ...     nombre = Attribute("Nombre de persona")

  >>> class IEspecial(Interface):
  ...     pass

  >>> class Persona(object):
  ...     implements(IPersona)
  ...     nombre = u""

  >>> from zope.interface import classImplements
  >>> classImplements(Person, IEspecial)

  >>> from zope.interface import implementedBy

  Obtener una lista de todas las interfaces implementadas por esa clase: ::

  >>> [x.__name__ for x in implementedBy(Persona)]
  ['IPersona', 'IEspecial']


implementer
~~~~~~~~~~~

Crea un decorador para declarar interfaces implementadas por una fábrica.
Un llamable es devuelto eso hace una declaración de implementación en los objetos 
pasados a ese.

 - Ubicación: ``zope.interface``

 - Firma: `implementer(*interfaces)`

Ejemplo: ::

  >>> from zope.interface import implementer
  >>> class IPrueba(Interface):
  ...     pass
  >>> class Prueba(object):
  ...     implements(IPrueba)

  >>> @implementer(IPrueba)
  ... def creadorprueba():
  ...     prueba = Prueba()
  ...     return prueba
  >>> list(implementedBy(creadorprueba))
  [<InterfaceClass __builtin__.IPrueba>]


implements
~~~~~~~~~~

Declara interfaces implementadas por instancias de una clase. Esta función es llamada en una definición de clase.  Los argumentos son uno o más 
interfaces.  Las interfaces dadas son agregadas a cualquier interfaces
previamente declaradas.  Las declaraciones previas incluye declaraciones para 
clases base a menos que se allá usado ``implementsOnly``.

 - Ubicación: ``zope.interface``

 - Firma: `implements(*interfaces)`

Ejemplo: ::

  >>> from zope.interface import Attribute
  >>> from zope.interface import Interface
  >>> from zope.interface import implements

  >>> class IPersona(Interface):
  ...
  ...     nombre = Attribute("Nombre de persona")

  >>> class Persona(object):
  ...
  ...     implements(IPersona)
  ...     nombre = u""

  >>> pedro = Persona()
  >>> pedro.nombre = "Pedro"

  Usted puede probar con esto: ::

  >>> from zope.interface import providedBy
  >>> IPersona in providedBy(pedro)
  True


implementsOnly
~~~~~~~~~~~~~~

Declara solamente interfaces implementadas por instancias de una clase.  Esta 
función es llamada en una definición de clase.  Los argumentos son uno o 
más interfaces.  Las declaraciones previas incluye declaraciones para 
clases base que son sobrescritas.

 - Ubicación: ``zope.interface``

 - Firma: `implementsOnly(*interfaces)`

Ejemplo: ::

  >>> from zope.interface import Attribute
  >>> from zope.interface import Interface
  >>> from zope.interface import implements
  >>> from zope.interface import implementsOnly

  >>> class IPersona(Interface):
  ...
  ...     nombre = Attribute("Nombre de persona")

  >>> class IEstudiante(Interface):
  ...
  ...     colegio = Attribute("Nombre de colegio")

  >>> class Persona(object):
  ...
  ...     implements(IPersona)
  ...     nombre = u""

  >>> class NuevaPersona(Persona):
  ...     implementsOnly(IEstudiante)
  ...     colegio = u""

  >>> pedro = NuevaPersona()
  >>> pedro.colegio = "Nuevo Colegio"

  Usted puede probar con esto: ::

  >>> from zope.interface import providedBy
  >>> IPersona in providedBy(pedro)
  False
  >>> IEstudiante in providedBy(pedro)
  True


Interface
~~~~~~~~~

Usando esta clase, usted puede definir una interfaz.  To define an
interface, just inherit from ``Interface`` class.

 - Ubicación: ``zope.interface``

 - Firma: `Interface(name, doc='')`

Ejemplo 1::

  >>> from zope.interface import Attribute
  >>> from zope.interface import Interface

  >>> class IPersona(Interface):
  ...
  ...     nombre = Attribute("Nombre de persona")
  ...     email = Attribute("Direccion de email")


Ejemplo 2: ::

  >>> from zope.interface import Interface

  >>> class IAnfitrion(Interface):
  ...
  ...     def buenosdias(huesped):
  ...         """Le dice buenos días al huesped"""


moduleProvides
~~~~~~~~~~~~~~

Declara interfaces proveídas por un módulo.  Esta función es usada en una 
definición de módulo.  Los argumentos son uno o más interfaces.  Las 
interfaces dadas son usadas para crear la especificación de la interfaz del direct-object 
del modulo.  Un error será lazado si el módulo 
ya tiene una especificación de interfaz.  En otras palabras, es es un 
error para llamar a esta función más que una vez en una definición módulo.

Esta función es proveída por conveniencia.  Eso provee una más 
conveniente forma de llamar ``directlyProvides`` para un módulo.

 - Ubicación: ``zope.interface``

 - Firma: `moduleProvides(*interfaces)`

 - Ver también: `directlyProvides`_

Usted puede ver un ejemplo usado en el código fuente `zope.component` en si mismo.  El archivo 
`__init__.py` tiene una sentencia como esta: ::

  moduleProvides(IComponentArchitecture,
                 IComponentRegistrationConvenience)

Entonces, el `zope.component` provee dos interfaces:
`IComponentArchitecture` y `IComponentRegistrationConvenience`.


noLongerProvides
~~~~~~~~~~~~~~~~

Remueve una interfaz desde la lista de un directiva proveída de las interfaces 
de objeto.

 - Ubicación: ``zope.interface``

 - Firma: `noLongerProvides(object, interface)`

Ejemplo: ::

  >>> from zope.interface import Attribute
  >>> from zope.interface import Interface
  >>> from zope.interface import implements
  >>> from zope.interface import classImplements

  >>> class IPersona(Interface):
  ...
  ...     nombre = Attribute("Nombre de persona")

  >>> class IEstudiante(Interface):
  ...
  ...     colegio = Attribute("Nombre de colegio")

  >>> class Persona(object):
  ...
  ...     implements(IPersona)
  ...     nombre = u""

  >>> pedro = Persona()
  >>> pedro.nombre = "Pedro"
  >>> pedro.colegio = "Nuevo Colegio"
  >>> directlyProvides(pedro, IEstudiante)

  Usted puede probar con esto: ::

  >>> from zope.interface import providedBy
  >>> IPersona in providedBy(pedro)
  True
  >>> IEstudiante in providedBy(pedro)
  True
  >>> from zope.interface import noLongerProvides
  >>> noLongerProvides(pedro, IEstudiante)
  >>> IPersona in providedBy(pedro)
  True
  >>> IEstudiante in providedBy(pedro)
  False


provideAdapter
~~~~~~~~~~~~~~

Ese es recomendado para usar `registerAdapter`_ .


provideHandler
~~~~~~~~~~~~~~

Ese es recomendado para usar `registerHandler`_ .


provideSubscriptionAdapter
~~~~~~~~~~~~~~~~~~~~~~~~~~

Ese es recomendado para usar `registerSubscriptionAdapter`_ .


provideUtility
~~~~~~~~~~~~~~

Ese es recomendado para usar `registerUtility`_ .


providedBy
~~~~~~~~~~

Probar si la interfaz esta implementada por el objeto.  Devuelve True 
si el objeto afirma que implementa la interfaz, incluyendo 
incluyendo afirmando que implementa una interfaz extendida.

 - Ubicación: ``zope.interface``

 - Firma: `providedBy(object)`

Ejemplo 1::

  >>> from zope.interface import Attribute
  >>> from zope.interface import Interface
  >>> from zope.interface import implements

  >>> class IPersona(Interface):
  ...
  ...     nombre = Attribute("Nombre de persona")

  >>> class Persona(object):
  ...
  ...     implements(IPersona)
  ...     nombre = u""

  >>> pedro = Persona()
  >>> pedro.nombre = "Pedro"

  Usted puede probar con esto: ::

  >>> from zope.interface import providedBy
  >>> IPersona in providedBy(pedro)
  True

Ejemplo 2: ::

  >>> from zope.interface import Attribute
  >>> from zope.interface import Interface
  >>> from zope.interface import implements

  >>> class IPersona(Interface):
  ...     nombre = Attribute("Nombre de persona")

  >>> class IEspecial(Interface):
  ...     pass

  >>> class Persona(object):
  ...     implements(IPersona)
  ...     nombre = u""

  >>> from zope.interface import classImplements
  >>> classImplements(Person, IEspecial)
  >>> from zope.interface import providedBy
  >>> pedro = Persona()
  >>> pedro.nombre = "Pedro"

  Para obtener un listado de todas interfaces proveídas por ese objeto: ::

  >>> [x.__name__ for x in providedBy(pedro)]
  ['IPersona', 'IEspecial']


queryAdapter
~~~~~~~~~~~~

Buscar un adaptador nombrado a una interfaz para un objeto.  Devuelve un 
adaptador que puede adaptar un objeto a una interfaz.  Si un coincidencia de búsqueda de 
adaptador no fue encontrado, devuelve el predeterminado. 


 - Ubicación: ``zope.component``

 - Firma: `queryAdapter(object, interface=Interface, name=u'',
   default=None, context=None)`

Ejemplo: ::

  >>> from zope.interface import Attribute
  >>> from zope.interface import Interface

  >>> class IRegistrador(Interface):
  ...     """Un registrador registrará los detalles de un objeto"""
  ...
  ...     def registrar():
  ...         """Registrar detalles de un objeto"""
  ...

  >>> from zope.interface import implements
  >>> from zope.component import adapts

  >>> class RegistradorHuespedNG(object):
  ...
  ...     implements(IRegistrador)
  ...     adapts(IHuesped)
  ...
  ...     def __init__(self, huesped):
  ...         self.huesped = huesped
  ...
  ...     def registrar(self):
  ...         huesped_id = obtener_proximo_id()
  ...         huespedes_db[huesped_id] = {
  ...         'nombre': huesped.nombre,
  ...         'lugar': huesped.lugar,
  ...         'telefono': huesped.telefono
  ...         }

  >>> class Huesped(object):
  ...
  ...     implements(IHuesped)
  ...
  ...     def __init__(self, nombre, lugar):
  ...         self.nombre = nombre
  ...         self.lugar = lugar

  >>> pedro = Huesped("Pedro", "España")
  >>> pedro_registradorhuesped = RegistradorHuespedNG(pedro)

  >>> IRegistrador.providedBy(pedro_registradorhuesped)
  True

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()
  >>> gsm.registerAdapter(RegistradorHuespedNG,
  ...                     (IHuesped,), IRegistrador, 'ng')

  >>> queryAdapter(pedro, IRegistrador, 'ng') #doctest: +ELLIPSIS
  <RegistradorHuespedNG object at ...>


queryAdapterInContext
~~~~~~~~~~~~~~~~~~~~~

Buscar un especial adaptador a una interfaz para un objeto.

.. note:: 
    Este método sólo debe utilizarse si un contexto personalizado tiene que ser
    previsto para proporcionar búsqueda del componente personalizado. De los contrario, llama la 
    interfaz, como en: ::

      interface(object, default)

Devuelve un adaptador que puede adaptar un objeto a una interfaz.  Si una coincidencia de búsqueda del 
adaptador no fue encontrado, devuelve el predeterminado.

Contexto se adapta a IServiceService, y estos adaptadores de servicio 
de adaptador es usado.

Si el objeto tiene un método __conform__, será llamado a este método
con la interfaz requerido.  Si el método devuelva un valor non-None 
ese valor será devuelto. De lo contrario, si el objeto ya 
implementa la interfaz, el objeto será devuelto.

 - Ubicación: ``zope.component``

 - Firma: `queryAdapterInContext(object, interface, context,
   default=None)`

 - Ver también: `getAdapterInContext`_

Ejemplo: ::

  >>> from zope.component.globalregistry import BaseGlobalComponents
  >>> from zope.component import IComponentLookup
  >>> sm = BaseGlobalComponents()

  >>> class Context(object):
  ...     def __init__(self, sm):
  ...         self.sm = sm
  ...     def __conform__(self, interface):
  ...         if interface.isOrExtends(IComponentLookup):
  ...             return self.sm

  >>> context = Context(sm)

  >>> from zope.interface import Attribute
  >>> from zope.interface import Interface

  >>> class IRegistrador(Interface):
  ...     """Un registrador registrará los detalles de un objeto"""
  ...
  ...     def registrar():
  ...         """Registrar detalles de un objeto"""
  ...

  >>> from zope.interface import implements
  >>> from zope.component import adapts

  >>> class RegistradorHuespedNG(object):
  ...
  ...     implements(IRegistrador)
  ...     adapts(IHuesped)
  ...
  ...     def __init__(self, huesped):
  ...         self.huesped = huesped
  ...
  ...     def registrar(self):
  ...         huesped_id = obtener_proximo_id()
  ...         huespedes_db[huesped_id] = {
  ...         'nombre': huesped.nombre,
  ...         'lugar': huesped.lugar,
  ...         'telefono': huesped.telefono
  ...         }

  >>> class Huesped(object):
  ...
  ...     implements(IHuesped)
  ...
  ...     def __init__(self, nombre, lugar):
  ...         self.nombre = nombre
  ...         self.lugar = lugar

  >>> pedro = Huesped("Pedro", "España")
  >>> pedro_registradorhuesped = RegistradorHuespedNG(pedro)

  >>> IRegistrador.providedBy(pedro_registradorhuesped)
  True

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()
  >>> sm.registerAdapter(RegistradorHuespedNG,
  ...                     (IHuesped,), IRegistrador)

  >>> from zope.component import queryAdapterInContext

  >>> queryAdapterInContext(pedro, IRegistrador, sm) #doctest: +ELLIPSIS
  <RegistradorHuespedNG object at ...>


queryMultiAdapter
~~~~~~~~~~~~~~~~~

Buscar un multi-adaptador a una interfaz para objetos.  Devuelve un 
multi-adaptador que puede adaptar objetos a interfaz.  Si una coincidencia de búsqueda del 
adaptador no fue encontrado, devuelve el predeterminado.  El nombre consiste de 
una cadena vacía es reservada para adaptadores sin nombrar (unnamed).  Los métodos adaptadores 
sin nombrar muy a menudo llaman al método adaptador nombrado con 
una cadena vacía por un nombre.

 - Ubicación: ``zope.component``

 - Firma: `queryMultiAdapter(objects, interface=Interface,
   name=u'', default=None, context=None)`

 - Ver también: `getMultiAdapter`_

Ejemplo: ::

  >>> from zope.interface import Interface
  >>> from zope.interface import implements
  >>> from zope.component import adapts

  >>> class IAdaptadoUno(Interface):
  ...     pass

  >>> class IAdaptadoDos(Interface):
  ...     pass

  >>> class IFuncionalidad(Interface):
  ...     pass

  >>> class MiFuncionalidad(object):
  ...     implements(IFuncionalidad)
  ...     adapts(IAdaptadoUno, IAdaptadoDos)
  ...
  ...     def __init__(self, uno, dos):
  ...         self.uno = uno
  ...         self.dos = dos

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()

  >>> gsm.registerAdapter(MiFuncionalidad)

  >>> class Uno(object):
  ...     implements(IAdaptadoUno)

  >>> class Dos(object):
  ...     implements(IAdaptadoDos)

  >>> uno = Uno()
  >>> dos = Dos()

  >>> from zope.component import queryMultiAdapter

  >>> getMultiAdapter((uno,dos), IFuncionalidad) #doctest: +ELLIPSIS
  <MiFuncionalidad object at ...>

  >>> myfunctionality = queryMultiAdapter((uno,dos), IFuncionalidad)
  >>> mifuncionalidad.uno #doctest: +ELLIPSIS
  <Uno object at ...>
  >>> mifuncionalidad.dos #doctest: +ELLIPSIS
  <Dos object at ...>


queryUtility
~~~~~~~~~~~~

Esta función es usada  para buscar una utilidad que provee una interfaz.
If one is not found, returns default. Si uno no fue encontrado, devuelve por defecto.

 - Ubicación: ``zope.component``

 - Firma: `queryUtility(interface, name='', default=None)`

Ejemplo: ::

  >>> from zope.interface import Interface
  >>> from zope.interface import implements

  >>> class ISaludador(Interface):
  ...     def saludar(nombre):
  ...         "decir hola"

  >>> class Saludador(object):
  ...
  ...     implements(ISaludador)
  ...
  ...     def saludar(self, nombre):
  ...         return "Hola" + nombre

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()

  >>> saludar = Saludador()
  >>> gsm.registerUtility(saludar, ISaludador)

  >>> from zope.component import queryUtility

  >>> queryUtility(ISaludador).saludar('Pedro')
  'Hola Pedro'


registerAdapter
~~~~~~~~~~~~~~~

Esta función es usado para registrar una fábrica adaptador.

 - Ubicación: ``zope.component - IComponentRegistry``

 - Firma: `registerAdapter(factory, required=None, provided=None,
   name=u'', info=u'')`

 - Ver también: `unregisterAdapter`_

Ejemplo: ::

  >>> from zope.interface import Attribute
  >>> from zope.interface import Interface

  >>> class IRegistrador(Interface):
  ...     """Un registrador registrará los detalles de un objeto"""
  ...
  ...     def registrar():
  ...         """Registrar detalles de un objeto"""
  ...

  >>> from zope.interface import implements
  >>> from zope.component import adapts

  >>> class RegistradorHuespedNG(object):
  ...
  ...     implements(IRegistrador)
  ...     adapts(IHuesped)
  ...
  ...     def __init__(self, huesped):
  ...         self.huesped = huesped
  ...
  ...     def registrar(self):
  ...         huesped_id = obtener_proximo_id()
  ...         huespedes_db[huesped_id] = {
  ...         'nombre': huesped.nombre,
  ...         'lugar': huesped.lugar,
  ...         'telefono': huesped.telefono
  ...         }

  >>> class Huesped(object):
  ...
  ...     implements(IHuesped)
  ...
  ...     def __init__(self, nombre, lugar):
  ...         self.nombre = nombre
  ...         self.lugar = lugar

  >>> pedro = Huesped("Pedro", "España")
  >>> pedro_registradorhuesped = RegistradorHuespedNG(pedro)

  >>> IRegistrador.providedBy(pedro_registradorhuesped)
  True

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()
  >>> gsm.registerAdapter(RegistradorHuespedNG,
  ...                     (IHuesped,), IRegistrador, 'ng')

  Usted puede probar con esto: ::

  >>> queryAdapter(pedro, IRegistrador, 'ng') #doctest: +ELLIPSIS
  <RegistradorHuespedNG object at ...>


registeredAdapters
~~~~~~~~~~~~~~~~~~

Devuelve un iterable de `IAdapterRegistrations`.  Estos registros 
describe los registros actual del adaptador en el objeto.

 - Ubicación: ``zope.component - IComponentRegistry``

 - Firma: `registeredAdapters()`

Ejemplo: ::

  >>> from zope.interface import Attribute
  >>> from zope.interface import Interface

  >>> class IRegistrador(Interface):
  ...     """Un registrador registrará los detalles de un objeto"""
  ...
  ...     def registrar():
  ...         """Registrar detalles de un objeto"""
  ...

  >>> from zope.interface import implements
  >>> from zope.component import adapts

  >>> class RegistradorHuespedNG(object):
  ...
  ...     implements(IRegistrador)
  ...     adapts(IHuesped)
  ...
  ...     def __init__(self, huesped):
  ...         self.huesped = huesped
  ...
  ...     def registrar(self):
  ...         huesped_id = obtener_proximo_id()
  ...         huespedes_db[huesped_id] = {
  ...         'nombre': huesped.nombre,
  ...         'lugar': huesped.lugar,
  ...         'telefono': huesped.telefono
  ...         }

  >>> class Huesped(object):
  ...
  ...     implements(IHuesped)
  ...
  ...     def __init__(self, nombre, lugar):
  ...         self.nombre = nombre
  ...         self.lugar = lugar

  >>> pedro = Huesped("Pedro", "España")
  >>> pedro_registradorhuesped = RegistradorHuespedNG(pedro)

  >>> IRegistrador.providedBy(pedro_registradorhuesped)
  True

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()
  >>> gsm.registerAdapter(RegistradorHuespedNG,
  ...                     (IHuesped,), IRegistrador, 'ng2')


  >>> reg_adapter = list(gsm.registeredAdapters())
  >>> 'ng2' in [x.name for x in reg_adapter]
  True


registeredHandlers
~~~~~~~~~~~~~~~~~~

Devuelve un iterable de `IHandlerRegistrations`.  Estos registros 
describe los registros actual del manipulador en el objeto.

 - Ubicación: ``zope.component - IComponentRegistry``

 - Firma: `registeredHandlers()`

Ejemplo: ::

  >>> import datetime

  >>> def documentoCreado(evento):
  ...     evento.doc.creado = datetime.datetime.utcnow()

  >>> from zope.interface import Interface
  >>> from zope.interface import Attribute
  >>> from zope.interface import implements

  >>> class IDocumentoCreado(Interface):
  ...     doc = Attribute("El documento que fue creado")

  >>> class DocumentoCreado(object):
  ...     implements(IDocumentoCreado)
  ...
  ...     def __init__(self, doc):
  ...         self.doc = doc


  >>> def documentoCreado(evento):
  ...     evento.doc.creado = datetime.datetime.utcnow()

  >>> from zope.component import adapter

  >>> @adapter(IDocumentoCreado)
  ... def documentoCreado(evento):
  ...     evento.doc.creado = datetime.datetime.utcnow()


  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()

  >>> gsm.registerHandler(documentoCreado, info='ng3')

  >>> reg_adapter = list(gsm.registeredHandlers())
  >>> 'ng3' in [x.info for x in reg_adapter]
  True

  >>> gsm.registerHandler(documentoCreado, name='ng4')
  Traceback (most recent call last):
  ...
  TypeError: Named handlers are not yet supported


registeredSubscriptionAdapters
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Devuelve un iterable de `ISubscriptionAdapterRegistrations`.  Estos 
registros describe la subscripción actual del adaptador en el objeto.

 - Ubicación: ``zope.component - IComponentRegistry``

 - Firma: `registeredSubscriptionAdapters()`

Ejemplo: ::

  >>> from zope.interface import Interface
  >>> from zope.interface import Attribute
  >>> from zope.interface import implements

  >>> class IValidar(Interface):
  ...     def validar(ob):
  ...         """Determine si el objeto es valido
  ...
  ...         Devuelve una cadena describiendo un problema de validación.
  ...         Una cadena vacía es devuelta a indicar que el 
  ...         objeto es valido.
  ...         """

  >>> class IDocumento(Interface):
  ...     resumen = Attribute("Resumen del Documento")
  ...     cuerpo = Attribute("Texto del Documento")

  >>> class Documento(object):
  ...     implements(IDocumento)
  ...     def __init__(self, resumen, cuerpo):
  ...         self.resumen, self.cuerpo = resumen, cuerpo

  >>> from zope.component import adapts

  >>> class LongitudAdecuada(object):
  ...
  ...     adapts(IDocumento)
  ...     implements(IValidar)
  ...
  ...     def __init__(self, doc):
  ...         self.doc = doc
  ...
  ...     def validar(self):
  ...         if len(self.doc.cuerpo) < 1000:
  ...             return 'el cuerpo del documento es muy corto'
  ...         else:
  ...             return ''

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()

  >>> gsm.registerSubscriptionAdapter(LongitudAdecuada, info='ng4')

  >>> reg_adapter = list(gsm.registeredSubscriptionAdapters())
  >>> 'ng4' in [x.info for x in reg_adapter]
  True


registeredUtilities
~~~~~~~~~~~~~~~~~~~

Esta función devuelve un iterable de`IUtilityRegistrations`.  Estos 
registros describe los registros de la utilidad actual en el 
objeto.

 - Ubicación: ``zope.component - IComponentRegistry``

 - Firma: `registeredUtilities()`

Ejemplo: ::

  >>> from zope.interface import Interface
  >>> from zope.interface import implements

  >>> class ISaludador(Interface):
  ...     def saludar(nombre):
  ...         "decir hola"

  >>> class Saludador(object):
  ...
  ...     implements(ISaludador)
  ...
  ...     def saludar(self, nombre):
  ...         print "Hola", nombre

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()

  >>> saludar = Saludador()
  >>> gsm.registerUtility(saludar, info='ng5')

  >>> reg_adapter = list(gsm.registeredUtilities())
  >>> 'ng5' in [x.info for x in reg_adapter]
  True


registerHandler
~~~~~~~~~~~~~~~

Esta función es usado para registrar un manipulador.  Un manipulador es un 
suscriptor que no computa un adaptador pero realiza alguna función 
cuando se le llama.

 - Ubicación: ``zope.component - IComponentRegistry``

 - Firma: `registerHandler(handler, required=None, name=u'', info='')`

 - Ver también: `unregisterHandler`_

.. note:: 
    En la implementación actual del paquete ``zope.component`` no soporta el atributo `name`.

Ejemplo: ::

  >>> import datetime

  >>> def documentoCreado(evento):
  ...     evento.doc.creado = datetime.datetime.utcnow()

  >>> from zope.interface import Interface
  >>> from zope.interface import Attribute
  >>> from zope.interface import implements

  >>> class IDocumentoCreado(Interface):
  ...     doc = Attribute("El documento que fue creado")

  >>> class DocumentoCreado(object):
  ...     implements(IDocumentoCreado)
  ...
  ...     def __init__(self, doc):
  ...         self.doc = doc


  >>> def documentoCreado(evento):
  ...     evento.doc.creado = datetime.datetime.utcnow()

  >>> from zope.component import adapter

  >>> @adapter(IDocumentoCreado)
  ... def documentoCreado(evento):
  ...     evento.doc.creado = datetime.datetime.utcnow()


  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()

  >>> gsm.registerHandler(documentoCreado)

  >>> from zope.component import handle

  >>> handle(documentoCreado(doc))
  >>> doc.creado.__class__.__name__
  'datetime'


registerSubscriptionAdapter
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Esta función se utiliza para registrar una fábrica suscriptor.

 - Ubicación: ``zope.component - IComponentRegistry``

 - Firma: `registerSubscriptionAdapter(factory, required=None,
   provides=None, name=u'', info='')`

 - Ver también: `unregisterSubscriptionAdapter`_

Ejemplo: ::

  >>> from zope.interface import Interface
  >>> from zope.interface import Attribute
  >>> from zope.interface import implements

  >>> class IValidar(Interface):
  ...     def validar(ob):
  ...         """Determine si el objeto es valido
  ...
  ...         Devuelve una cadena describiendo un problema de validación.
  ...         Una cadena vacía es devuelta a indicar que el 
  ...         objeto es valido.
  ...         """

  >>> class IDocumento(Interface):
  ...     resumen = Attribute("Resumen del Documento")
  ...     cuerpo = Attribute("Texto del Documento")

  >>> class Documento(object):
  ...     implements(IDocumento)
  ...     def __init__(self, resumen, cuerpo):
  ...         self.resumen, self.cuerpo = resumen, cuerpo

  >>> from zope.component import adapts

  >>> class LongitudAdecuada(object):
  ...
  ...     adapts(IDocumento)
  ...     implements(IValidar)
  ...
  ...     def __init__(self, doc):
  ...         self.doc = doc
  ...
  ...     def validar(self):
  ...         if len(self.doc.cuerpo) < 1000:
  ...             return 'el cuerpo del documento es muy corto'
  ...         else:
  ...             return ''

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()

  >>> gsm.registerSubscriptionAdapter(LongitudAdecuada)


registerUtility
~~~~~~~~~~~~~~~

Esta función es usado para registrar una utilidad.

 - Ubicación: ``zope.component - IComponentRegistry``

 - Firma: `registerUtility(component, provided=None, name=u'',
   info=u'')`

 - Ver también: `unregisterUtility`_

Ejemplo: ::

  >>> from zope.interface import Interface
  >>> from zope.interface import implements

  >>> class ISaludador(Interface):
  ...     def saludar(nombre):
  ...         "decir hola"

  >>> class Saludador(object):
  ...
  ...     implements(ISaludador)
  ...
  ...     def saludar(self, nombre):
  ...         print "Hola", nombre

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()

  >>> saludar = Saludador()
  >>> gsm.registerUtility(saludar)


subscribers
~~~~~~~~~~~

Esta función es usado para obtener subscriptores.  Los suscriptores se devuelven 
que proporcionan la interfaz proveída y que dependen y son 
calculado a partir de la secuencia de los objetos requeridos.

 - Ubicación: ``zope.component - IComponentRegistry``

 - Firma: `subscribers(required, provided, context=None)`

Ejemplo: ::

  >>> from zope.interface import Interface
  >>> from zope.interface import Attribute
  >>> from zope.interface import implements

  >>> class IValidar(Interface):
  ...     def validar(ob):
  ...         """Determine si el objeto es valido
  ...
  ...         Devuelve una cadena describiendo un problema de validación.
  ...         Una cadena vacía es devuelta a indicar que el 
  ...         objeto es valido.
  ...         """

  >>> class IDocumento(Interface):
  ...     resumen = Attribute("Resumen del Documento")
  ...     cuerpo = Attribute("Texto del Documento")

  >>> class Documento(object):
  ...     implements(IDocumento)
  ...     def __init__(self, resumen, cuerpo):
  ...         self.resumen, self.cuerpo = resumen, cuerpo

  >>> from zope.component import adapts

  >>> class ResumenLineaSimple:
  ...     adapts(IDocumento)
  ...     implements(IValidar)
  ...
  ...     def __init__(self, doc):
  ...         self.doc = doc
  ...
  ...     def validar(self):
  ...         if '\n' in self.doc.resumen:
  ...             return 'El resumen debe solamente tener una linea'
  ...         else:
  ...             return ''

  >>> class LongitudAdecuada(object):
  ...     adapts(IDocumento)
  ...     implements(IValidar)
  ...
  ...     def __init__(self, doc):
  ...         self.doc = doc
  ...
  ...     def validar(self):
  ...         if len(self.doc.cuerpo) < 1000:
  ...             return 'el cuerpo del documento es muy corto'
  ...         else:
  ...             return ''

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()

  >>> gsm.registerSubscriptionAdapter(ResumenLineaSimple)
  >>> gsm.registerSubscriptionAdapter(LongitudAdecuada)

  >>> from zope.component import subscribers

  >>> doc = Documento("Un\nDocumento", "blah")
  >>> [adaptador.validar()
  ...  for adaptador in subscribers([doc], IValidar)
  ...  if adaptador.validar()]
  ['El resumen debe solamente tener una linea', 'El cuerpo del documento es muy corto']

  >>> doc = Documento("Un\nDocumento", "blah" * 1000)
  >>> [adaptador.validar()
  ...  for adaptador in subscribers([doc], IValidar)
  ...  if adaptador.validar()]
  ['El resumen debe solamente tener una linea']

  >>> doc = Documento("Un Documento", "blah")
  >>> [adaptador.validar()
  ...  for adaptador in subscribers([doc], IValidar)
  ...  if adaptador.validar()]
  ['El cuerpo del documento es muy corto']


unregisterAdapter
~~~~~~~~~~~~~~~~~

Esta función es usado para quitar registro una fábrica adaptador.  Un booleano es 
devuelto indicando si el registro fue cambiando.  Si el componente 
dado es None y allí no hay componente registrado, o si el 
componente dado no es None y no esta registrado, entonces la función
devuelve False, de lo contrario ese devuelve True.

 - Ubicación: ``zope.component - IComponentRegistry``

 - Firma: `unregisterAdapter(factory=None, required=None,
   provided=None, name=u'')`

 - Ver también: `registerAdapter`_

Ejemplo: ::

  >>> from zope.interface import Attribute
  >>> from zope.interface import Interface

  >>> class IRegistrador(Interface):
  ...     """Un registrador registrará los detalles de un objeto"""
  ...
  ...     def registrar():
  ...         """Registrar detalles de un objeto"""
  ...

  >>> from zope.interface import implements
  >>> from zope.component import adapts

  >>> class RegistradorHuespedNG(object):
  ...
  ...     implements(IRegistrador)
  ...     adapts(IHuesped)
  ...
  ...     def __init__(self, huesped):
  ...         self.huesped = huesped
  ...
  ...     def registrar(self):
  ...         huesped_id = obtener_proximo_id()
  ...         huespedes_db[huesped_id] = {
  ...         'nombre': huesped.nombre,
  ...         'lugar': huesped.lugar,
  ...         'telefono': huesped.telefono
  ...         }

  >>> class Huesped(object):
  ...
  ...     implements(IHuesped)
  ...
  ...     def __init__(self, nombre, lugar):
  ...         self.nombre = nombre
  ...         self.lugar = lugar

  >>> pedro = Huesped("Pedro", "España")
  >>> pedro_registradorhuesped = RegistradorHuespedNG(pedro)

  >>> IRegistrador.providedBy(pedro_registradorhuesped)
  True

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()
  >>> gsm.registerAdapter(RegistradorHuespedNG,
  ...                     (IHuesped,), IRegistrador, 'ng6')

  Usted puede probar con esto: ::

  >>> queryAdapter(pedro, IRegistrador, 'ng6') #doctest: +ELLIPSIS
  <RegistradorHuespedNG object at ...>

  Ahora quite el registro: ::

  >>> gsm.unregisterAdapter(RegistradorHuespedNG, name='ng6')
  True

  Después de quitar el registro: ::

  >>> print queryAdapter(pedro, IRegistrador, 'ng6')
  None


unregisterHandler
~~~~~~~~~~~~~~~~~

Esta función es usado para quitar registro un manipulador.  Un manipulador es un 
suscriptor que no computa un adaptador pero realiza alguna función 
cuando se le llama.  Un booleano es devuelto indicando si el registro fue cambiando.

 - Ubicación: ``zope.component - IComponentRegistry``

 - Firma: `unregisterHandler(handler=None, required=None,
   name=u'')`

 - Ver también: `registerHandler`_

Ejemplo: ::

  >>> from zope.interface import Interface
  >>> from zope.interface import Attribute
  >>> from zope.interface import implements

  >>> class IDocumento(Interface):
  ...
  ...     resumen = Attribute("Resumen del Documento")
  ...     cuerpo = Attribute("Texto del Documento")

  >>> class Documento(object):
  ...
  ...     implements(IDocumento)
  ...     def __init__(self, resumen, cuerpo):
  ...         self.resumen, self.cuerpo = resumen, cuerpo

  >>> doc = Documento("Un\nDocumento", "blah")

  >>> class IDocumentoConsultado(Interface):
  ...     doc = Attribute("El documento que fue accesado")

  >>> class DocumentoConsultado(object):
  ...     implements(IDocumentoConsultado)
  ...
  ...     def __init__(self, doc):
  ...         self.doc = doc
  ...         self.doc.count = 0

  >>> from zope.component import adapter

  >>> @adapter(IDocumentAccessed)
  ... def documentAccessed(event):
  ...     event.doc.count = event.doc.count + 1

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()

  >>> gsm.registerHandler(documentAccessed)

  >>> from zope.component import handle

  >>> handle(DocumentAccessed(doc))
  >>> doc.count
  1

  Ahora quite el registro: ::

  >>> gsm.unregisterHandler(documentAccessed)
  True

  Después de quitar el registro: ::

  >>> handle(DocumentAccessed(doc))
  >>> doc.count
  0


unregisterSubscriptionAdapter
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Esta función se utiliza para quitar registro a una fábrica suscriptor.  Un booleano 
es devuelto indicando si el registro fue cambiando.  Si el componente 
dado es None y allí no hay componente registrado, o si el 
componente dado no es None y no esta registrado, entonces la función
devuelve False, de lo contrario ese devuelve True.

 - Ubicación: ``zope.component - IComponentRegistry``

 - Firma: `unregisterSubscriptionAdapter(factory=None,
   required=None, provides=None, name=u'')`

 - Ver también: `registerSubscriptionAdapter`_

Ejemplo: ::

  >>> from zope.interface import Interface
  >>> from zope.interface import Attribute
  >>> from zope.interface import implements

  >>> class IValidar(Interface):
  ...     def validar(ob):
  ...         """Determine si el objeto es valido
  ...
  ...         Devuelve una cadena describiendo un problema de validación.
  ...         Una cadena vacía es devuelta a indicar que el 
  ...         objeto es valido.
  ...         """

  >>> class IDocumento(Interface):
  ...     resumen = Attribute("Resumen del Documento")
  ...     cuerpo = Attribute("Texto del Documento")

  >>> class Documento(object):
  ...     implements(IDocumento)
  ...     def __init__(self, resumen, cuerpo):
  ...         self.resumen, self.cuerpo = resumen, cuerpo

  >>> from zope.component import adapts

  >>> class LongitudAdecuada(object):
  ...
  ...     adapts(IDocumento)
  ...     implements(IValidar)
  ...
  ...     def __init__(self, doc):
  ...         self.doc = doc
  ...
  ...     def validar(self):
  ...         if len(self.doc.cuerpo) < 1000:
  ...             return 'el cuerpo del documento es muy corto'
  ...         else:
  ...             return ''

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()

  >>> gsm.registerSubscriptionAdapter(LongitudAdecuada)

  >>> from zope.component import subscribers

  >>> doc = Documento("Un\nDocumento", "blah")
  >>> [adaptador.validar()
  ...  for adaptador in subscribers([doc], IValidar)
  ...  if adaptador.validar()]
  ['El cuerpo del documento es muy corto']

  Ahora quite el registro: ::

  >>> gsm.unregisterSubscriptionAdapter(LongitudAdecuada)
  True

  Después de quitar el registro: ::

  >>> [adaptador.validar()
  ...  for adaptador in subscribers([doc], IValidar)
  ...  if adaptador.validar()]
  []


unregisterUtility
~~~~~~~~~~~~~~~~~

Esta función es usado para quitar registro un utilidad.  Un booleano es 
devuelto indicando si el registro fue cambiando.  Si el 
componente dado es None y allí no hay componente registrado, o si 
el componente dado no es None y no esta registrado, entonces la función
devuelve False, de lo contrario ese devuelve True.

 - Ubicación: ``zope.component - IComponentRegistry``

 - Firma: `unregisterUtility(component=None, provided=None,
   name=u'')`

 - Ver también: `registerUtility`_

Ejemplo: ::

  >>> from zope.interface import Interface
  >>> from zope.interface import implements

  >>> class ISaludador(Interface):
  ...     def saludar(nombre):
  ...         "decir hola"

  >>> class Saludador(object):
  ...
  ...     implements(ISaludador)
  ...
  ...     def saludar(self, nombre):
  ...         return "Hola" + nombre

  >>> from zope.component import getGlobalSiteManager
  >>> gsm = getGlobalSiteManager()

  >>> saludar = Saludador()
  >>> gsm.registerUtility(saludar)

  >>> queryUtility(ISaludador).saludar('Pedro')
  'Hola Pedro'

  Ahora quite el registro: ::

  >>> gsm.unregisterUtility(greet)
  True

  Después de quitar el registro: ::

  >>> print queryUtility(ISaludador)
  None


Fuentes bibliográficas
----------------------

-   `Una guía comprensiva de la Arquitectura de Componentes de Zope`_, por Baiju M.

.. _Una guía comprensiva de la Arquitectura de Componentes de Zope: http://www.muthukadan.net/docs/zca-es.html
