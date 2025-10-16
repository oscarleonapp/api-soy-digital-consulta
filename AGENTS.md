# Repository Guidelines

## Project Structure & Module Organization
- `index.html` contiene el layout completo: HTML semántico, estilos embebidos y lógica JavaScript para consumir el endpoint de validación de cédulas.
- Centraliza las referencias a credenciales de prueba y valores `bot_script_id`; coloca ajustes adicionales (por ejemplo, endpoints alternativos) dentro de utilidades/autocomplete en la sección `<script>` para mantener la configuración en un solo archivo.
- Mantén los assets autoproducidos (capturas, documentación) fuera de la raíz o dentro de carpetas con prefijo `_docs/` para evitar mezclarlos con el artefacto desplegable.

## Build, Test, and Development Commands
- `php -S localhost:8080` (raíz del repo): sirve el HTML con HTTPS off y permite pruebas locales sin restricciones de CORS de archivo.
- `python -m http.server 8080` es una alternativa ligera cuando PHP no está disponible.
- `npx prettier@latest --write index.html` formatea el archivo único siguiendo un estilo consistente antes de abrir un PR.

## Coding Style & Naming Conventions
- Usa indentación de dos espacios en HTML, CSS y JS; evita tabulaciones para que los diffs sean claros.
- Prefiere `const` y funciones flecha para utilidades; mantiene helpers puros cerca del bloque donde se consumen.
- Sigue el patrón actual de nombres en mayúsculas para claves devueltas por el API (`CEDULA`, `NOMBRE`) y camelCase para variables locales (`btnSend`, `payloadPreview`).

## Testing Guidelines
- Realiza una prueba manual positiva con una cédula válida (por defecto `00300858230`) y confirma que `bot_script_id` coincide con el valor configurado de éxito.
- Ejecuta un caso negativo ajustando `bot_script_id_not_found` o introduciendo una cédula inexistente para validar mensajes y estados.
- Comprueba tiempos de respuesta y manejo de errores simulando timeouts mediante valores bajos en el campo `Timeout`.

## Commit & Pull Request Guidelines
- Escribe mensajes cortos en modo imperativo (ej. `Ajusta manejo de timeout`); agrega contexto adicional en el cuerpo si introduces nuevas dependencias o credenciales temporales.
- Incluye en el PR: propósito funcional, capturas o clips si cambian flujos de UI, y pasos manuales para validar en un entorno local.
- Referencia tickets o incidencias internas (`Refs #123`) y señala riesgos de seguridad cuando se modifiquen endpoints o credenciales.

## Security & Configuration Tips
- Mantén las credenciales de prueba visibles solo en entornos controlados; documenta cualquier reemplazo productivo en el PR.
- Valida siempre nuevos endpoints en HTTPS y actualiza la alerta del botón “Tip local” con instrucciones acordes al despliegue.
