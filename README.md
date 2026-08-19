# AutoTrade P2P — sitio web

Pagina estatica para GitHub Pages. Sin build: son ficheros HTML, un CSS y un JS.

## Que hay aqui

| Fichero | Que es |
|---|---|
| `index.html` | Portada |
| `privacy.html` | Politica de privacidad |
| `terms.html` | Terminos y condiciones |
| `assets/idioma.js` | El conmutador EN / ES |
| `assets/styles.css` | Los estilos, con la paleta de la propia app |

## El idioma

**Ingles por defecto**, espanol a un clic, y la eleccion se recuerda en el navegador.

Cada texto lleva sus DOS versiones en el mismo sitio, en los atributos `data-en` y `data-es`.
Es a proposito: con dos ficheros separados por idioma, alguien corrige una frase en ingles,
se olvida del espanol, y el sitio empieza a prometer cosas distintas segun quien lo lea.

No adivina el idioma del navegador. Un sitio que se pinta distinto segun desde donde se abra
es imposible de compartir: mandas un enlace, lo abren, y ven otra cosa.

## Pendiente de la certificacion

`index.html` lleva un aviso temporal debajo del boton de descarga que dice que la app esta en
revision de Microsoft Store. **Hay que borrar esa linea** en cuanto la app se publique: esta
marcada con un comentario `AVISO TEMPORAL`. Hasta entonces el enlace
`https://apps.microsoft.com/detail/9PL6F67SSZV8` devuelve 404, y prometer una descarga que no
existe es peor que decir la verdad.

## Dominio: autotradep2p.com

En linea desde el 2026-08-19 en **https://autotradep2p.com**, con certificado HTTPS emitido
por GitHub y redireccion forzada.

DNS en GoDaddy (los nameservers siguen siendo los de GoDaddy, ns27/ns28.domaincontrol.com):

| Tipo | Nombre | Valor |
|---|---|---|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | blasmani.github.io. |
| TXT | _github-pages-challenge-blasmani | (codigo de verificacion de GitHub) |

**Las cuatro A hacen falta**, no una: son los cuatro servidores de GitHub Pages, y con una
sola la web se cae cuando ese servidor falla.

El fichero `CNAME` de este repositorio es lo que hace que GitHub recuerde el dominio en cada
publicacion. Si se borra, el sitio vuelve a servirse en `blasmani.github.io/...`.

La A que habia antes apuntaba al creador de webs de GoDaddy («WebsiteBuilder Site») y se
sustituyo. El CNAME `www` apuntaba al propio dominio y ahora apunta a GitHub.
