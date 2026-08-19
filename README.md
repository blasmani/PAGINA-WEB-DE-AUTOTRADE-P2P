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

## Dominio

Ahora mismo se sirve en `blasmani.github.io/PAGINA-WEB-DE-AUTOTRADE-P2P`. Si algun dia se
compra un dominio, se anade un fichero `CNAME` con el nombre y se apunta el DNS a GitHub
Pages, igual que en la web de LocalClip.
