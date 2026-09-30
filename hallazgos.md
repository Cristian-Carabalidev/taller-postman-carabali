# Hallazgos
| # | Petición        | Código esperado | Código obtenido | ¿Coincide?  |
|---|-----------------|-----------------|-----------------|-------------|
| 1 | GET /posts/1    |  200            | 200             | Si          |
| 2 | GET /posts      |  200            | 200             | Si          |
| 3 | GET /posts/9999 |  404            | 404             | Si           |
| 4 | POST /posts     | 201             | 201             | Si           |
| 5 | PUT /posts/1    |  200            | 200             | Si           |
| 6 | PATCH /posts/1  | 200             | 200             | Si           |
| 7 | DELETE /posts/1 | 204             | 200             | No          |

#### Lee un recurso y la colección completa
En Get /posts/1 llego un solo objeto con los campos UserId,id,tittle,body, en la petición Get /posts/ llegaron 100 objetos con los mismos campos, el codigo estado de cada uno es 200.

¿En qué se diferencian los criterios de aceptación cuando pides un recurso y cuando pides una colección?
Cuando se pide un solo recurso el criterio de éxito es puntual se valida que el objeto que llego sea exactamente el correcto con sus campos correspondientes.

Cuando se pide una colección, el criterio ya cambia por que ya no es sobre un dato unico si no sobre un conjunto, ya se validan más cosas como si vino la cantidad correspondientes de elemento, si todos tienen la misma estructura y si el arreglo esta correcto. 

#### Provoca un error a propósito
¿Este caso de prueba pasó o falló?
Paso el caso de prueba por que cuando se hizo el Get /posts se evaluo que el id maximo era 100 entonces ya se esperaba que esa prueba iba dar ese resultado.

¿qué pasaría si esa misma petición hubiera devuelto 200 con un cuerpo vacío?
¿Sería un defecto?
Ya seria un defecto por que el criterio es un id que es inexistente entonces debe devolver 404, si en algun caso devuelve 200 eso haria pensar que el recurso existe cuando en realidad no.

#### Crea un recurso con POST
¿qué observaste?
Se observo que al enviar la misma petición POST varias veces seguidad el campo Id se mantuvo siempre en 101 sin incrementarse.

¿Por qué crees que ocurre eso?
Porque JSONPlaceholder es una API de prueba que simula las respuestas, pero no tiene una base de datos real detrás que recuerde los posts en peticiones anteriores.

¿Cómo comprobarías, en una API real, que el recurso se creó de verdad?
Haría una petición GET al id que devolvió el POST (por ejemplo, GET /posts/101) para confirmar que el recurso realmente existe y persiste en el servidor. Si el GET también devuelve el objeto creado, confirmo que sí se guardó de verdad; si devuelve 404, sabría que el POST no persistió el dato aunque haya respondido con éxito

#### La diferencia entre PUT y PATCH
¿Qué diferencia encontraste entre ambas respuestas?
Al enviar solo el campo "title" en ambas peticiones, la respuesta de PUT únicamente trajo los campos "title" e "id", perdiendo los campos "userId" y "body" que el post original tenía. En cambio, la respuesta de PATCH trajo el objeto completo: "userId", "id", "title" (ya actualizado) y "body" (sin cambios). Esto confirma que PUT reemplaza el recurso completo con lo que se envía, mientras que PATCH solo modifica los campos indicados y conserva el resto intacto.

¿Cuál usarías para corregir un error de escritura en un solo campo, y por qué?
Usaría PATCH, porque solo actualiza el campo específico que necesito corregir sin afectar el resto del recurso. Si usara PUT para corregir un solo campo, correría el riesgo de perder los demás datos del recurso (como pasó con "userId" y "body" en esta prueba), ya que PUT espera que envíes el recurso completo, no solo el campo a modificar.

Respuesta PUT:
{
    "title": "Titulo actualizado con PUT",
    "id": 1
}

Respuesta PATCH:
{
    "userId": 1,
    "id": 1,
    "title": "Titulo actualizado con PATCH",
    "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
}

#### Encuentra el límite
¿cómo se llama ese tipo de caso de prueba?
Este tipo de caso de prueba se llama prueba de valores límite, consiste en probar justo en el borde de un rango válido, el último valor que funciona y el primero que ya no.
¿Por qué se dice que los defectos se concentran ahí?
Los defectos se concentran ahí porque los errores de programación más comunes ocurren justamente en las condiciones que definen los límites de un rango. Probar valores muy alejados del límite raramente detecta este tipo de error; solo se detecta probando exactamente en el borde.

#### Explora otros recursos
Get /users
https://jsonplaceholder.typicode.com/users
Codigo: 200
Campos: id, name, username,email,address,street,suite,city,zipcode, geo, lat, lng
Get /albums
https://jsonplaceholder.typicode.com/albums
Codigo: 200
Campos: UserId,id,tittle
GET /posts/1/comments (ruta anidada)
https://jsonplaceholder.typicode.com/posts/1/comments
Codigo: 200
Campos: PostId,id,name,email,body
#### Escribe tu primera prueba automática
¿Por qué es importante ver una prueba fallar antes de confiar en ella?
Porque si nunca se ve fallar, no hay forma de saber si realmente está verificando algo o si simplemente siempre da verde sin comprobar nada . Al forzarla a fallar a propósito y confirmar que se pone en rojo, se demuestra que la prueba sí detecta problemas reales, y solo entonces se puede confiar en que un resultado verde significa que la respuesta realmente cumplió lo esperado.

#### Escribe tus propias pruebas
**Verifica que existe el campo title:** 
```javascript
pm.test("La respuesta contiene el campo title", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property("title");
});
```
**Verifica que el tiempo de respuesta sea menor a 1000ms:**
```javascript
pm.test("El tiempo de respuesta es menor a 1000ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(1000);
});
```
**Verifica que el campo id sea de tipo numero:**
```javascript
pm.test("El campo id es de tipo numero", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.id).to.be.a("number");
});
```


