---
layout: post
title: Lo que aprendí tras comprarme un nombre de dominio
date: 2015-07-28 01:27:10.000000000 +01:00
tags:
- DNS
- dominios
status: publish
type: post
published: true
meta:
  _edit_last: '1'
author:
  login: palvarez89
  email: palvarez89@gmail.com
  display_name: palvarez89
  first_name: 'Pedro'
  last_name: 'Alvarez Piedehierro'
---

Llevaba ya un tiempo dándole vueltas a nombres de dominio. Tenía ganas de
comprar uno para poder usarlo para apuntar a mi página web personal, con
información sobre mi etc. También para poder usarlo para otros motivos, como
usar urls consistentes para algún servicio web y no depender de los diferentes
hostings (gratuitos) y sus nombres de dominio aleatorios.

Al final me decanté por comprar **alvarezpiedehierro.com**, para luego usar
como subdomino mi nombre. Hice un *research* acerca de en donde me saldría más
barato y al final acabé comparándolo en Nominalia.

El proceso de compra fue muy sencillo. El problema empezó cuando empecé a
intentar configurarlo..

<!--more-->

Lo primero que intenté crear un subdominio **pedro** apuntando a
[pedroalvarez.hol.es][2]. Tras leer [sobre los diferentes tipos de registros
DNS][1], decidí probar por un registro **CNAME** ya que, por lo que entendí, es
la manera de crear alias de otros dominios. Como podéis leer: *"... se usa para
crear nombres de servidores de alojamiento adicionales, o alias, para los
servidores de alojamiento de un dominio..."* no está del todo claro, pero era
lo que más se ajustaba a lo que quería.

No funcionó. Lo único que conseguí es que se mostrase una pagina de error de
Hostinger (donde tenía alojado mi WordPress). Estaba claro que el CNAME estaba
funcionando, pero a Hostinger no le estaba gustando... Y yo entendía nada...

Jugando con las posibilidades que me daba Nominalia encontré (entre muchos
conceptos nuevos para mi) la palabra **redirección**, y decidí intentarlo con
esa opción. Tras hacer el cambio y esperar a que el nuevo registro fuese
actualizado, pude comprobar que esa opción funcionaba.

Ya está!! Funciona, ha sido sencillo, no? Pero... un momento... Cuando abro la
página desde el móvil no se ve del todo bien... Y cuando abro la [URL del
blog][2] directamente se ve perfecto, responsive, etc...

Tras investigar un poco encontré gente con problemas parecidos (ya sabes, en
este mundo lo que te pasa a ti seguro que ya le ha pasado a alguien), y el
problema resultó ser que sus redirecciones estaban poniendo la web de destino
dentro de un `<frame>`. En efecto! Eso mismo me estaba pasando a mi.

**Inaceptable!** Yo quería que mi web se viese bien desde todos sitios, por
ello me había esforzado en integrar un tema *responsive*! Me puse manos a la
obra y a investigar cómo podría solucionar esto, y si alguien usando Hostinger
había intentado hacer lo mismo que yo. Las primeras pistas que encontré eran
cosas como:

  * *"Ey, lo que tienes que hacer es configurar tu dominio para usar los
    nameservers de Hostinger."*

  * *Tienes que ir al panel de control de Hostinger, buscar la IP, y crear un
    registro de tipo 'A' con la misma."*

La primera pista aún no la entendía, así que decidí ir a por la segunda e
investigando por Hostinger encontré la IP que debía usar para un *registro A*.
Pero con el *registro A* también fallaba con la misma pagina de error de
Hostinger... Y si abro directamente la IP en el navegador? Mismo error! Y yo
sigo sin entender nada!

Por qué el registro A debía funcionar si al abrir la IP Hostinger no me
mostraba la página? Es que tengo una IP dedicada en un servidor de free
hosting? Si hay una cosa que no sobran en 2015 son direcciones IPv4, por tanto
supongo que no, que Hostinger sirve varios hosting usando la misma IP, y como
consecuencia, simplemente con el registro A, o abriendo la IP en el navegador,
no sabe que página mostrarme (La mía o cualquier otra corriendo en el mismo
servidor).

Hay algo que se me escapa... Como va a saber Hostinger qué página abrir solo
con la IP, si la misma IP esta siendo usada para muchas mas páginas?

Tras leer mas comentarios por internet creí que la verdadera respuesta era usar
los nameservers de Hostinger, pero dado que en Hostinger no podía cambiarlos,
decidí migrar a GoDaddy (por solo £1, good deal). Una vez migrado empecé a
jugar con los nameservers, pero para mi, este plan seguía sin tener sentido
alguno. Por qué al usar los nameservers de Hostiner todo debería funcionar
milagrosamente? Como saben los nameservers de Hostinger que lo que tienen que
resolver es pedro.alvarezpiedehierro.com? Ni idea!

Pero tras buscar, buscar y madurar información sobre estos conceptos aún tan
abstractos para mi, logré encontrar algo, que me guió para poder entender todo
el meollo. Por lo visto, lo que me faltaba configurar era Hostinger para que
supiera que mi sitio web iba a poder ser accedido desde una URL diferente. Y
esto se conseguía **aparcando el dominio** en la configuración de Hostinger...
Aunque aún me quedaba una ultima sorpresa antes de que pudiera configurar la
entrada DNS a mi blog: **Hostinger no permite aparcar subdominios,** perfecto!

---

Después de todo este proceso de error-aprendizaje, ya sabía cuales eran las
piezas que necesitaba para poder hacer lo que quería, y una de ellas Hostinger
no me la podía ofrecer, con lo que debía de moverme a otro sito. Tras probar
ciertas alternativas que permiten aparcar subdominos (x10hosting, 000webhost)
intenté configurar Wordpress en ellos, y de hecho conseguí lo que quería en
ambos, pero también descubrí que x10hosting funcionaba a veces, y que
000webhost no aguantaba la carga de PHP de Wordpress.

Al final, tras mucho investigar decidí abandonar Wordpress y moverme a Jekyll,
con Github sites, y olvidarme de Wordpress. Una simple página web no debería
necesitar tantos recursos.

## Lecciones aprendidas

* Con un **registro A** apuntas a una IP.

* Con uno del tipo **CNAME** apuntas a una IP también, pero especificando el
  nombre de dominio. A efectos prácticos es como si resolvieras la IP del
  dominio al que quieres apuntar, y crearas un *registro A* con esa IP.

* Apuntar con un domino a otra URL no es normalmente posible. Depende de a
  dónde quieras apuntar, y si el sitio al que apuntas permite ser abierto con
  el nombre de dominio que quieres usar. Si un sitio es accesible vía IP, esto
  podría suponer problemas de seguridad para éste.

* Si usas los nameservers de tu hosting provider, lo único que estas haciendo
  es que eso nameservers decidan. Nada funcionará si no tienes nada configurado
  en esos nameservers (o en tu hosting provider) para indicar cual es el dominio
  o subdominio que quieres usar. Al hacer esto también cualquier registro que
  tengas configurado en tu proveedor de nombres de dominio, no será usado.

* La herramienta `nslookup` es útil para saber a que IP resuelven cierto
  dominio en cierto nameserver. Esto me fue útil en x10hosting para descubrir
  la IP que tenia que usar en el *registro A* en lugar de usar sus nameservers.

* Puedes empezar a probar la configuración de un nombre de dominio incluso
  antes de comprarlo. Usando /etc/hosts para definir tuplas "IP -
  nombre-de-dominio" puedes comprobar el resultado.

* Antes de comprar un dominio, asegúrate de que vas a poder utilizarlo. No
  todos los hostings te permiten usar tu propio nombre de dominio. En algunos
  incluso te dan la opción de pagar un extra para darte esta opción.

* Wordpress, Joomla? Necesitamos tanto para crear paginas web estáticas? Por
  supuesto que no.

* Jekyll & Github pages mola.

[1]: https://es.m.wikipedia.org/w/index.php?title=Domain_Name_System&redirect=no

[2]: http://pedroalvarez.hol.es
