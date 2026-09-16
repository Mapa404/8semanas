# Meditación, 8 semanas

App de seguimiento de meditación: calendario, temporizador con campana, plan de 8 semanas y una guía para aprender a meditar.

Es un único archivo (`index.html`) sin build ni backend, más dos imágenes chicas para el favicon y la vista previa al compartir el link. El progreso se guarda en `localStorage`, en el navegador de quien la usa — cada dispositivo lleva su propio historial, no se sincroniza entre navegadores.

## Archivos a subir

- `index.html`
- `og-image.png` — imagen que se muestra al compartir el link en WhatsApp, Slack, Twitter/X, etc. Tiene que vivir en la raíz del sitio, al lado de `index.html`, porque el `<meta property="og:image">` la referencia por esa ruta.
- `apple-touch-icon.png` — ícono cuando alguien agrega el sitio a la pantalla de inicio en iOS.

## Si cambiás de dominio

El `index.html` tiene el dominio actual (`https://8semanas.vercel.app`) hardcodeado en tres lugares: `<link rel="canonical">`, `<meta property="og:url">` y `<meta property="og:image">`. Si el sitio se muda a otra URL, hay que actualizar esos tres valores para que las vistas previas sigan funcionando.

## Publicar en GitHub Pages

1. Subí los tres archivos de arriba a la raíz de un repositorio.
2. En el repo, andá a **Settings → Pages**.
3. En **Source**, elegí la rama y la carpeta donde están los archivos (por ejemplo `main` / `/root`).
4. Guardá. GitHub te va a dar una URL tipo `https://tu-usuario.github.io/tu-repo/` en uno o dos minutos.

No hace falta ningún paso de instalación ni `npm install`.
