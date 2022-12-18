# Desafio 9 Curso Backend

## MongoDB

### Comenzamos:

> ( 1 ) - Para crear la base de datos:

```
use ecommerce
```

> O bien descargar la carpeta ecommerce y usar la TOOLS mongorestore y saltearse al paso N° ( 4 )

> ( 2 ) - Crear colecciones "mensajes" y "productos":

```
db.createCollection('mensajes')
db.createCollection('productos')
```

> ( 3 ) - Agregar 10 documentos con valores distintos en cada una de las colecciones:

- Agregando 10 productos a coleccion productos

```
db.productos.insertMany([{"nombre": "Escuadra", "precio":120, "foto": "https://cdn3.iconfinder.com/data/icons/education-209/64/ruler-triangle-stationary-school-256.png", "date": ISODate()},{"nombre": "Calculadora", "precio":500, "foto": "https://cdn3.iconfinder.com/data/icons/education-209/64/calculator-math-tool-school-256.pngchool-256.png", "date": ISODate()},{"nombre": "Carpeta", "precio":350, "foto": "https://cdn3.iconfinder.com/data/icons/education-209/64/calculator-math-tool-school-256.pngchool-256.png", "date": ISODate()},{"nombre": "Globo Terraqueo", "precio":850, "foto": "https://cdn3.iconfinder.com/data/icons/education-209/64/calculator-math-tool-school-256.pngchool-256.png", "date": ISODate()},{"nombre": "Goma de borrar", "precio":1300, "foto": "https://cdn3.iconfinder.com/data/icons/education-209/64/calculator-math-tool-school-256.pngchool-256.png", "date": ISODate()},{"nombre": "Tijera", "precio":1650, "foto": "https://cdn3.iconfinder.com/data/icons/education-209/64/calculator-math-tool-school-256.pngchool-256.png", "date": ISODate()},{"nombre": "Sacapuntas", "precio":2350, "foto": "https://cdn3.iconfinder.com/data/icons/education-209/64/calculator-math-tool-school-256.pngchool-256.png", "date": ISODate()},{"nombre": "Transportador", "precio":2800, "foto": "https://cdn3.iconfinder.com/data/icons/education-209/64/calculator-math-tool-school-256.pngchool-256.png", "date": ISODate()},{"nombre": "Cartulinas", "precio":4250, "foto": "https://cdn3.iconfinder.com/data/icons/education-209/64/calculator-math-tool-school-256.pngchool-256.png", "date": ISODate()},{"nombre": "Cartuchera", "precio":4900, "foto": "https://cdn3.iconfinder.com/data/icons/education-209/64/calculator-math-tool-school-256.pngchool-256.png", "date": ISODate()}])
```

- Agregando 10 mensajes a la coleccion "mensajes"

```
db.mensajes.insertMany([{"email":"persona1@prueba.com", "mensaje": "Mensaje uno", "date": ISODate()},{"email":"persona2@prueba.com", "mensaje": "Mensaje dos", "date": ISODate()},{"email":"persona1@prueba.com", "mensaje": "Mensaje uno", "date": ISODate()},{"email":"persona2@prueba.com", "mensaje": "Mensaje dos", "date": ISODate()},{"email":"persona1@prueba.com", "mensaje": "Mensaje uno", "date": ISODate()},{"email":"persona2@prueba.com", "mensaje": "Mensaje dos", "date": ISODate()},{"email":"persona1@prueba.com", "mensaje": "Mensaje uno", "date": ISODate()},{"email":"persona2@prueba.com", "mensaje": "Mensaje dos", "date": ISODate()},{"email":"persona1@prueba.com", "mensaje": "Mensaje uno", "date": ISODate()},{"email":"persona2@prueba.com", "mensaje": "Mensaje dos", "date": ISODate()}])
```

> ( 4 ) - Listar todos los documentos en cada coleccion:

```
db.productos.find() // Lista coleccion Productos
db.mensajes.find() // Listar coleccion Mensajes
```

> ( 5 ) - Mostrar la cantidad de cada coleccion:

```
db.productos.estimatedDocumentCount()
db.mensajes.estimatedDocumentCount()
```

### Realizar CRUD sobre la coleccion productos

> ( 6 ) - Agregar un producto mas en la coleccion productos:

```
db.productos.insertOne({"nombre": "Fibron", "precio": 2450, "foto":"https://cdn3.iconfinder.com/data/icons/education-209/64/calculator-math-tool-school-256.pngchool-256.png", "date": ISODate()})
```

- ( a ) - Agregar un producto mas en la coleccion productos:

```
db.productos.insertOne({"nombre": "Fibron", "precio": 2450, "foto":"https://cdn3.iconfinder.com/data/icons/education-209/64/calculator-math-tool-school-256.pngchool-256.png", "date": ISODate()})
```

- ( b ) - Realizar una consulta por nombre producto especifico:

```
db.productos.find({nombre: "Escuadra"})
```

- ( c ) - Listar los productos con precio menor a $1000:

```
db.productos.find({precio: {$lt: 1000}})
```

- ( d ) - Listar los productos con precio entre $1000 a $3000:

```
db.productos.find({$and:[{precio:{$gt:1000}},{precio: {$lt:3000}}]})
```

- ( e ) - Listar los productos con precio mayor a $3000:

```
db.productos.find({precio: {$gt: 3000}})
```

- ( f ) - Realizar una consulta que traiga solo el nombre del tercer producto mas barato:

```
db.productos.find({},{"nombre":1, "_id":0}).skip(2).limit(1).sort({precio: 1})
```

- ( g ) - Hacer una actualizacion sobre todos los productos, agregando campo "stock" a todos con valor de 100:

```
db.productos.updateMany({},{$set: {"stock":100}})
```

- ( h ) - Cambiar el stock a 0 de los productos con precio mayora $4000:

```
db.productos.updateMany({precio:{$gt:4000}},{$set: {"stock":0}})
```

- ( i ) - Borrar los productos con precio menor a $1000:

```
db.productos.deleteMany({precio:{$lt: 1000}})
```

> Crear un usuario "pepe" clave:"asd456" con permiso de lectura en la base de datos ecommerce.

```
use admin //-->Ingresamos a esa base de datos

db.createUser({user: "pepe", pwd: "asd456", roles: [{role: "read", db: "ecommerce"}]})

```

```
C:\#confidential#>mongosh -u pepe
Enter password: ****** (asd456)
Current Mongosh Log ID: #confidential#
Connecting to:          #confidential#
Using MongoDB:          6.0.3
Using Mongosh:          1.6.1

For mongosh info see: https://docs.mongodb.com/mongodb-shell/

test> show dbs
ecommerce  80.00 KiB
test> use ecommerce
switched to db ecommerce
ecommerce> db.productos.insertOne({"nombre": "Intentado agregar algo"})
MongoServerError: not authorized on ecommerce to execute command { insert: "productos", documents: [ { nombre: "Intentado agregar algo", _id: ObjectId('639e57c22625f2c76ae8ebc7') } ], ordered: true, lsid: { id: UUID("477e1e3d-7e69-447e-accc-e810d487c744") }, $db: "ecommerce" }
ecommerce>
```

Autor: Matias Sanchez
