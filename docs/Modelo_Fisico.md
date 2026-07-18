# 07. Modelo Físico

## Objetivo

El modelo físico describe cómo será implementada la base de datos en PostgreSQL.

En esta etapa se definen los tipos de datos, las restricciones de cada columna, las claves primarias, las claves foráneas, los índices y las convenciones que utilizará la base de datos.

Este modelo constituye la última etapa del diseño antes de comenzar la implementación mediante sentencias SQL.

---

# Motor de Base de Datos

El sistema utilizará PostgreSQL como motor de base de datos relacional debido a las siguientes características:

- Código abierto.
- Alto rendimiento.
- Soporte para integridad referencial.
- Compatibilidad con transacciones ACID.
- Excelente integración con FastAPI mediante SQLAlchemy.
- Amplio soporte para índices y optimización de consultas.

---

# Convenciones de Nombres

Para mantener consistencia en toda la base de datos se utilizarán las siguientes convenciones.

## Tablas

- Singular.
- Minúsculas.
- Separación mediante guion bajo (_).

Ejemplos

usuario

rol

casa

propietario

lectura

factura

recibo

---

## Columnas

- Minúsculas.
- snake_case.

Ejemplos

fecha_creacion

numero_factura

lectura_actual

propietario_id

---

## Claves Primarias

Todas las tablas utilizarán una columna llamada:

id

---

## Claves Foráneas

Las claves foráneas utilizarán el formato:

<tabla>_id

Ejemplos

rol_id

propietario_id

casa_id

periodo_id

recibo_id

---

# Tipos de Datos

Los siguientes tipos de datos serán utilizados en el proyecto.

| Tipo PostgreSQL | Uso |
|-----------------|-----|
| UUID | Identificadores únicos |
| VARCHAR(n) | Texto corto |
| TEXT | Texto largo |
| INTEGER | Valores enteros |
| NUMERIC(10,2) | Valores monetarios |
| BOOLEAN | Valores verdadero o falso |
| DATE | Fechas |
| TIMESTAMP | Fecha y hora |
| BYTEA o ruta del archivo | Archivos si se almacenan localmente (en este proyecto solo se almacenará la ruta al archivo en Google Drive) |

---

# Restricciones

La base de datos utilizará las siguientes restricciones para garantizar la integridad de la información.

## PRIMARY KEY

Identifica de forma única cada registro.

Ejemplo

id

---

## FOREIGN KEY

Representa la relación entre dos tablas.

Ejemplo

propietario_id → propietario.id

---

## NOT NULL

Impide almacenar valores nulos.

Se utilizará en los campos obligatorios.

Ejemplos

nombre

correo

numero

fecha_emision

---

## UNIQUE

Impide almacenar valores duplicados.

Ejemplos

correo del usuario

numero_factura

---

## CHECK

Permite validar reglas de negocio.

Ejemplos

consumo >= 0

monto_total > 0

mes BETWEEN 1 AND 12

---

## DEFAULT

Permite asignar un valor automáticamente.

Ejemplos

activo = TRUE

fecha_creacion = CURRENT_TIMESTAMP

---

# Índices

Para mejorar el rendimiento de las consultas se crearán índices sobre las columnas utilizadas con mayor frecuencia en búsquedas y relaciones.

Índices recomendados:

- propietario_id
- casa_id
- periodo_id
- recibo_id
- rol_id
- fecha_emision
- fecha_registro

---

# Estrategia para Identificadores

Todas las tablas utilizarán UUID como clave primaria.

Ventajas:

- Evita colisiones entre registros.
- Facilita la sincronización entre sistemas.
- Mayor seguridad al no utilizar identificadores consecutivos.
- Escalable para futuras integraciones.

---

# Eliminación de Registros

Como política general, los registros históricos no serán eliminados físicamente.

En su lugar se utilizará un atributo como:

activo

o

estado

para indicar si un registro continúa vigente.

Esto permitirá conservar el historial completo del sistema.

---

# Archivos

Los archivos PDF y las fotografías no serán almacenados directamente dentro de PostgreSQL.

La base de datos únicamente almacenará:

- nombre del archivo
- ruta
- identificador del archivo en Google Drive
- fecha de carga

Los archivos físicos permanecerán almacenados en Google Drive.

---

# Auditoría

Las tablas principales podrán incorporar los siguientes campos para facilitar el seguimiento de cambios.

fecha_creacion

fecha_actualizacion

usuario_creacion

usuario_actualizacion

Estos campos permitirán conocer cuándo y quién realizó una modificación.

---

# Próximo Paso

Una vez definido el modelo físico, el siguiente paso consistirá en implementar la base de datos mediante sentencias SQL.

Se crearán las tablas utilizando la instrucción CREATE TABLE, definiendo sus columnas, restricciones, claves primarias, claves foráneas e índices de acuerdo con el diseño establecido en este documento.