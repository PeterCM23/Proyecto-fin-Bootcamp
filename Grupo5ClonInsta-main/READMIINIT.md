# Simple Meow API

Este ejercicio consiste en crear una API que simule el funcionamiento de una aplicación similar a Instagram oriendata a subida de contenido de gatos.

## Instalar

1. Instalar las dependencias mediante el comando `npm install` o `npm i`.
2. Guardar el archivo `.env.example` como `.env` y cubrir los datos necesarios.
3. Ejecutar `npm run initDb` para crear las tablas necesarias en la base de datos anteriormente creada(En caso de no estar creada, crear base de datos).
4. Ejecutar `npm run dev` para lanzar el servidor.

## ENTIDADES

### Users

| Campo          | Tipo     | Descripción                           |
| ----------     | -------- | ------------------------------------- |
| id             | INT      | Identificador único del usuario.      |
| username       | VARCHAR  | Nombre de usuario.                    |
| email          | VARCHAR  | Dirección de correo electrónico.      |
| password       | VARCHAR  | Contraseña del usuario.               |
| avatar         | VARCHAR  | Nombre del avatar del usuario.        |
| role           | VARCHAR  | Rol del usuario (normal o admin).     |
|registrationCode| VARCHAR  | Enlace registro enviado por email.    |
|recoveryPassCode| VARCHAR  | Código para resetear contraseña.      |
| active         | BOOLEAN  | Verificación de código de registro    |
| createdAt      | DATETIME | Fecha y hora de creación del usuario. |
| modifiedAt     | DATETIME | Fecha y hora de última modificación.  |

### Entries

| Campo     | Tipo     | Descripción                                   |
| --------- | -------- | --------------------------------------------  |
| id        | INT      | Identificador único de la entrada.            |
|description| VARCHAR  | Texto descriptivo de la entrada.              |
| userId    | INT      | Identificador del usuario que creó la entrada.|
| createdAt | DATETIME | Fecha y hora de creación de la entrada.       |
| modifiedAt| DATETIME | Fecha y hora de la modificacion de la entrada.|


### Likes

| Campo     | Tipo     | Descripción                                      |
| --------- | -------- | --------------------------------------------     |
| id        | INT      | Identificador único del like.                    |
| userId   | INT      | Identificador del usuario que dio el like.       |
| postId   | INT      | Identificador de la entrada que recibió el like. |
| createdAt | DATETIME | Fecha y hora de creación del like.               |
| update_at | DATETIME | Fecha y hora de modificación del like.           |


### Photos

| Campo     | Tipo     | Descripción                                           |
| --------- | -------- | --------------------------------------------          |
| id        | INT      | Identificador único de la foto.                       |
| entryId   | INT      | Identificador de la entrada que recibió la foto       |
| photoName | VARCHAR  | Nombre con el que se guarda la foto.                  |
| createdAt | DATETIME | Fecha y hora de creación de la subida de la foto.     |
|modifiedAt | DATETIME | Fecha y hora de modificación de la foto.              |


## Comments
| Campo     | Tipo     | Descripción                                           |
| --------- | -------- | --------------------------------------------          |
| id        | INT      | Identificador único del comentario.                   |
| entryId   | INT      | Identificador de la entrada que recibió el comentario |
| userId    | INT      | Identificador del usuario que hizo la entrada         |
|commentText| TEXT     | Comentario introducido                                |
| createdAt | DATETIME | Fecha y hora de creación de la subida de la foto.     |


## Videos
| Campo     | Tipo     | Descripción                                           |
| --------- | -------- | --------------------------------------------          |
| id        | INT      | Identificador único del video.                        |
| entryId   | INT      | Identificador de la entrada que recibió el video      |
| userId    | INT      | Identificador del usuario que hizo la entrada         |
| videoName | VARCHAR  | Nombre con el que se guarda el video.                 |
| createdAt | DATETIME | Fecha y hora de creación de la subida del video.      |
|modifiedAt | DATETIME | Fecha y hora de modificación  del video.              |


## ENDPOINTS:

### Usuarios:

-   POST `/users` - Registro de usuario.
-   POST `/users/validate/:idvalidate` - Validación de usuario.
-   POST `/users/login` - Login de usuario (devuelve token).
-   GET `/users` - Devuelve información del usuario de todos los usuarios.
-   GET `/users/:id` - Devuelve información del usuario concreto segun ID.
-   PUT `/users/avatar` - Editar el avatar.
-   PUT `/users/recover-password` - Envia correo con token de recuperación.
-   PUT `/users/reset-password` - Edita la contraseña con token + newPass.


### Entries:

-   POST `/entries` - Permite crear una entrada.
-   PUT  `/entries/:entryid` - Permite actualizar la descripción de la entrada.
-   POST `/entries/:entryid/photos` - Permite añadir una imagen a la entrada.
-   DELETE `/entries/:entryid/photos/:photoid` - Permite eliminar una imagen.
-   GET `/entries` - Lista todas las entradas.
-   GET `/entries/:entryid` - Muestra la entrada buscada por su id.
-   GET `/entries/description?description=<descripción>` - Muestra la entrada buscada por palabras en su descripción.
-   POST `/entries/:entryid/likes/add` - Añade un like a una entrada.
-   DELETE `/entries/:entryid/likes/remove` - Deshace un like de una entrada.
-   POST `/entries/:entryid/comments`  - Añade un comentario a una entrada.
-   DELETE `/entries/:entryid/comments/:commentid` - Borra un comentario a una entrada.