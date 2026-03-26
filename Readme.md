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
 
3. Configurar las Variables de Entorno (PATH)
Para poder usar el comando mongod o herramientas de terminal desde cualquier carpeta, debes añadir la ruta al sistema:

Busca en tu computadora la carpeta bin de MongoDB. Normalmente está en:

C:\Program Files\MongoDB\Server\7.0\bin (la versión puede variar).

Copia esa ruta.

En el buscador de Windows escribe: "Editar las variables de entorno del sistema".

Haz clic en el botón Variables de entorno.

En la lista de abajo ("Variables del sistema"), busca la que se llama Path y dale a Editar.

Haz clic en Nuevo y pega la ruta que copiaste.

Dale a Aceptar en todas las ventanas.

4. Verificar la instalación
Abre una terminal (CMD o PowerShell) y escribe:

Bash
mongod --version
Si te responde con información de la versión, ¡felicidades! MongoDB está instalado.

5. El toque final: MongoDB Shell (mongosh)
A partir de la versión 6.0, MongoDB ya no incluye la terminal de comandos (mongo.exe) en el instalador principal. Si quieres usar la terminal para escribir consultas, debes bajar el MongoDB Shell:

Ve a MongoDB Shell Download.

Descarga el archivo Zip.

Descomprímelo y copia el archivo mongosh.exe dentro de la carpeta bin que configuramos en el paso 3 (la de Program Files).

Ahora, si escribes mongosh en tu terminal, entrarás a la consola de la base de datos.

¿Qué sigue?
Ahora que lo tienes instalado, ¿te gustaría que te enseñe cómo conectar Python con MongoDB usando la librería pymongo?