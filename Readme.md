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