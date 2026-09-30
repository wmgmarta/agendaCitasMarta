# Agenda de citas — Marta R.

Página web (un único `index.html`, sin build ni backend propio) para que las clientas de Marta R. reserven sesión de
neurocoaching. Sigue la guía de marca (`Marta R.` — OrganicStudio): paleta de color, tipografía Fraunces + Inter y
los 4 pilares del acompañamiento.

## Cómo funciona

La web **no gestiona las citas ella misma** — las reservas reales se hacen en un "Horario de citas" de Google
Calendar de Marta. La web es la puerta de entrada bonita y de marca: la clienta elige el tipo de sesión y la
llevamos directamente al calendario real de Marta para que elija día y hora.

Con esto, las tres cosas que hacían falta quedan resueltas por Google (no por código nuestro, que podría fallar):

- **La cita se guarda de verdad**, en el Google Calendar de Marta, no en el navegador de la clienta.
- **Marta se entera al momento**: la cita aparece directamente en su calendario en cuanto se reserva.
- **A la clienta le llega confirmación por email**, con opción de añadirla a su propio calendario, cambiarla o
  cancelarla — todo gestionado por Google, no por nosotros.

## Configuración (hacerlo una vez, desde la cuenta de Google de Marta)

1. Entra en [Google Calendar](https://calendar.google.com) con la cuenta de Marta.
2. Pulsa **Crear** → **Horario de citas**.
3. Crea un horario por cada tipo de sesión (repite esto 3 veces). Para cada uno, copia y pega el título y la
   descripción de la tabla siguiente — la descripción ya incluye el aviso de privacidad y el recordatorio de dejar
   el teléfono:

   | | Primera sesión | Sesión de seguimiento | Sesión online |
   |---|---|---|---|
   | **Título** | Primera sesión — Marta R. | Sesión de seguimiento — Marta R. | Sesión online — Marta R. |
   | **Duración** | 75 min | 50 min | 50 min |
   | **Ubicación** | (tu dirección de consulta) | (tu dirección de consulta) | Videollamada — activa "Añadir Google Meet" |
   | **Descripción** | Conversación inicial para conocernos. Cuéntame en las notas qué te trae por aquí y déjame tu teléfono si quieres el recordatorio por WhatsApp. Tus datos se usan únicamente para gestionar tu cita, conforme a mi política de privacidad. | Continuamos tu proceso. Si quieres, déjame tu teléfono en las notas para el recordatorio por WhatsApp. Tus datos se usan únicamente para gestionar tu cita, conforme a mi política de privacidad. | Sesión por videollamada — el enlace te llegará en la confirmación. Si quieres, déjame tu teléfono en las notas para el recordatorio por WhatsApp. Tus datos se usan únicamente para gestionar tu cita, conforme a mi política de privacidad. |

   Además, en cada horario:
   - En **"Formulario de reserva"**, activa el campo de teléfono si está disponible; si no, activa "Notas
     adicionales" (el texto de arriba ya le pide a la clienta que apunte ahí su teléfono).
   - Define los días y horas en los que Marta está disponible, y el margen mínimo de antelación para reservar
     (por ejemplo, mínimo 12h y máximo 60 días vista).
4. Una vez creado cada horario, pulsa **Compartir** → **Copiar enlace de reservas**. Ese enlace es el que hay que
   pegar en el código (ver siguiente paso).
5. Abre [`index.html`](index.html) y, cerca del final del archivo, sustituye los tres enlaces de ejemplo:

   ```js
   const ENLACES_RESERVA = {
     primera: 'https://calendar.app.google/PON_AQUI_EL_ENLACE_PRIMERA_SESION',
     seguimiento: 'https://calendar.app.google/PON_AQUI_EL_ENLACE_SEGUIMIENTO',
     online: 'https://calendar.app.google/PON_AQUI_EL_ENLACE_ONLINE',
   };
   ```

   por los tres enlaces reales copiados en el paso 4.
6. Justo debajo, pon el número de WhatsApp real de Marta (formato internacional, sin espacios ni "+"):

   ```js
   const WHATSAPP_NUMERO = 'PON_AQUI_EL_NUMERO'; // ej: '34600000000'
   ```

7. Guarda, haz commit y publica los cambios (ver "Cómo verlo" más abajo).

Mientras estos valores tengan el texto `PON_AQUI...`, la web avisa con un mensaje en vez de abrir un enlace roto —
así nunca se queda "silenciosamente" rota si alguien lo intenta reservar antes de terminar la configuración.

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
