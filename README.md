# Agenda de citas — Marta R.

Página web (un único `index.html`, sin build ni backend propio) para que las clientas de Marta R. reserven sesión de
neurocoaching. Sigue la guía de marca (`Marta R.` — OrganicStudio): paleta de color, tipografía Fraunces + Inter y
los 4 pilares del acompañamiento.

## Cómo funciona

La web **no gestiona las citas ella misma** — la reserva real se hace en el "Horario de citas" de Google Calendar
de Marta (una única sesión de 1h, válida tanto para online como presencial). La web es la puerta de entrada bonita
y de marca: el botón "Pedir cita ahora" lleva directamente a ese calendario real para que la clienta elija día y
hora.

Con esto, las tres cosas que hacían falta quedan resueltas por Google (no por código nuestro, que podría fallar):

- **La cita se guarda de verdad**, en el Google Calendar de Marta, no en el navegador de la clienta.
- **Marta se entera al momento**: la cita aparece directamente en su calendario en cuanto se reserva.
- **A la clienta le llega confirmación por email**, con opción de añadirla a su propio calendario, cambiarla o
  cancelarla — todo gestionado por Google, no por nosotros.

## Configuración (hacerlo una vez, desde la cuenta de Google de Marta)

1. Entra en [Google Calendar](https://calendar.google.com) con la cuenta de Marta.
2. Pulsa **Crear** → **Horario de citas**.
3. Configura la sesión — título `Sesión con Marta R.`, duración 1h, y en **Descripción** pega esto tal cual (ya
   incluye el aviso de privacidad y el recordatorio de dejar el teléfono):

   > Sesión de neurocoaching (online o presencial — indícamelo en las notas). Cuéntame en las notas qué te trae
   > por aquí y déjame tu teléfono si quieres el recordatorio por WhatsApp. Tus datos se usan únicamente para
   > gestionar tu cita, conforme a mi política de privacidad.

   Además:
   - En **"Formulario de reserva"**, activa el campo de teléfono si está disponible; si no, activa "Notas
     adicionales" (el texto de arriba ya le pide a la clienta que apunte ahí su teléfono y la modalidad).
   - Define los días y horas en los que Marta está disponible, y el margen mínimo de antelación para reservar
     (por ejemplo, mínimo 12h y máximo 60 días vista).
   - En **Ubicación**, ya que sirve para online y presencial, puedes poner algo como "Se confirma la modalidad
     por WhatsApp tras la reserva" o activar "Añadir Google Meet" y avisar en la descripción de que solo aplica
     a las sesiones online.
4. Pulsa **Compartir** → **Copiar enlace de reservas**.

El enlace real ya está incorporado en [`index.html`](index.html):

```js
const ENLACE_RESERVA = 'https://calendar.app.google/MuWoC7tKX28WT7138';
```

Si en algún momento Marta cambia de horario de citas (o crea uno nuevo), solo hay que sustituir esa línea por el
enlace nuevo, hacer commit y publicar (ver "Cómo verlo" más abajo).

Todavía falta poner el número de WhatsApp real de Marta (formato internacional, sin espacios ni "+"), un poco más
abajo en el mismo archivo:

```js
const WHATSAPP_NUMERO = 'PON_AQUI_EL_NUMERO'; // ej: '34600000000'
```

Mientras ese valor tenga el texto `PON_AQUI...`, la web avisa con un mensaje en vez de abrir un enlace roto — así
nunca se queda "silenciosamente" rota si alguien pulsa el botón antes de terminar la configuración.

### Sobre la política de privacidad

Tanto la web como las descripciones de arriba mencionan "mi política de privacidad", pero de momento no existe
ninguna. Como Marta trata datos relacionados con salud/bienestar emocional, antes de publicar esto de cara a
clientas reales conviene tener un texto básico de privacidad (qué datos se piden, para qué se usan, cuánto se
guardan) — no hace falta que sea complejo, pero sí que exista. No es algo que deba resolver el código; coméntalo
con Marta o con quien lleve su gestoría/asesoría para tenerlo listo antes de compartir el enlace.

## Qué NO hace

No es un sistema a medida con base de datos propia: toda la lógica de disponibilidad, confirmación, recordatorios y
cancelación la lleva Google Calendar. Eso es intencionado — significa menos piezas que puedan fallar y cero
mantenimiento técnico para Marta. Si en el futuro hace falta algo que Google Calendar no cubre (por ejemplo,
recordatorios automáticos por WhatsApp), habría que añadir una integración aparte (Zapier, Make, o un pequeño
backend).

## Cómo verlo

Es un único archivo `index.html` sin build. Puedes:

- Abrirlo directamente en el navegador.
- Publicarlo en [GitHub Pages](https://pages.github.com/) (Settings → Pages → Deploy from branch → `main` / `/root`).
- Arrastrarlo a [Netlify Drop](https://app.netlify.com/drop).
