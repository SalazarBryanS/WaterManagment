# 05. Diseño de la Base de Datos

## Objetivo

Antes de implementar la base de datos es necesario comprender qué información debe almacenar el sistema. Para ello se identifican las entidades, sus atributos y posteriormente las relaciones entre ellas.

---

# Identificación de entidades

Una entidad representa un objeto o concepto del negocio sobre el cual el sistema necesita almacenar información de forma permanente.

Generalmente se identifican analizando los sustantivos presentes en los requerimientos y respondiendo preguntas como:

- ¿Qué información necesita recordar el sistema?
- ¿Qué objetos existen dentro del negocio?
- ¿Qué elementos poseen identidad propia?

---

# Identificación de atributos

Los atributos representan las características o propiedades de una entidad.

Se identifican preguntando:

- ¿Qué información necesito conocer de esta entidad?
- ¿Qué datos debo almacenar sobre ella?

---

# Entidades identificadas

## Usuario

Representa las personas que pueden acceder al sistema.

Atributos principales:

- id
- nombre
- correo
- contraseña
- activo

---

## Rol

Define los permisos asignados a cada usuario.

Atributos principales:

- id
- nombre
- descripción

---

## Condominio

Representa el conjunto residencial administrado por el sistema.

Atributos principales:

- id
- nombre
- dirección

---

## Casa

Representa una vivienda dentro del condominio.

Atributos principales:

- id
- número
- estado

---

## Propietario

Representa a la persona responsable de una o varias viviendas.

Atributos principales:

- id
- nombre
- apellido
- teléfono
- correo

---

## Período

Representa un ciclo mensual de facturación.

Atributos principales:

- id
- año
- mes
- fecha_inicio
- fecha_fin
- estado

---

## Factura

Representa la factura emitida por el proveedor de agua.

Atributos principales:

- id
- número_factura
- fecha_emisión
- monto_total
- consumo_total
- archivo_pdf

---

## Lectura

Representa la lectura del medidor de una casa durante un período.

Atributos principales:

- id
- lectura_anterior
- lectura_actual
- consumo
- fecha_registro

---

## Fotografía

Representa la imagen del medidor utilizada para obtener la lectura mediante OCR.

Atributos principales:

- id
- ruta_archivo
- fecha_subida
- procesada

---

## Recibo

Representa el documento generado para cada vivienda.

Atributos principales:

- id
- monto
- fecha_generación
- archivo_pdf

---

## Envío

Representa el registro de envío de un recibo.

Atributos principales:

- id
- tipo
- fecha
- estado
- mensaje_error

---

## Job

Representa una tarea pendiente que será ejecutada por el agente local.

Atributos principales:

- id
- tipo
- estado
- fecha_creación
- fecha_ejecución

---

# Relaciones entre entidades

Una vez identificadas las entidades y sus atributos, el siguiente paso consiste en determinar cómo se relacionan entre sí.

Una relación representa la forma en que dos entidades interactúan dentro del negocio.

Para descubrir las relaciones es recomendable analizar nuevamente los requerimientos y formular preguntas como:

- ¿Quién pertenece a quién?
- ¿Quién utiliza a quién?
- ¿Quién genera a quién?
- ¿Puede una entidad tener varias instancias relacionadas con otra?
- ¿La relación es uno a uno, uno a muchos o muchos a muchos?

Por ejemplo:

"Cada propietario puede tener varias casas."

De esta oración podemos identificar que existe una relación entre las entidades **Propietario** y **Casa**.

Otro ejemplo:

"Cada casa registra una lectura cada mes."

Aquí identificamos una relación entre **Casa** y **Lectura**.

El análisis de este tipo de reglas permite construir el modelo de datos antes de implementar la base de datos.

---

# Cardinalidad de las relaciones

Las relaciones pueden clasificarse según la cantidad de registros asociados entre dos entidades.

## Uno a Uno (1:1)

Cada registro de una entidad se relaciona con un único registro de la otra entidad.

Ejemplo:

Una factura electrónica podría tener un único archivo PDF.

---

## Uno a Muchos (1:N)

Un registro de una entidad puede estar relacionado con muchos registros de otra entidad.

Ejemplo:

Un propietario puede tener varias casas.

Cada casa solamente pertenece a un propietario.

---

## Muchos a Muchos (N:M)

Un registro puede relacionarse con varios registros de otra entidad y viceversa.

Ejemplo:

Un estudiante puede matricular muchos cursos.

Un curso puede tener muchos estudiantes.

Este tipo de relación normalmente requiere una tabla intermedia.

En WaterManagement actualmente no se identifica ninguna relación de este tipo.

---

# Relaciones identificadas

## Rol → Usuario

Un rol puede estar asignado a muchos usuarios.

Cada usuario posee un único rol.

Cardinalidad:

1 : N

---

## Condominio → Casa

Un condominio posee múltiples casas.

Cada casa pertenece únicamente a un condominio.

Cardinalidad:

1 : N

---

## Propietario → Casa

Un propietario puede ser responsable de varias casas.

Cada casa tiene un propietario activo.

Cardinalidad:

1 : N

---

## Período → Factura

Cada período posee una única factura del proveedor.

Cada factura pertenece únicamente a un período.

Cardinalidad:

1 : 1

---

## Período → Lectura

Durante un período se registran múltiples lecturas.

Cada lectura pertenece únicamente a un período.

Cardinalidad:

1 : N

---

## Casa → Lectura

Cada casa registra múltiples lecturas a lo largo del tiempo.

Cada lectura pertenece únicamente a una casa.

Cardinalidad:

1 : N

---

## Lectura → Fotografía

Cada lectura puede tener una fotografía asociada como evidencia.

Cada fotografía pertenece únicamente a una lectura.

Cardinalidad:

1 : 1

---

## Casa → Recibo

Cada casa tendrá un recibo por cada período.

A lo largo del tiempo una casa acumulará muchos recibos.

Cardinalidad:

1 : N

---

## Período → Recibo

Durante un período se genera un recibo para cada casa.

Cardinalidad:

1 : N

---

## Recibo → Envío

Un recibo puede enviarse varias veces.

Por ejemplo:

- reenvío por correo
- reenvío por WhatsApp
- reintento después de un error

Cardinalidad:

1 : N

---

## Job → Envío

Un trabajo ejecutado por el agente puede generar uno o varios envíos.

Cardinalidad:

1 : N

---

# Claves Primarias (Primary Keys)

Una clave primaria identifica de forma única cada registro de una tabla.

Sus características principales son:

- Nunca se repite.
- No puede ser nula.
- Identifica un único registro.
- Cada tabla posee una única clave primaria.

En este proyecto todas las entidades utilizarán un campo llamado **id** como clave primaria.

Ejemplos:

Usuario
- id

Rol
- id

Casa
- id

Propietario
- id

Lectura
- id

Factura
- id

Recibo
- id

---

# Claves Foráneas (Foreign Keys)

Una clave foránea es un atributo que referencia la clave primaria de otra tabla.

Su propósito es mantener la integridad de la información y representar las relaciones entre entidades.

Por ejemplo:

La tabla Casa necesita conocer quién es su propietario.

En lugar de almacenar nuevamente el nombre, correo y teléfono del propietario, solamente almacena su identificador.

Ejemplo:

Casa

- id
- numero
- propietario_id

El atributo **propietario_id** hace referencia al **id** de la tabla Propietario.

---

# Foreign Keys del proyecto

## Usuario

- rol_id → Rol.id

---

## Casa

- condominio_id → Condominio.id
- propietario_id → Propietario.id

---

## Factura

- periodo_id → Periodo.id

---

## Lectura

- casa_id → Casa.id
- periodo_id → Periodo.id

---

## Fotografía

- lectura_id → Lectura.id

---

## Recibo

- casa_id → Casa.id
- periodo_id → Periodo.id

---

## Envío

- recibo_id → Recibo.id
- job_id → Job.id

---

# Modelo Entidad-Relación (ERD)

El **Entity Relationship Diagram (ERD)** o **Diagrama Entidad-Relación** es una representación gráfica del modelo de datos.

Su objetivo es mostrar:

- Las entidades del sistema.
- Sus atributos principales.
- Las relaciones entre ellas.
- La cardinalidad de cada relación.

El ERD sirve como plano antes de implementar la base de datos y facilita comprender la estructura completa del sistema.

---

# ERD del proyecto

```text
Rol
 │
 └───────< Usuario


Condominio
 │
 └───────< Casa >──────── Propietario
               │
               │
               ├────────< Lectura >──────── Período ─────── Factura
               │               │
               │               └──────── Fotografía
               │
               └────────< Recibo >──────── Período
                               │
                               └────────< Envío >──────── Job
```

Donde:

- `>` representa el lado "muchos".
- La ausencia de `>` representa el lado "uno".

Este diagrama constituye el primer modelo lógico de la base de datos y servirá como referencia para la implementación de las tablas en PostgreSQL.