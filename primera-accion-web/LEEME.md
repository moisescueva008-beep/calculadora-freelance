# Primera Acción Perú · paquete para publicar

Página web instalable (PWA). No necesita servidor ni compilación: son archivos estáticos.

## Qué hay en la carpeta

| Archivo | Para qué sirve |
|---|---|
| `index.html` | La página completa (diseño, datos y lógica). |
| `manifest.webmanifest` | Nombre, colores e íconos para instalarla como app. |
| `sw.js` | Service worker: guarda la página para abrirla sin conexión. |
| `icons/` | Íconos de 192 y 512 px, ícono adaptable para Android, ícono de iPhone y favicon. |
| `_headers` | Reglas de caché para Netlify y Cloudflare Pages. Otros hostings la ignoran. |
| `.nojekyll` | Evita que GitHub Pages ignore archivos. |

## Cómo publicarla (elige una)

Todas ofrecen planes gratuitos para sitios estáticos. Las pantallas pueden cambiar, así que guíate por sus nombres, no por la posición de los botones.

1. **Netlify Drop (lo más rápido).** Entra a `app.netlify.com/drop`, arrastra la carpeta completa y obtienes una dirección pública.
2. **Cloudflare Pages.** Crea un proyecto con «Direct Upload», sube la carpeta y publica.
3. **GitHub Pages.** Crea un repositorio, sube todos los archivos (incluido `.nojekyll`), ve a Settings → Pages y elige la rama principal como origen.
4. **Vercel.** Importa la carpeta como proyecto estático, sin comando de compilación.

Tiene que servirse por **HTTPS** (todos los anteriores lo hacen) para que funcione el modo sin conexión y la instalación.

## Dominio propio (opcional)

Compra un dominio (`.pe` o `.com`) y, en el panel de tu hosting, añade «dominio personalizado». Sigue las instrucciones de DNS que te muestre.

## Instalarla como app

- **Android (Chrome):** menú ⋮ → «Instalar app» o «Agregar a pantalla de inicio».
- **iPhone (Safari):** botón Compartir → «Agregar a pantalla de inicio».
- **Computadora (Chrome o Edge):** ícono de instalar en la barra de direcciones.

## Antes de difundirla

- [ ] Revisa que cada dato tenga fecha reciente (dividendos, precios, tarifas de brokers). Todo está escrito a mano en `index.html`.
- [ ] Confirma las tarifas de Trii, XTB y Hapi en sus sitios oficiales. La tarifa de Trii (S/ 10) es de 2022.
- [ ] Haz revisar el aviso legal con un profesional si la vas a promover de forma pública.
- [ ] Si agregas estadísticas de uso, cookies o formularios, añade una política de privacidad. Hoy la página solo guarda tu avance en el navegador del propio usuario y no envía datos a ningún servidor.

## Cómo actualizar datos o diseño

1. Abre `index.html` con un editor de texto.
2. Los datos de empresas están en el objeto `CO` (dentro del `<script>`): dividendos, precios, rentabilidad y notas. Los retornos anuales de VOO están en `RET` y los precios y dividendos de Coca-Cola en `KOP` y `KOD`. Los brokers están en `BROKERS`.
3. Guarda el archivo.
4. En `sw.js`, **sube el número de `VERSION`** (por ejemplo de `primera-accion-v1` a `primera-accion-v2`). Sin este paso, algunos usuarios seguirían viendo la versión anterior guardada.
5. Vuelve a subir los archivos al hosting.

## Probarla en tu computadora

Desde la carpeta, en una terminal:

```
python3 -m http.server 8000
```

Abre `http://localhost:8000`. En `localhost` el service worker también funciona, así que puedes probar la instalación y el modo sin conexión (DevTools → Application).

## Tipografías

Las letras (Instrument Serif, Hanken Grotesk y DM Mono) se cargan desde Google Fonts y el service worker las guarda después de la primera visita. Si prefieres no depender de un tercero, descárgalas, colócalas en una carpeta `fonts/` y reemplaza el enlace de Google Fonts por reglas `@font-face`.

## Publicar en tiendas (más adelante)

Con la PWA publicada puedes empaquetarla para Google Play con herramientas como PWABuilder. Las tiendas piden cuenta de desarrollador y revisan el contenido financiero según sus reglas.
