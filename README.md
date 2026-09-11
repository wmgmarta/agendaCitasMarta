# Agenda de citas — Marta R.

Prototipo web (una sola página, sin backend) del flujo de reserva de citas para las sesiones de neurocoaching de Marta R. Sigue la guía de marca (`Marta R.` — OrganicStudio): paleta de color, tipografía Fraunces + Inter y los 4 pilares del acompañamiento.

## Qué hace

- Elegir tipo de sesión (primera sesión, seguimiento, online).
- Elegir día y hora entre los próximos huecos disponibles.
- Rellenar los datos de contacto y confirmar la cita.
- Ver, cambiar o cancelar la próxima cita desde "Mis citas".
- Descargar la cita como archivo `.ics` para añadirla al calendario.

Las citas se guardan en el navegador (`localStorage`), así que sobreviven a recargar la página pero no se comparten entre dispositivos.

## Qué NO hace (todavía)

Esto es un prototipo de interfaz, no un sistema de reservas real: no envía recordatorios por WhatsApp ni bloquea huecos en un calendario compartido. Para eso hace falta conectar el formulario con una herramienta real (Calendly, Google Calendar, WhatsApp Business...) o un backend propio.

## Cómo verlo

Es un único archivo `index.html` sin build. Puedes:

- Abrirlo directamente en el navegador.
- Publicarlo en [GitHub Pages](https://pages.github.com/) (Settings → Pages → Deploy from branch → `main` / `/root`).
- Arrastrarlo a [Netlify Drop](https://app.netlify.com/drop).
