# multiplica-medium-senior-backend
Reto para evaluar skills de desarrollo.

Author: Cesar Augusto Córdoba Bermúdez
Date: 2021-02-23
email: cesar.warrior@hotmail.com.

Descripción:

Esta es una aplicación que permite la administración de los colores que se van a estandarizar para páginas web, nuevos diseños y redes sociales por medio de una parte backend de tipo APIREST que expone los servicios GET /colores para obtener todos los colores creados, GET /colores/:id para obtener un color especifico, POST /colores para crear un nuevo color, PUT /colores/:id para actualizar un color especifico y DELETE /colores/:id para eliminar un color especifico. el atributo :id es de tipo integer y hace referencia al identificador con el cual fue creado el color en la base de datos. Y por medio de otra parte frontend de tipo aplicación WEB que permite acceder al administrador con los perfiles de usuario y administrador para crear, acutalizar, eliminar o listar los colores consumiendo el servicio del api.

Tecnologías utilizadas:

El proyecto consta de una carpeta llamada api-code donde se encuentra el código del API que expone los servicios del controlador "colores", éste fue creado con Ruby on Rails, ruby version 2.7.0, rails version 6.0.3.5, se utilizaron las gemas sqlite3 en versión 1.4 para la base de datos y kaminari para la paginación del index. 
La otra carpeta de la que consta el proyecto es una llamada admin-code donde se encuentra el código de la app que consume los servicios y permite el acceso a los perfiles de administrador y usuario para consultar y administrar la información contenida en el api, ésta fue creada con Ruby on Rails, ruby version 2.7.2, rails version 6.1.3, se utilizarion las gemas sqlite3 version 1.4 para la administración de la base de datos, rest-client para realizar el consumo de los servicios expuestos por el api y devise para administrar los perfiles de los usuarios que se registran a la plataforma. También se instalo bootstrap 4 para dar formato de manera responsive a los formularios y el CRUD en general.

Importante! Para que la aplicación funcione correctamente es necesario que los servidores, tanto el api como de la aplicación, esten ejecutandose localmente (siguiendo los pasos detallados más abajo) 

********************************************************************************************
Pasos para configurar e iniciar el api:

1. Crear en api-code/config un archivo llamado auth_credentials.rb con las siguientes lineas: 
ENV['user_token'] = "vURjXbANsTEvaSf5vQ5GVg8h"
ENV['admin_token'] = "irizREhyoG6Ejwr4AcjsQME9"

Este archivo es importante para que se puedan consumir los métodos de GET, PUT, POST y DELETE por el administrador

2. Dirigirse a api-code y ejecutar el comando: rake db:migrate para que se creen las tablas necesarias para el proyecto en la base de datos sqlite3.

3. Ejecute el comando 'rails db:seed' para crear los datos de prueba en la base de datos local.

4. Ejecute el comando 'bundle i' para instalar las gemas (dependencias) necesarias para que se pueda correr la aplicación.

5. Dentro de la carpeta raíz del api "api-code" ejecutar el comando rails s para iniciar el servidor y poder hacer las solicitudes a la url: localhost:3001/colores

Nota: Para consumir el método listado de colores es importante agregar en el header los pámatros, sin comillas, items (número de resultados por página), page (número de la página que desea) y type ("xml" o "json") como se muestra en este ejemplo: 

$http({method: 'GET', url: 'localhost:3001/colores', headers: {
  'page': 1, 'items': 9, 'type': json}
});

Si se envía el parámetro 'type': xml no se tiene en cuenta los demás parámetros para páginación.
Si no se envía el parámetro type el servicio retorna la respuesta como json por defecto.

*******************************************************************************************
Pasos para configurar e iniciar el administrador:

1. Dirigirse a admin-code y ejecutar el comando: rake db:migrate para que se creen las tablas necesarias para el proyecto en la base de datos sqlite3.

2. Ejecute el comando 'bundle i' para instalar las gemas (dependencias) necesarias para que la aplicación se pueda ejecutar.

3. Ejecute el comando 'rails db:seed' para crear los datos de prueba en la base de datos local.
se crean dos usuarios de prueba:

Administrador => email: admin@test.com, password: 123456
Usuario => email: user@test.com, password: 123456

4. Dentro de la carpeta raíz del api "admin-code" ejecutar el comando rails s para iniciar el servidor y poder acceder con los usuarios creados en el anterior paso por medio de la url: localhost:3000/users/sign_in ó localhost:3000

Al loguearse la apliación redirige al usuario al listado (index) de los colores, conforme al wireframe adjuntado en el reto, en la parte inferior izquierda de esa patalla se encuntra el botón "Nuevo color" que le permite al administrador ingresar al formulario de creación de color, este botón no se muestra para el usuario solo al administrador.

En el listado se muestran los cuadros de color gris con los datos de los colores, al dar click sobre cada uno se accede al show (detalle) del color seleccionado.

Una vez dentro del show del color puede ejecutar las acciones de edición y eliminación del mismo cuando se encuentra en el perfil de administrador.

Si ya está logueado como uno de los usuarios y desea probar el otro perfil es necesario dar click en el boton de logout que se encuentra en la parte superior derecha de la pantalla.