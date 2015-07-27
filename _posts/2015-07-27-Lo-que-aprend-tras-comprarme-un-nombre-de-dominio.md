---
layout: post
title: Lo que aprendí tras comprarme un nombre de dominio
date: 2015-07-28 01:27:10.000000000 +01:00
tags:
- DNS
- dominios
status: draft
type: post
published: false
meta:
  _edit_last: '1'
author:
  login: palvarez89
  email: palvarez89@gmail.com
  display_name: palvarez89
  first_name: 'Pedro'
  last_name: 'Alvarez Piedehierro'
excerpt: !ruby/object:Hpricot::Doc
  options: {}
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

Lo primero que intenté crear un subdominio **pedro** apuntando a
[pedroalvarez.hol.es][2]. Tras leer [sobre los diferentes tipos de registros
DNS][1], decidí probar por un registro **CNAME** ya que, por lo que entendí,
es la manera de crear alias de otros dominios. Como podéis leer: *"... se usa
para crear nombres de servidores de alojamiento adicionales, o alias, para los
servidores de alojamiento de un dominio... "* no está del todo claro, pero era
lo que más se ajustaba a lo que quería.

No funcionó. Lo único que conseguí es que se mostrase una pagina de error
de Hostinger (donde tenía alojado mi WordPress). Estaba claro que el CNAME
estaba funcionando, pero a Hostinger no le estaba gustando... Y yo entendía
nada...

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

Inaceptable! Yo queria que mi web se viese bien desde todos sitios, por ello me
habia esforzado en integrar un tema *responsive*! Me puse manos a la obra y a
investigar cómo podría solucionar esto, y si alguien usando Hostinger había
intentado hacer lo mismo que yo. Las primeras pistas que encontré eran cosas
como:

  * *"Hey, lo que tienes que hacer es configurar tu dominio para usar los
    NameServers de Hostinger."*

  * *Tienes que ir al panel de control de Hostinger, buscar la IP, y crear un
    registro de tipo 'A' con la misma."*

La primera pista aún no la entendía, asique decidí ir a por la segunda e
investigando por Hostinger encontre la IP que debía usar para el registro A.
Pero con el registro A tambien fallab con la misma pagina de error de
Hostinger... Y si abro directamente la IP en el navegador? Mismo error! Y yo
sigo sin entender nada!

Por qué el registro A debía funcionar si al abrir la IP Hostinger no me
motstraba la página? Es que tengo una IP dedicada en un servidor de free
hosting? Si hay una cosa que no sobran en 2015 son direcciones IPv4, por tanto
supongo que no, que Hostinger sirve varios hosting usando la misma IP, y como
consecuencia, simplemente con el registro A, o abriendo la IP en el navegador,
no sabe que página mostrarme (La mia o cualquier otra corriendo en el mismo
servidor).

Hay algo que se me escapa...



## Lecciones aprendidas

Puedes empezar a probar la configuración de un nombre de dominio incluso antes
de comprarlo.

[1]: https://es.m.wikipedia.org/w/index.php?title=Domain_Name_System&redirect=no

[2]: http://pedroalvarez.hol.es

