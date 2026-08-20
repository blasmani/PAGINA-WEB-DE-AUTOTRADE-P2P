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
| `assets/hero.jpg` | La ilustracion de la portada, 1066x896 |
| `assets/icono.png` | El icono de la app, usado tambien como favicon |

### Si cambias la ilustracion de la portada

Dos cosas, y las dos han fallado ya:

1. **Cambia `width` y `height` del `<img>` para que coincidan con el archivo nuevo.** No son
   decoracion: le dicen al navegador la proporcion antes de descargarla, y con ellos mal el
   texto de al lado da un salto al terminar de cargar.
2. **Comprueba que sigue el `height: auto` del CSS.** Sin el, el navegador usa el atributo
   `height` como alto real y la imagen sale estirada. Paso el 2026-08-19: proporcion original
   1,79 y pintada 0,30.

La proporcion comoda aqui esta entre 4:3 y 1:1. El contenedor mide 339 px en movil, **817 px
en tableta —que es el mas ancho—** y 501 px en un escritorio de 1920: una imagen 16:9 se queda
como una tira y una vertical empuja el resto de la pagina fuera de la primera pantalla.
Y guardala en JPEG salvo que necesite transparencia: la actual pasaba de 1.073 KB en PNG a
159 KB en JPEG de calidad 92 sin diferencia visible.

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
