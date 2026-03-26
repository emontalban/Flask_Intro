# Entorno virtual
Creamos una carpeta y dentro de ella ejecutamos las siguente instruciones

 - Para crearlo   
 `pipenv install --python 3`
 - Para activar el entorno  
 `pipenv shell`
 - Para ejecutar el programa  
 `pipenv run python 'nombre_del_archivo.py'`

## Añadir librerias
- Instalar Flask-SQLAlchemy  
`pipenv install Flask-SQLAlchemy`
- Instalar flask-marshmallow  
`pipenv install flask-marshmallow` 
- Instalar marshmallow-sqlalchemy  
`pipenv install marshmallow-sqlalchemy`


## Crear app.sqlite
Desde la terminal  entramos en python y ejecutamos las siguientes instrucciones
```
>>> from app import db  
>>> from app import app  
>>> with app.app_context():  
...    db.create_all()  
```
## Eliminar archivos de VS code despues de haberlos subido a Git hub
Si has subido los archivos y despues has creado .gitignore para solucionarlo  
` git rm -r --cached .vscode`  
y despues actualizas el repositorio  
```
git add .  
git commit -m "Eliminar .vscode del repo"  
git push  
```


## Instalar MongoDB en Windows

- **1. Descargar el instalador**  
Ve a la página oficial de descargas: MongoDB Community Download.  
https://www.mongodb.com/try/download/community  
En la sección de "Software Version", elige la más actual.  
En "Platform", selecciona Windows.  
Asegúrate de que el "Package" sea msi.  
Haz clic en Download.  

- **2. Proceso de Instalación**  
Ejecuta el archivo .msi descargado y sigue estas instrucciones en las ventanas que aparecerán:  
Acepta los términos: Haz clic en Next y acepta la licencia.  
Tipo de instalación: Elige "Complete" (es la más sencilla para empezar).  
Service Configuration: Deja marcadas las opciones por defecto:  
Install MongoDB as a Service: Esto hace que MongoDB se inicie solo cada vez que prendas tu PC.  
Run service as Network Service user.  
Instalar MongoDB Compass: ¡Muy importante! Asegúrate de que esta casilla esté marcada. MongoDB Compass es la interfaz gráfica que te permitirá ver tus bases de datos sin usar comandos.  
Haz clic en Install.
 
- **3. Configurar las Variables de Entorno (PATH)**  
Para poder usar el comando mongod o herramientas de terminal desde cualquier carpeta, debes añadir la ruta al sistema:  
Busca en tu computadora la carpeta bin de MongoDB. Normalmente está en:  
C:\Program Files\MongoDB\Server\7.0\bin (la versión puede variar).  
Copia esa ruta.  
En el buscador de Windows escribe: "Editar las variables de entorno del sistema".  
Haz clic en el botón Variables de entorno.  
En la lista de abajo ("Variables del sistema"), busca la que se llama Path y dale a Editar.  
Haz clic en Nuevo y pega la ruta que copiaste.  
Dale a Aceptar en todas las ventanas.  

- **4. Verificar la instalación**
Abre una terminal (CMD o PowerShell) y escribe:
```Bash
mongod --version
```
Si te responde con información de la versión, MongoDB está instalado.

- **5. MongoDB Shell (mongosh)**  
A partir de la versión 6.0, MongoDB ya no incluye la terminal de comandos (mongo.exe) en el instalador principal. Si quieres usar la terminal para escribir consultas, debes bajar el MongoDB Shell:  
Ve a https://www.mongodb.com/try/download/shell.  
Descarga el archivo Zip.    
Descomprímelo y copia el archivo mongosh.exe dentro de la carpeta bin que configuramos en el paso 3 (la de Program Files).    
Si escribes`mongosh` en tu terminal, entrarás a la consola de la base de datos.  

   - `show dbs` Para ver las base de datos que tienes  
   - `use 'nombre de la bbdd' ` crea una base de datos pero no la va a reconocer hasta que agregemos datos puedo usar `db` despues ya que cree un objeto.
   - `db.createUser({'user'})` para crear un usuario
   - `db.getUser('user') o db.getUsers()` para ver un usario o todos
   - `db.dropUser('user')` borra un usuario  
   - `db.createCollection('collection')` se crea las colecciones ('tablas' en SQL)  
   - `show collections` muestra las colecciones
   - `db.books.find()` para buscar todos los datos dentro de un coleccion (books es el nombre de la colecion) 
   - `db.books.find({name: "OOP Programming"})` pasandole un dato en concreto. 

   Ejemplo create:
   ```bash
   db.createUser({ user: 'Hexe', 
               pwd:'password',
               customData:{startDate:new Date()},
                 roles:[
                     {role: 'clusterAdmin', db: 'admin'},
                     {role: 'readAnyDatabase', db: 'admin'},
                     'readWrite'
                 ]
     })
   ```
   Ejemplo insert un documento
   ```bash
   db.books.insert({ "name": "OOP Programming", 
               "startDate": new Date(),
                "author": [
                     {"name": "Greg Stabilo"}                 
                 ]
    })
   ```
   Inserta varias objetos a al vez
   ```bash
   db.books.insertMany([
    {
        "name": "Python",
        "publishedDate": new Date(),
        "author": [
            { "name": "Guido van Rossum" }
        ]
    },
    {
        "name": "JavaScript",
        "publishedDate": new Date(),
        "author": [
            { "name": "Brendan Eich" }
        ]
    }  
  ])

   ```

   Para encontrar un documentos dentro de la coleccion pero que te devuelva solo los datos solicitados, para ello hay que crear otro objeto para que te devuelva solo los que quiere para ello  le pones un numero 1 y si no quieres que salga no se ponen excepto el _id que tienes que pasarle un cero para que no aparezca es el unico.

   ```bash
  db.books.find(
    {
        name: "Python"
    },
    {
        _id: 0,
        name: 1,
        author: 1
    }
  )
   ```
Tenemos varias librerias y para que nos de solo la primera usamos $slice con uno saca el uno con 2 saca 2 y con los negativos tambien pero empezando por detras
   ```bash
   db.languages.find(
    {
        name: "Java"
    },
    {
        year:1,
        creator:1,
        name:1,
        libraries:{$slice: 2}
    }
)
   ```
   Esto esta obsoleto
   Para borrar usamos `remove()`
   `db.books.remove({name:"OOP Programming"})` borra todos los items que haya.
   `db.books.remove({name:"OOP Programming"}, 1)` si le pasamos un segundo parametro borra los que le indiquemos en este caso uno

   Para borrar uno usamos `deleteOne` y para borrar muchos `deleteMany`

   Para actualizar se usa `updateOne`
   ```bash
   db.languages.updateOne(
        { name: "Java" },
        {
            $set: {
            versions: [
                { version: "8", release_year: 2014 },
                { version: "11", release_year: 2018 },
                { version: "17", release_year: 2021 }
            ]
            }
        }
    )
   ```
Y ahora queremos solo las versiones no el año para que solo nos de las versiones sera_
```bash
db.languages.find(
   { name: "Kotlin" },
   { 
      name: 1,
      "versions.version" :1
   }
)
```
Una colección en MongoDB es:

Un conjunto de documentos relacionados que se almacenan dentro de una base de datos.  
- Colección → agrupa datos (equivale a una tabla en SQL)
- Documentos → cada elemento dentro de la colección  
- Campos → los datos de cada documento

La funcion `pretty()` sirve para mostrar los datos ordenados cuando te los devuelve en una sola linea




