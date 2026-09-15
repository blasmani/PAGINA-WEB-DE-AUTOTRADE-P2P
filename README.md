# AutoTrade P2P — sitio web

Pagina estatica para GitHub Pages. Sin build: son ficheros HTML, un CSS y un JS.

## El producto que vende esta web: DOS versiones vivas

Esto es lo primero que hay que saber antes de escribir una sola frase en los HTML, porque
casi todas las correcciones de esta web han salido de olvidarlo:

| Version | Donde corre | Estado |
|---|---|---|
| **Web** — <https://app.autotradep2p.com/> | El motor y los datos, en servidores nuestros | **Disponible ya** |
| **Windows** — Microsoft Store | Todo en la PC del usuario | **En certificacion** |

No es que una sustituyera a la otra: **conviven, y el usuario elige**. Una frase que solo
valga para una tiene que decir para cual —«en la version web» / «en la version de Windows»—,
y esto vale igual para la portada que para los dos legales. La `privacy.html` §12 cuenta el
caso de manual: se publico «todo se queda en tu PC» sin acotar, dejo de ser cierto de la web,
y la correccion se paso de frenada dando por muerta la version de Windows —que es la que
enlaza esa misma pagina desde su ficha de la Store—.

Y lo que la app puede hacer de verdad manda sobre lo que aqui se prometa. Ejemplo medido: la
portada prometio **CSV** hasta el 2026-08-25, y el boton de CSV se habia retirado de la app el
2026-08-21. Hoy hay **dos descargas de Excel** y ninguna otra: la completa y la «Excel F»,
reducida para pegar en el sistema de facturacion.

## Que hay aqui

| Fichero | Que es |
|---|---|
| `index.html` | Portada |
| `privacy.html` | Politica de privacidad |
| `terms.html` | Terminos y condiciones |
| `assets/idioma.js` | El conmutador EN / ES |
| `assets/sitio.js` | 30 lineas: el filete de la cabecera al hacer scroll y «solo una pregunta abierta» en el FAQ. Sin el, la pagina funciona igual |
| `assets/styles.css` | Los estilos del diseño «Marino sobre hielo» (abajo) |
| `assets/og.png` | La imagen de la vista previa social (1200x630): la maqueta del ranking con la banda, rasterizada. **No hay ilustracion en la portada desde el 2026-09-15**: la imagen es el producto, en maquetas HTML |
| `assets/icono.png` | El icono de la app, usado como favicon. **En la cabecera ya no va** (2026-09-12, el dueno lo quito con la captura delante: solo el nombre) |

### Si cambias la portada, vuelve a generar `assets/og.png`

La imagen social no se dibuja a mano: es una pagina de 1200x630 con la maqueta del ranking
(el `_og.html` que se uso el 2026-09-14 esta en el historial del repositorio
`autotradep2p-web-rediseno`), rasterizada con el Electron del monorepo
(`herramientas/capturar-web.cjs`, ver la memoria «capturas web con Electron»). Chrome y Edge
sin cabeza no escribieron nada en este equipo; el panel del navegador tampoco devuelve capturas.

## El diseño: «Marino sobre hielo» (2026-09-15)

Sustituyo a «Mesa de Control» (2026-08-20, negro con el amarillo de Binance) porque el dueño lo
vio **«un poco feo con esos colores, no se ve premium»** y pidio inspirarse en los colores de
autop2p.dev y silver5ai.com. Lo que queda de aquel: la idea de fondo —esto toca dinero de
verdad, lo premium es la **precision**, no el espectaculo—, cero emojis, iconos SVG de trazo.

Lo que define al nuevo, y conviene no romper sin querer:

1. **Lienzo claro gris frio (`#eef1f5`), tinta azul marino (`#0f1729`) y UN solo acento azul
   (`#2f63e6`)**, que aparece solo donde se pulsa: boton primario, riel de la banda, anillo de
   foco. El verde y el rojo son semanticos y solo viven dentro de las maquetas y de la banda
   «Tres nunca, dos siempre». Ni negro ni amarillo.
2. **Islas blancas de radio grande** (36 px en escritorio, 20 px en movil) sobre el lienzo, y
   **una sola isla oscura** (`#0b1220`), la del motor de precios: el contraste ocurre una vez.
   La isla oscura redefine los tokens (`--tinta`, `--linea`, `--ok`…), asi que lo que hay
   dentro se pinta con las mismas reglas; si anades un color, redefinelo ahi tambien o saldra
   ilegible (el verde de fuera daba 2,3:1 dentro).
3. **Instrument Sans + Geist Mono**, dos familias de Google Fonts. Titular de 72 px en
   escritorio y 40 en movil; rotulos mono de 12 px, que es el **suelo de todo el sitio**
   (tambien dentro de las maquetas), y **44 px** para cualquier cosa que se pueda pulsar. La
   unica excepcion es el enlace `t.me/…` dentro de una frase del FAQ (WCAG 2.5.8 exceptua los
   enlaces en linea).
4. **La imagen es el producto.** No hay robot ni capturas: maquetas en HTML y CSS del ranking
   con la banda de puestos, del chat de una orden, del historial, de los disparadores, de la
   regla del motor, de tres instantes del ranking y de los cuatro pasos. Se traducen con el
   conmutador, pesan cero bytes y **todas llevan el rotulo «Ilustracion · datos de ejemplo»**.
   Los datos son ficticios: apodos inventados, iniciales, «Transferencia» y «Billetera» como
   metodos, sin bancos ni nombres de personas, y **solo marcadores que la app tenga de verdad**
   (`{nombre}`; un `{amount}` inventado lo tumbo la revision).
5. **Nada rebota, nada se levanta al pasar el raton, nada late en bucle.** Los hover y los
   `:active` cambian color, no posicion. El revelado al hacer scroll es CSS puro
   (`animation-timeline: view()`), dentro de `@supports` **y** de `prefers-reduced-motion`:
   con un observador de JavaScript, si no arranca, el contenido se queda invisible sin error.
6. **Movil sin menu**: por debajo de 900 px las anclas de la cabecera se van y aparece un
   indice de secciones bajo la franja de hechos (`.indice`); `scroll-padding-top` en `html`
   deja el rotulo a la vista al saltar por ancla bajo la cabecera pegada.

Salio de un panel de tres direcciones de diseño juzgadas por tres revisores y de una revision
adversaria (contenido, idiomas, accesibilidad, tecnica, diseño) antes de publicarse. Las
capturas de comprobacion se hacen con Electron a 1366, 820 y 390 px en los dos idiomas.

### El icono nunca va dentro de un texto traducido

`idioma.js` hace `n.innerHTML = n.getAttribute('data-' + idioma)` sobre **cada** elemento con
`[data-en]`. Un `<svg>` metido dentro desaparece la primera vez que alguien pulsa ES y ya no
vuelve, **sin dar ningún error**. El SVG va siempre como hermano del `<span>` traducido:

```html
BIEN : <p class="fila"><svg class="i">…</svg><span data-en="…" data-es="…">…</span></p>
MAL  : <p data-en="…" data-es="…"><svg>…</svg>texto</p>
```

Se comprueba contando `document.querySelectorAll('svg').length` antes y después de varios
ciclos EN → ES → EN. Tiene que dar el mismo número.

### Cómo revisar el móvil de verdad

Chrome headless **impone un ancho mínimo de ventana** (~500px): pedir `--window-size=390,…`
da una captura de 390px de una página maquetada a 500, y parece un desborde que no existe.
Para un viewport real de 390 se usa `_movil.html`, un andamio con un `<iframe>` de 390px
dentro de una ventana grande. Está en `.gitignore` a propósito: es una herramienta, no parte
del sitio.

## El idioma

**Ingles por defecto**, espanol a un clic, y la eleccion se recuerda en el navegador.

Cada texto lleva sus DOS versiones en el mismo sitio, en los atributos `data-en` y `data-es`.
Es a proposito: con dos ficheros separados por idioma, alguien corrige una frase en ingles,
se olvida del espanol, y el sitio empieza a prometer cosas distintas segun quien lo lea.

No adivina el idioma del navegador. Un sitio que se pinta distinto segun desde donde se abra
es imposible de compartir: mandas un enlace, lo abren, y ven otra cosa.

## Pendiente de la certificacion

> Esta seccion decia que habia que buscar un comentario **`AVISO TEMPORAL`** y dejar «solo el
> boton de la Store». Las dos cosas son falsas desde el 2026-08-25: ese comentario ya no
> existe —se llama `CANJE-STORE`— y dejar solo el boton de la Store seria borrar el enlace de
> la app web, que es **la version que funciona hoy**. Se deja escrito para que nadie lo
> «restaure».

Mientras dure la certificacion, el enlace `https://apps.microsoft.com/detail/9PL6F67SSZV8`
devuelve **404**. `index.html` tiene los dos puntos afectados marcados con el comentario
**`CANJE-STORE`** (1 de 2 en la portada, 2 de 2 en la ficha de precio); se encuentran
buscando esa palabra.

El dia que Microsoft apruebe la ficha:

- **Se borra** el chip «In Store certification», que va pegado al boton de la Store en la
  portada.
- **Se borran** las dos notas que dicen que la version de Windows sigue en certificacion: la
  de debajo de los botones de la portada y la del pie de la ficha de precio.
- **Se revisa** el «once approved» / «cuando la aprueben» de las filas *Trial*, *Billing* y
  *Cancellation* de la ficha de precio, y el «still in certification» de `terms.html` §2 y de
  `privacy.html` §12.
- **NO se toca nada mas. Los dos botones se quedan**, y el de la app web va primero en el pie:
  la web no es un parche mientras dura la certificacion, es una de las dos versiones del
  producto.

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
