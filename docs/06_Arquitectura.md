# 08. Arquitectura del Sistema

# Objetivo

La arquitectura del sistema describe la organización general de los componentes que conforman la aplicación y la forma en que estos interactúan entre sí.

Su propósito es establecer una estructura clara antes de comenzar el desarrollo, permitiendo definir las responsabilidades de cada componente, el flujo de la información y la comunicación entre los diferentes servicios.

Una arquitectura bien definida facilita el mantenimiento, la escalabilidad y la incorporación de nuevas funcionalidades sin afectar el funcionamiento del sistema.

---

# Arquitectura General

WaterManagement estará compuesto por cinco componentes principales:

- Frontend
- Backend
- Base de Datos
- Almacenamiento de Archivos
- Agente Local

Cada componente será independiente y tendrá responsabilidades específicas.

La comunicación entre ellos se realizará mediante APIs y servicios web.

---

# Componentes del Sistema

## Frontend

Tecnología:

- React

Responsabilidad:

El frontend constituye la interfaz gráfica del sistema.

Será el encargado de permitir la interacción entre los usuarios y la aplicación.

Desde este componente los usuarios podrán:

- iniciar sesión
- administrar propietarios
- administrar casas
- registrar lecturas
- consultar consumos
- revisar facturas
- visualizar reportes
- descargar recibos

El frontend no accederá directamente a la base de datos.

Toda la información será obtenida mediante peticiones HTTP al backend.

---

## Backend

Tecnología:

- FastAPI

Responsabilidad:

El backend representa el núcleo de la aplicación.

Será responsable de implementar toda la lógica del negocio y exponer una API REST para ser consumida por el frontend y por el agente local.

Entre sus responsabilidades se encuentran:

- autenticación de usuarios
- autorización mediante roles
- validación de información
- procesamiento de lecturas
- cálculo de consumos
- generación de recibos
- comunicación con Google Drive
- creación de trabajos para el agente local
- acceso a la base de datos

El backend será el único componente autorizado para interactuar directamente con PostgreSQL.

---

## Base de Datos

Tecnología:

- PostgreSQL

Responsabilidad:

La base de datos almacenará toda la información del sistema.

Entre los datos almacenados se encuentran:

- usuarios
- roles
- condominios
- propietarios
- casas
- períodos
- lecturas
- facturas
- recibos
- historial de envíos
- trabajos pendientes

PostgreSQL garantizará la integridad referencial mediante claves primarias y claves foráneas.

---

## Almacenamiento de Archivos

Tecnología:

- Google Drive

Responsabilidad:

Los archivos generados o recibidos por el sistema no serán almacenados directamente dentro de PostgreSQL.

En Google Drive se almacenarán:

- facturas del proveedor
- fotografías de medidores
- recibos en formato PDF

La base de datos únicamente almacenará la información necesaria para localizar dichos archivos.

Por ejemplo:

- identificador del archivo
- nombre
- ruta
- fecha de carga

---

## Agente Local

Tecnología:

- Python

Responsabilidad:

El agente local será una aplicación independiente que se ejecutará en la computadora del administrador.

Su función será realizar aquellas tareas que requieren acceso a recursos locales o servicios externos.

Entre ellas:

- consultar trabajos pendientes
- enviar mensajes por WhatsApp
- enviar correos electrónicos
- actualizar el estado de los trabajos
- informar errores al backend

El agente consultará periódicamente la API para conocer las tareas pendientes.

---

# Comunicación entre Componentes

Los componentes del sistema se comunicarán mediante HTTP utilizando una API REST.

La comunicación seguirá el siguiente flujo:

Frontend

↓

Backend

↓

PostgreSQL

Cuando sea necesario acceder a archivos, el backend se comunicará con Google Drive.

Cuando exista un trabajo pendiente, el backend lo registrará en la base de datos y el agente local lo ejecutará posteriormente.

---

# Flujo General del Sistema

El funcionamiento general del sistema puede resumirse de la siguiente manera.

Administrador

↓

Frontend (React)

↓

Backend (FastAPI)

↓

PostgreSQL

↓

Respuesta al Frontend

Este flujo se utilizará para la mayoría de las operaciones del sistema.

---

# Flujo para el Registro de Lecturas

Administrador

↓

Carga fotografía del medidor

↓

Frontend

↓

Backend

↓

OCR

↓

Lectura obtenida

↓

Validación

↓

PostgreSQL

---

# Flujo para la Generación de Recibos

Factura del proveedor

↓

Backend

↓

Obtención de lecturas

↓

Cálculo del consumo

↓

Distribución del costo

↓

Generación del PDF

↓

Google Drive

↓

Registro del recibo en PostgreSQL

---

# Flujo para el Envío de Recibos

Recibo generado

↓

Backend

↓

Creación de Job

↓

PostgreSQL

↓

Agente Local

↓

Correo / WhatsApp

↓

Actualización del estado del envío

---

# Principios de Diseño

Durante el desarrollo del sistema se seguirán los siguientes principios.

## Separación de Responsabilidades

Cada componente tendrá funciones claramente definidas.

Esto facilita el mantenimiento y evita dependencias innecesarias.

---

## Escalabilidad

Cada componente podrá evolucionar de manera independiente.

Por ejemplo, será posible cambiar el frontend sin modificar el backend.

---

## Bajo Acoplamiento

Los componentes dependerán lo menos posible entre sí.

La comunicación se realizará mediante interfaces bien definidas (API REST).

---

## Alta Cohesión

Cada componente concentrará únicamente funcionalidades relacionadas con su propósito.

---

## Persistencia Centralizada

Toda la información será almacenada en PostgreSQL.

Ningún componente mantendrá información permanente fuera de la base de datos.

---

# Arquitectura General

```text
                    +----------------------+
                    |      Frontend        |
                    |        React         |
                    +----------+-----------+
                               |
                          HTTP / JSON
                               |
                               ▼
                    +----------------------+
                    |       Backend        |
                    |       FastAPI        |
                    +----+-----------+-----+
                         |           |
                         |           |
                 SQL     |           | API
                         |           |
                         ▼           ▼
              +---------------+   +----------------+
              | PostgreSQL    |   | Google Drive   |
              +---------------+   +----------------+
                         ^
                         |
                   HTTP / JSON
                         |
                         ▼
              +----------------------+
              |     Agente Local     |
              |       Python         |
              +----------------------+
```

---

# Beneficios de esta Arquitectura

La arquitectura propuesta ofrece las siguientes ventajas:

- Separación clara entre la interfaz de usuario y la lógica del negocio.
- Independencia entre los diferentes componentes.
- Facilidad para realizar mantenimiento y agregar nuevas funcionalidades.
- Mayor seguridad al centralizar el acceso a la base de datos únicamente a través del backend.
- Escalabilidad para incorporar nuevos servicios en el futuro.
- Posibilidad de reutilizar la API desde aplicaciones móviles u otros clientes.
- Mejor organización del código fuente y del proceso de desarrollo.

---

# Próximo Paso

Una vez definida la arquitectura del sistema, el siguiente paso consistirá en diseñar la API REST que permitirá la comunicación entre el frontend, el backend y el agente local.

En dicha etapa se definirán los recursos del sistema, los endpoints, los métodos HTTP, los parámetros de entrada y las respuestas esperadas para cada operación.