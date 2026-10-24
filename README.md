# Órbita — Quiz de exploración espacial

Un cuestionario interactivo en español con 10 preguntas sobre exploración
espacial. Cada respuesta muestra una explicación y actualiza la puntuación y
el progreso. Al terminar puedes repasar las preguntas falladas o volver a
intentarlo.

La interfaz es adaptable a móviles, admite temas claro y oscuro según las
preferencias del sistema y respeta la preferencia de movimiento reducido.

## Ejecutar en local

Clona este repositorio y abre `index.html` directamente en un navegador moderno.
No necesitas instalar dependencias, ejecutar un servidor ni compilar nada:
el HTML, los estilos y el JavaScript están incluidos en ese archivo.

Para comprobar el funcionamiento, responde una pregunta correctamente y otra
incorrectamente, comprueba la puntuación y el progreso, completa las 10 preguntas
y pulsa **Volver a intentarlo** para verificar que se reinicia el cuestionario.

## Publicación

El sitio se publica en <https://condorcoders.github.io/space-quiz/>.

El workflow [Deploy GitHub Pages](.github/workflows/pages.yml) empaqueta
`index.html` como un artefacto estático en los pull requests dirigidos a `main`.
Al integrar cambios en `main`, lo despliega en GitHub Pages. También se puede
ejecutar manualmente desde **Actions → Deploy GitHub Pages → Run workflow**,
seleccionando `main`.

En **Settings → Pages → Build and deployment**, la fuente debe ser
**GitHub Actions**. El despliegue utiliza el entorno `github-pages` y el
`GITHUB_TOKEN` del workflow; no requiere secretos adicionales.
