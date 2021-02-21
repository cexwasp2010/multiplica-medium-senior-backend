# multiplica-medium-senior-backend
Reto para evaluar skills de desarrollo.

Pasos para configurar el api:

1. Crear en api-code/config un archivo llamado auth_credentials.rb con las siguientes lineas: 
ENV['user_token'] = "vURjXbANsTEvaSf5vQ5GVg8h"
ENV['admin_token'] = "irizREhyoG6Ejwr4AcjsQME9"

Este archivo es importante para que se puedan consumir los métodos de GET, PUT, POST y DELETE por el administrador

2. Dirigirse a api-code y ejecutar el comando: rake db:migrate para que se creen las tablas necesarias para el proyecto en la base de datos sqlite3.

3. Dentro de la carpeta raíz del api "api-code" ejecutar el comando rails s para iniciar el servidor y poder hacer las solicitudes a la url: localhost:3001/colores

Nota: Para consumir el método listado de colores es importante agregar los pámatros item_per_pag y respond_type como se muestra en este ejemplo: "localhost:3001/colores&item_per_pag=6?respond_type=json"


