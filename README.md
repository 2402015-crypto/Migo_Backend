
---

# MIGO Backend

Backend de MIGO construido con **Node.js**, **Express**, **MySQL2**, **CORS** y **Multer**. Expone una API REST para usuarios, publicaciones, veterinarias, reseñas, comentarios y catálogos base.

## Tecnologías

- Node.js
- Express.js
- MySQL2
- CORS
- Multer

## Estructura

```text
backend/
├── server.js
├── package.json
├── README.md
├── sql/
│   ├── scripdatabasenueva.sql
│   └── inserts.sql
└── uploads/
```

## Configuración local

1. Instala dependencias:

```bash
npm install
```

2. Crea la base de datos ejecutando primero `sql/scripdatabasenueva.sql` y después `sql/inserts.sql`.

3. Revisa la conexión en `server.js`.

La conexión actual está configurada con estos valores fijos:

```js
host: 'localhost'
user: 'root'
password: ''
database: 'migo_db_VUE'
```

4. Inicia el servidor:

```bash
npm start
```

El backend escucha en `http://localhost:4000`.

## API base

Todas las rutas viven bajo `/api`.

### Archivos

- `GET /uploads/:archivo` sirve los archivos cargados en la carpeta `uploads/`.

### Usuarios

- `POST /api/usuarios` crea un usuario.
- `GET /api/usuarios/:id` obtiene el perfil de un usuario.
- `PUT /api/usuarios/:id_usuario` actualiza el perfil de un usuario.
- `POST /api/login` autentica usuarios con rol `usuario`.

Ejemplo de cuerpo para crear usuario:

```json
{
  "nombre": "Ana",
  "apellido": "López",
  "correo": "ana@mail.com",
  "contrasena": "123456",
  "telefono": "5551234567",
  "direccion": "Centro",
  "id_colonia": 1,
  "rol": "usuario"
}
```

### Veterinarias

- `POST /api/login-vet` autentica usuarios con rol `veterinario`.
- `POST /api/registro-vet` registra un usuario veterinario y su veterinaria en una transacción.
- `GET /api/veterinarias` lista veterinarias simples.
- `GET /api/veterinarias/detallado` lista veterinarias con horarios y servicios.
- `GET /api/veterinaria/:id` obtiene una veterinaria simple.
- `GET /api/veterinaria/:id/detallado` obtiene una veterinaria con horarios y servicios.
- `PUT /api/veterinarias/:id` actualiza datos generales de la veterinaria.
- `POST /api/veterinarias/:id/logo` sube y guarda el logo de la veterinaria.
- `GET /api/horarios/:idVet` obtiene horarios de una veterinaria.
- `PUT /api/horarios/:idVet` reemplaza o actualiza horarios por día.
- `GET /api/dias-semana` obtiene el catálogo de días.
- `GET /api/servicios` obtiene el catálogo de servicios.
- `POST /api/servicios` crea un servicio.
- `POST /api/vet-servicios/:idVet` asigna servicios a una veterinaria.
- `GET /api/vet-servicios/:idVet` obtiene los servicios asignados a una veterinaria.
- `GET /api/resenas/:id` obtiene reseñas de una veterinaria.
- `POST /api/resenas` publica una reseña.
- `PUT /api/resenas/:id` edita una reseña.
- `DELETE /api/resenas/:id` elimina una reseña.

### Publicaciones

- `GET /api/publicaciones` lista publicaciones con información relacionada.
- `POST /api/publicaciones` crea una publicación.
- `PUT /api/publicaciones/:id_publi` edita una publicación validando que pertenezca al usuario.
- `POST /api/fotos/:id_publi` sube una imagen asociada a una publicación con el campo `foto`.

### Comentarios

- `GET /api/comentarios/:id_publi` obtiene comentarios de una publicación.
- `POST /api/comentarios` publica un comentario.
- `PUT /api/comentarios/:id_comentario` edita un comentario validando el `id_usuario`.
- `DELETE /api/comentarios/:id_comentario/:id_usuario` elimina un comentario validando el autor.

### Catálogos

- `GET /api/colonias`
- `GET /api/especies`
- `GET /api/tipos_publi`

## Esquema de base de datos

El proyecto usa la base `migo_db_VUE` y estas tablas principales:

- `colonias`
- `tipos_publi`
- `estados_publi`
- `especies`
- `servicios`
- `dias_semana`
- `usuarios`
- `veterinarias`
- `publicaciones`
- `fotos_publi`
- `resenas`
- `horarios_vet`
- `vet_servicios`
- `comentarios`
- `logs`

## Notas importantes

- El backend no usa variables de entorno en la configuración actual; la conexión a BD está declarada directamente en `server.js`.
- El puerto está fijado en `4000`.
- Las imágenes se guardan en `uploads/` y se publican como archivos estáticos.
- El endpoint de login de usuario solo permite el rol `usuario`; el de veterinaria solo permite el rol `veterinario`.

## Autor

Proyecto desarrollado por Bryan Martínez Jiménez.