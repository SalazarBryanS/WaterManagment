# 09. Diseño de la API REST

# Objetivo

La API (Application Programming Interface) constituye el medio de comunicación entre el frontend, el backend y el agente local.

Su objetivo es exponer un conjunto de servicios que permitan consultar, crear, actualizar y eliminar información de manera segura y controlada.

En WaterManagement, el backend desarrollado con FastAPI actuará como el único punto de acceso a la información almacenada en PostgreSQL. Esto significa que ningún componente accederá directamente a la base de datos; todas las operaciones deberán realizarse mediante solicitudes HTTP a la API.

El diseño de la API se realiza antes de comenzar la implementación para definir claramente los recursos disponibles, las operaciones permitidas y la información que deberá intercambiarse entre los diferentes componentes del sistema.

---

# ¿Qué es una API REST?

Una API REST (Representational State Transfer) es un conjunto de reglas que permite la comunicación entre aplicaciones mediante el protocolo HTTP.

Cada recurso del sistema posee una dirección (endpoint) a la cual pueden realizarse solicitudes para consultar o modificar información.

Por ejemplo:

GET /casas

permite obtener la información de las viviendas registradas.

POST /lecturas

permite registrar una nueva lectura.

La API recibe una solicitud, procesa la información solicitada y devuelve una respuesta generalmente en formato JSON.

---

# Arquitectura de Comunicación

El flujo de comunicación será el siguiente:

Usuario

↓

Frontend (React)

↓

HTTP Request

↓

API REST (FastAPI)

↓

Lógica del Negocio

↓

PostgreSQL

↓

HTTP Response (JSON)

↓

Frontend

Toda la lógica del sistema estará concentrada en el backend.

El frontend únicamente enviará solicitudes y mostrará la información recibida.

---

# Formato de Intercambio de Información

Todas las solicitudes y respuestas utilizarán el formato JSON.

Ejemplo de respuesta:

```json
{
    "id": 5,
    "numero": 12,
    "estado": "Activa"
}
```

---

# Métodos HTTP

La API utilizará los métodos HTTP estándar.

## GET

Obtiene información.

No modifica datos.

Ejemplos:

GET /casas

GET /propietarios

GET /periodos

---

## POST

Crea nuevos registros.

Ejemplos:

POST /casas

POST /lecturas

POST /usuarios

---

## PUT

Actualiza completamente un registro existente.

Ejemplos:

PUT /casas/15

PUT /propietarios/8

---

## PATCH

Actualiza parcialmente un registro.

Se utilizará cuando únicamente sea necesario modificar algunos campos.

Ejemplo:

PATCH /usuarios/10

---

## DELETE

Elimina un registro.

En aquellos casos donde sea necesario conservar el historial se implementará eliminación lógica mediante un atributo "activo" o "estado".

Ejemplo:

DELETE /usuarios/7

---

# Recursos de la API

Los recursos representan las entidades principales del sistema.

Se utilizarán los siguientes recursos.

- usuarios
- roles
- condominios
- propietarios
- casas
- periodos
- facturas
- lecturas
- fotografias
- recibos
- envios
- jobs

Cada recurso contará con sus respectivos endpoints.

---

# Endpoints

## Usuarios

| Método | Endpoint | Descripción |
|---------|----------|-------------|
| GET | /usuarios | Obtener todos los usuarios |
| GET | /usuarios/{id} | Obtener un usuario |
| POST | /usuarios | Crear usuario |
| PUT | /usuarios/{id} | Actualizar usuario |
| DELETE | /usuarios/{id} | Eliminar usuario |

---

## Roles

| Método | Endpoint | Descripción |
|---------|----------|-------------|
| GET | /roles | Obtener roles |
| POST | /roles | Crear rol |

---

## Propietarios

| Método | Endpoint | Descripción |
|---------|----------|-------------|
| GET | /propietarios | Obtener propietarios |
| GET | /propietarios/{id} | Obtener propietario |
| POST | /propietarios | Crear propietario |
| PUT | /propietarios/{id} | Actualizar propietario |
| DELETE | /propietarios/{id} | Eliminar propietario |

---

## Casas

| Método | Endpoint | Descripción |
|---------|----------|-------------|
| GET | /casas | Obtener todas las casas |
| GET | /casas/{id} | Obtener una casa |
| POST | /casas | Registrar una casa |
| PUT | /casas/{id} | Actualizar información de la casa |
| DELETE | /casas/{id} | Eliminar casa |

---

## Períodos

| Método | Endpoint | Descripción |
|---------|----------|-------------|
| GET | /periodos | Obtener períodos |
| GET | /periodos/{id} | Obtener un período |
| POST | /periodos | Crear período |

---

## Facturas

| Método | Endpoint | Descripción |
|---------|----------|-------------|
| GET | /facturas | Obtener facturas |
| GET | /facturas/{id} | Obtener factura |
| POST | /facturas | Registrar factura |
| PUT | /facturas/{id} | Actualizar factura |

---

## Lecturas

| Método | Endpoint | Descripción |
|---------|----------|-------------|
| GET | /lecturas | Obtener lecturas |
| GET | /lecturas/{id} | Obtener lectura |
| POST | /lecturas | Registrar lectura |
| PUT | /lecturas/{id} | Modificar lectura |

---

## Fotografías

| Método | Endpoint | Descripción |
|---------|----------|-------------|
| GET | /fotografias | Obtener fotografías |
| POST | /fotografias | Subir fotografía |

---

## Recibos

| Método | Endpoint | Descripción |
|---------|----------|-------------|
| GET | /recibos | Obtener recibos |
| GET | /recibos/{id} | Obtener un recibo |
| POST | /recibos | Generar recibo |

---

## Envíos

| Método | Endpoint | Descripción |
|---------|----------|-------------|
| GET | /envios | Consultar historial |
| POST | /envios | Registrar envío |

---

## Jobs

| Método | Endpoint | Descripción |
|---------|----------|-------------|
| GET | /jobs | Obtener trabajos pendientes |
| GET | /jobs/{id} | Obtener un trabajo |
| POST | /jobs | Crear trabajo |
| PUT | /jobs/{id} | Actualizar estado |

---

# Códigos de Respuesta HTTP

La API utilizará los siguientes códigos de estado.

| Código | Significado |
|---------|-------------|
| 200 OK | Solicitud procesada correctamente. |
| 201 Created | Recurso creado correctamente. |
| 204 No Content | Operación exitosa sin contenido de respuesta. |
| 400 Bad Request | La solicitud contiene información inválida. |
| 401 Unauthorized | El usuario no está autenticado. |
| 403 Forbidden | El usuario no posee permisos suficientes. |
| 404 Not Found | El recurso solicitado no existe. |
| 409 Conflict | Existe un conflicto con la información enviada. |
| 500 Internal Server Error | Error interno del servidor. |

---

# Autenticación

Todas las operaciones que modifiquen información requerirán autenticación.

El backend verificará la identidad del usuario antes de permitir el acceso a los recursos protegidos.

Posteriormente se implementará autenticación basada en JWT (JSON Web Tokens).

---

# Validaciones

Antes de almacenar información en la base de datos, la API validará:

- tipos de datos
- obligatoriedad de los campos
- reglas de negocio
- existencia de claves foráneas
- permisos del usuario

Las solicitudes que incumplan alguna validación devolverán un código HTTP adecuado junto con un mensaje descriptivo del error.

---

# Principios de Diseño

La API seguirá los siguientes principios:

- Utilizar nombres de recursos claros y consistentes.
- Mantener una estructura uniforme en todos los endpoints.
- Separar la lógica del negocio de la interfaz de usuario.
- Utilizar códigos HTTP adecuados.
- Validar toda la información recibida.
- No exponer directamente la base de datos.
- Facilitar la reutilización de la API por futuras aplicaciones móviles o servicios externos.

---

# Próximo Paso

Una vez definido el diseño de la API, el siguiente paso será comenzar la implementación del backend utilizando FastAPI.

Se creará la estructura del proyecto, la conexión con PostgreSQL, los modelos de datos, los esquemas de validación y los primeros endpoints definidos en este documento.