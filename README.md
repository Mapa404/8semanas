![Meditación, 8 semanas](./og-image.png)

# Meditación, 8 semanas

Una app minimalista para armar el hábito de meditar todos los días: calendario de seguimiento, temporizador con campana, un plan progresivo de 8 semanas y una guía para aprender a meditar.

**Demo en vivo:** [8semanas.vercel.app](https://8semanas.vercel.app)

No tiene backend, no tiene base de datos, no tiene build. Es un único archivo `index.html` que corre en cualquier navegador y guarda el progreso en `localStorage`.

---

## Qué hace

- **Calendario mensual** donde cada día se marca solo o a mano, con navegación entre meses.
- **Temporizador** con presets de 5 a 20 minutos, campana de inicio y cierre (sintetizada con Web Audio, sin archivos de audio), y una animación de círculo que "respira" mientras corre la sesión.
- **Plan de 8 semanas** que sube de a poco los minutos diarios y se detiene dos semanas para consolidar el hábito antes del próximo salto. El plan no es estático: la app calcula sola en qué semana estás según cuántos días completaste, y arranca cada sesión con la duración recomendada.
- **Racha de días seguidos**, para reforzar la idea central del método: todos los días le gana a mucho rato una vez por semana.
- **Guía "Aprender a meditar"**: postura, qué hacer cuando la mente se dispersa, errores comunes al empezar y preguntas frecuentes.
- Sin cuenta, sin login, sin tracking. Todo vive en el navegador de quien la usa.

## Cómo se hizo

El punto de partida fue **Google AI Studio** (Gemini): ahí armé la primera versión como un proyecto React + TypeScript + Vite, con el calendario y el plan como dos bloques separados. Cuando se acabaron los tokens de esa sesión, me pasé a **Claude** para rediseñarla de cero y sumarle lo que faltaba: el temporizador con campana, la barra de progreso real (calculada sobre las sesiones guardadas, no sobre la fecha del calendario), la racha, y la guía de meditación.

La decisión más importante fue técnica: en vez de mantener el proyecto Vite original, lo convertí a **un solo archivo HTML sin paso de build**. La razón es simple — quería poder subir esto a GitHub Pages o Vercel arrastrando un archivo, sin `npm install`, sin pipeline, sin que un cambio de versión de una dependencia rompa el deploy dentro de dos años. React, ReactDOM y Babel Standalone se cargan por CDN, y Babel transpila el JSX directo en el navegador al cargar la página.

El contenido de "Aprender a meditar" lo escribí después de revisar varias guías de meditación para principiantes (Mayo Clinic, Insight Timer, entre otras) para asegurarme de que la técnica y los errores comunes que describo son los que realmente se repiten en la literatura sobre el tema — pero está redactado de cero, no copiado de ninguna fuente.

## Stack técnico

- **React 18** (build UMD, vía CDN) — sin JSX precompilado
- **Babel Standalone** — transpila el JSX en el navegador al cargar la página
- **Web Audio API** — genera la campana de inicio/cierre con osciladores, no hay archivos `.mp3`
- **`localStorage`** — persistencia del progreso, por navegador
- **CSS variables + estilos inline** — sin Tailwind ni ningún framework de CSS
- **Google Fonts** — Fraunces (serif, para títulos y números) + Inter (sans, para el resto)
- Cero dependencias de `npm`, cero paso de build

## Decisiones de diseño

Quise evitar la estética genérica de "SaaS con IA" (fondo crema + acento terracota, o tarjetas idénticas con el mismo border-radius en todo). La paleta terminó siendo papel + musgo + un violeta apagado para los estados "actuales", pensada para que se sienta más cuaderno de hábitos que dashboard.

Dos decisiones puntuales:

- El **plan de 8 semanas se visualiza como un sendero de piedras** (círculos numerados conectados por una línea) en vez de una lista de tarjetas — la metáfora del camino le queda mejor a un hábito que se construye semana a semana que una tabla de datos.
- El **temporizador es un círculo que respira** (se expande y contrae cada 8 segundos mientras corre) en lugar de solo mostrar el número — un gesto chico, pero que conecta la interfaz con lo que estás haciendo mientras la mirás.

## Estructura del proyecto

```
├── index.html              App completa: HTML, CSS y JS en un solo archivo
├── og-image.png             Imagen para la vista previa al compartir el link
├── apple-touch-icon.png     Ícono para agregar el sitio a la pantalla de inicio en iOS
└── README.md
```

## Correr o publicar esto

No hace falta build ni `npm install`. Alcanza con abrir `index.html` en un navegador para probarlo local.

Para publicarlo:

**GitHub Pages**
1. Subí los tres archivos (`index.html`, `og-image.png`, `apple-touch-icon.png`) a la raíz del repo.
2. `Settings → Pages → Source`, elegí la rama `main` y la carpeta `/root`.
3. GitHub te da una URL en uno o dos minutos.

**Vercel**
Importá el repo tal cual — al no tener `package.json`, Vercel lo sirve como sitio estático sin ningún paso extra.

Si el dominio cambia, hay que actualizar tres líneas en el `<head>` de `index.html`: `<link rel="canonical">`, `<meta property="og:url">` y `<meta property="og:image">` — hoy apuntan a `https://8semanas.vercel.app`.

## Ideas para sumar

- Exportar/importar el progreso como JSON, para no perderlo si se cambia de navegador
- Modo oscuro
- Notificación diaria (vía Service Worker) para no depender de acordarse solo

## Licencia

MIT — usalo, forkealo, rompelo, lo que quieras.

## Autor

Hecho por **[Mapa Bianchi](https://www.linkedin.com/in/mapabianchi/)** — vibecoding.
Más proyectos en [mapabianchi.online](https://mapabianchi.online).
