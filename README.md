# taller-postman-carabali

#### Marco Conceptual
Qué significa que una API sea «REST»: REST es un patron de de diseño de APIs en la web, que permite que 2 programas se comuniquen entre si.
Las APIs REST se basan en recursos, cada petición devuelve una lista de recursos, un recurso individual o ejecuta una acción sobre uno estas acciones son : crear,leer,actualizar,eliminar.
Las APIs REST son usadas para permitir que 2 piezas de software se comuniquen entre si.

Qué es un recurso y qué es un endpoint: Un recurso es el dato o el objeto que la API te devuelve cuando lo consultas
Un Endpoint es la URL especifica y completa donde ese recurso puede ser accedido para realizar una acción sobre el.

Un ejemplo de una aplicación que uses a diario y que dependa de APIs:
El ejemplo que eligi es Spotify ya que esta utiliza una arquitectura basada en APIs para conectar las bases de datos musicales para poder escucharla en nuestros dispositivos

Fuente: (https://www.ibm.com/mx-es/think/topics/api-endpoint) ,(https://www.contentful.com/blog/what-is-a-rest-api/)



#### Metodos HTTP y el CRUD
Método    Operación CRUD     Qué hace
GET       Read               Solicita una representacion del recurso especificado
POST      Create             Envia una entidad al recurso especificado 
PUT       Update             Reemplaza todas las representaciones actuales del recurso destino por el contenido de la petición
PATCH     Update             Aplica modificaciones parciales a un recurso
DELETE    Delete             Elimina el recurso especificado
Fuente: (https://developer.mozilla.org/es/docs/Web/HTTP/Reference/Methods)

#### Las familias de códigos de estado
1xx(informational) - la petición fue recibida y el proceso continua
2xx(Succesfull) - la petición fue recibida, entendida y aceptada con éxito
3xx(Redirection) - se necesita una acción adicional para completar la petición
4xx(Client Error) - la petición contiene una sintaxis incorrecta o no puede cumplirse
5xx(Server Error ) - el servidor falló al cumplir una petición aparentemente válida

Ejemplo: 1xx - 100 Continue
2xx - 200 OK, 201 Created
3xx -  301 Moved Permanently
4xx - 404 Not Found
5xx - 500 Internal Server Error

¿por qué se separan los errores 4xx de los 5xx? ¿Qué cambia entre unos y otros desde el punto de vista de quién tiene la culpa?
la diferencia clave es de quién es la responsabilidad del error. Un 4xx indica que el cliente cometió un error o pidió algo mal formado o inexistente. Un 5xx indica que el servidor falló al procesar una petición que en principio, estaba bien hecha entonces la responsabilidad es del backend, no de quien consume la API.

Fuente: (https://developer.mozilla.org/es/docs/Web/HTTP/Reference/Status)