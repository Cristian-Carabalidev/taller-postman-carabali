# Conclusiones
## Idempotencia
Un método HTTP es idempotente cuando ejecutarlo una vez o varias veces seguidas produce el mismo resultado final en el servidor.

De los 5 métodos:
- GET: idempotente (solo lee datos, nunca cambia el servidor)
- PUT: idempotente (reemplaza el recurso completo; repetirlo dos veces deja el mismo resultado que una sola vez)
- DELETE: idempotente (borrar algo que ya no existe da el mismo resultado que borrarlo la primera vez)
- POST: NO idempotente (cada ejecución está pensada para crear un recurso nuevo)
- PATCH: generalmente NO idempotente (depende de la implementación)


Al repetir la petición PUT /posts/1 tres veces, la respuesta fue exactamente la misma en cada intento:
{
    "title": "Titulo actualizado con PUT",
    "id": 1
}

Al repetir la petición POST /posts tres veces, el id de la respuesta se mantuvo siempre en 101. Aunque esto se debe a que JSONPlaceholder no persiste datos reales, en una API real cada ejecución de POST crearía un recurso nuevo y distinto, lo que demuestra que POST no es idempotente, repetirlo no da el mismo resultado que ejecutarlo una sola vez.

Fuentes: (https://developer.mozilla.org/en-US/docs/Glossary/Idempotent)

#### Las cabeceras de la respuesta
Content-Type:indica qué tipo de dato viene en el cuerpo de la respuesta. Es importante al probar una API porque le dice al cliente cómo debe interpretar los datos recibidos si esta cabecera fuera incorrecta, el cliente no podría procesar la respuesta correctamente aunque los datos en si estuvieran bien.
Cache-Control:Indica si la respuesta se puede guardar en memoria temporal (caché) y por cuánto tiempo, para no tener que pedirle lo mismo al servidor una y otra vez.
Server:Identifica qué software o tecnología está corriendo del lado del servidor que respondió la petición,es util para pruebas y depuración porque  da una pista de la tecnología detrás de la API.

Fuente: (https://developer.mozilla.org/es/docs/Web/HTTP/Headers)


