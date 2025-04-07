# Filtro de evasión de bloqueos de LaLiga ⚽🚫
Este filtro permite evadir los bloqueos de LaLiga y Telefónica a miles de sitios web que utilizan CDNs como Cloudflare, BunnyCDN u otros proveedores cambiando la dirección IP de la solicitud hacia una dirección IP que no está bloqueada por las operadoras. 

## ¿Qué está pasando en España con LaLiga y Telefónica?
Gracias a una sentencia obtenida por LaLiga y Telefonica, las operadoras prinicipales están obligadas a bloquear las direcciones IP de las emisiones de fútbol pirata que se van ofreciendo con herramientas internas de LaLiga para detectar los enlaces de retransmisiones de fútbol pirata, obtener sus direcciones IP y enviarselas a las operadoras para su posterior bloqueo. Esta decisión se basa en que ECH y Apple Private Relay permiten a los usuarios esquivar los bloqueos tradicionales, que se hacían mediante filtrado DPI hacia el dominio que alojaba el contenido pirata. 

Sin embargo, este bloqueo ha traído graves consecuencias para los usuarios: la incapacidad de poder acceder a cientos de sitios web que comparten la dirección IP con los dominios que alojan tranmisiones de fútbol pirata. Afecta principalmente a Cloudflare, pero no están exentos otros CDN como BunnyCDN o incluso direcciones IP de GitHub, ya que LaLiga se argumenta en que se comparten dominios de retransmisiones pirata a través de GitHub. 

Dependiendo de la operadora utilizada podrás o no encontrarte con problemas para acceder a ciertos sitios web:

| Operadora | ¿Aplica el bloqueo? |
|-----------|:-------------------:|
| Movistar/O2 | ✅ |
| Vodafone/Lowi | ⚠️ |
| Orange/Jazztel/Simyo | ⚠️ |
| MasMovil/Yoigo/Pepephone | ✅ |
| DIGI | ✅ |
| Locales (Avatel, Adamo, Fi) | ❌ |

⚠️ Solo se aplican los bloqueos si el usuario no está utilizando ECH, ya que filtran solamente por DPI. Las retranmisiones de fútbol pirata quedan bloqueadas, pero no se bloquea el contenido legítimo. 

## ¿Cómo funciona el filtro? 
Este filtro aprovecha las bondades de los principales servidores CDN, permitiendo cambiar la dirección IP bloqueada que nos da el servidor DNS por una dirección IP del CDN afectado que no está bloqueado, permitiendo a los sitios web cargar correctamente. 

Por ejemplo, si la URL "ejemplo.com" está asociada a la IP "1.2.3.4" que está bloqueada por las operadoras, este filtro realiza el cambio a una IP no bloqueada, como "1.2.3.5", para que las páginas legítimas puedan cargar correctamente. Dependiendo de la situación, se rota a la siguiente dirección IP o se elige una dirección IP distinta que pertenezca al mismo CDN. 

## Limitaciones del filtro
### Subdominios (*.dominio.com)
Una importante limitación de este filtro, es que no se pueden aplicar ante algunos casos donde los subdominios pertenecientes a un mismo dominio pueden ser prácticamente ilimitados. Este es el caso del dominio github.io, cuyos subdominios pueden ser infinitos, y sería demasiado laborioso tener que estar agregando todos los subdominios (sin embargo, se pueden añadir los más populares).
### El mismo dominio con y sin www (dominio.com y wwww.dominio.com)
Otra limitación conciste en la existencia de páginas web que pueden resolver de ambas maneras: escribiendo los "wwww" y sin escribirlos. Aunque en los filtros se agregan ambos registros, es posible que en alguna página lo haya omitido y provoca que la versión sin www cargue durante un bloqueo, pero la versión con www no (y viceversa). 

### Desactivación de Cloudflare por parte de la página
Algunas páginas pueden hartarse de la situación, y desvincularse de la red del CDN. Esto puede provocar que el filtro bloquee el acceso a la página, ya que seguirá redirigiendo al CDN aunque este lo haya desactivado. En este caso, hay que [abrir una incidencia](https://github.com/fdezsergio02/Anti-LaLiga/issues/new/choose) para borrar la página web del filtro. 

## Cómo aplicar el filtro
El filtro tiene dos versiones: una versión adaptada a los clientes de Adguard (extensión, programas o Adguard Home) que permiten realizar la redirección, y otra versión adaptada directamente para aplicar directamente en el archivo hosts del sistema operativo, o usar aplicaciones como AdAway en el caso de Android para aplicar reglas hosts.

| Tipo    | Enlaces |
|---------|---------|
| Adblock | [Descargar](https://raw.githubusercontent.com/fdezsergio02/Anti-LaLiga/refs/heads/main/filters/adblock.txt) |
| Hosts   | [Descargar](https://raw.githubusercontent.com/fdezsergio02/Anti-LaLiga/refs/heads/main/filters/hosts.txt) |