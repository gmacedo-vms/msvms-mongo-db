### MongoDB

**Nota:** El acceso a la base de datos local de mongo se realiza por Windows Terminal y no tiene clave.

> show dbs

Lista las bases de datos ubicadas en el servidor

> db

Muestra el nombre de la base de datos a la que se encuentra conectado.

> use [nombre-bd]

Crea la base de datos con el nombre indicado. Tener en cuenta que si la base de datos no tiene información no se mostrará con el comando **show dbs**.
También este comando permite cambiar entre base de datos (solo para mongo shell).

> db.[nombre-colecction].insert([documento-formato-json]);

Crea una colección y a la vez inserta dentro del mismo un documento el cual tiene que estar en formato JSON.

```
db.estudiante.insert(
  {
    "Nombre": "Pedro",
    "Genero": "Masculino",
    "Edad": 18,   
    "Fecha": new Date()
  }
);
```

> db.[nombre-colecction].insertOne([documento-formato-json]);

La ejecución del insertOne devuelve el estado de la ejecución y el identificador creado 

```
{
  acknowledged: true,
  insertedId: ObjectId("62e307c948fa1e32ab4340ea")
}
```

> db.[nombre-colecction].insertMany([documento-formato-json], [documento-formato-json], ...);

Permite la inserción de varios documentos en una sola declaración,

```
db.estudiant2e.insertMany(
  {
    "Nombre": "Pablo",
    "Genero": "Masculino",
    "Edad": 18,   
    "Fecha": new Date()
  },
  {
    "Nombre": "Fernando",
    "Genero": "Femenino",
    "Edad": 21,   
    "Fecha": new Date()
  }
);
```
**Nota:** Al insertar documentos se recomienda que se indique la llave **_id**, si no se indica este valor mongodb colocará uno por defecto.

> db.[nombre-colecction].insertOne([document-json-*document-json*]);

Inserción de un documento dentro de otro documento.

```
var estudios = {"Primaria": true, "Secundaria": true, "Tecnico": false};
db.estudiante.insertOne(
  {
    "Nombre": "Pedro",
    "Genero": "Masculino",
    "Edad": 18,   
    "Fecha": new Date(),
    estudios
  }
);
```

> show collections;

Lista las colecciones dentro de la base de datos.

> db.[name-collection].find(); | db.getCollection('[name-collection]").find(); | db.[name-collection].find().pretty();

Lista todos los documentos de la colección y muestra todos los valores.

> db.[name-collection].find([where-document-json]);

Lista todos los documentos de la colección que cumplan con los criterios indicados y muestra todos los valores.

> db.[name-collection].find([where-document-json], [keys-json]);

Lista todos los documentos de la colección que cumplan con los criterios indicados y muestra los valores indicados [keys-json]

> db.[nombre-colecction].findOne();

La variante findOne trae el primer registro que coincida con el criterio ingresado, si este es vacío devuelve el primer documento.
**Nota:** También aplica los mismo filtros utilizados por **find**

> db.[name-collection].remove({"_id": [document-id]}); | db.[name-collection].remove({"_id": ObjectId("[document-id])});

El resultado devuelto será.
```
{ acknowledged: true, deletedCount: 1 }
```
> db.[nombre-colecction].drop()

Elimina la collection

> db.[nombre-colecction].save([variable]);

```
var datos = db.[nombre-colecction].findOne([where-document-json]);
datos;
datos.Nombre = "[new-value]";
datos.CampoNuevo = "[new-value]";
datos.Parientes = [document-json];
datos;
db.[name-collection].save(datos);
```
**Nota:** En caso el documento (variable) con los nuevos datos no tiene coincidencia con algún documento, se registra en la collection.

> db.[nombre-colecction].update("_id": [document-id], [variable]);

```
var datos = db.[nombre-colecction].findOne([where-document-json]);
datos;
datos.Nombre = "[new-value]";
datos.CampoNuevo = "[new-value]";
datos.Parientes = [document-json];
datos;
db.[name-collection].update({"Nombre": "Juan"}, datos);
```

> $set
> db.[nombre-colecction].update("_id": [document-id], {"$set": [document-json]});

```
db.[name-collection].update({"Nombre": "Juan"}, {"$set": {"Estado": "Soltero"}});
```
**Nota:** Si el valor, variable o documento que se envía como parámetro a **set** no existe, se añadirá como una nueva llave y valor, caso contrario actualiza el que existe.

> $inc
> db.[nombre-colecction].update("_id": [document-id], {"$inc": [document-json-numeric]});

```
db.[name-collection].update({"Nombre": "Juan"}, {"$set": {"Edad": "10"}});
```

> $gte | maypr igual que 
> db.[nombre-colecction].find([document-json(Key: {"$gte": value-conditional"})]);

>$gt | mayor que
> db.[nombre-colecction].find([document-json(Key: {"$gt": value-conditional"})]);

>$lt | menor que
> db.[nombre-colecction].find([document-json(Key: {"$lt": value-conditional"})]);

> db.[nombre-colecction].find([document-json(Key: {"$gt": value-conditional", "$lt": value-conditional"})]);

> $lte | menor igual que
> db.[nombre-colecction].find([document-json(Key: {"$lte": value-conditional"})]);

> db.[nombre-colecction].find([document-json(Key: {"$gte": value-conditional", "$lte": value-conditional"})]);

> db.estudiante.getIndexes();

> db.estudiante.createIndex({"Nombre":1}); -- 1 : valores se ordenen de forma ascendente

> db.estudiante.createIndex({"Nombre":1}, {unique:true}); --índice único

> db.estudiante.createIndex({"Nombre":1}, {background:true}); --índice único

Creación de usuarios
En Robot 3T, clic derecho en la bd , Selsscionar agregar usuario y brindar los permisos.

> db.getUser('[name-user]');

Consejos de diseño de base de datos no relacional

### ¿Cuando utilizar NoSQL?

Si se desaea mantener la integridad de la información, utiliza SQL.
Si la prioridad es mostrar información, consultas, lecturas, sistemas en tiempo real, utiliza NoSQL.

### Tips

Las collectiones de datos deben estar creadas en plural
Si no se indica el nombre para la collection, tomará el nombre de la clase para el nombre de la collection, lo mismo sucede que los campos de la collection 
mongobd no trabaja con un generador o id numerico, genera uno alfanumerico del tipo String
Las collection no se muestran cuando estas se encuentran vacias, sino que se muestran cuando almacenan informacion
JPQL no no se utiliza en MongoDB, ya que esto es para base de datos relacionales. Se utiliza pares y llaves para ser especificos con la consulta; también se puede utilizar la palabra reservada FindBy









