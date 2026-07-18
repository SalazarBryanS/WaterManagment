# Modelo Lógico

El modelo lógico representa la estructura que tendrá la base de datos antes de su implementación física.

En esta etapa se definen las entidades con sus atributos, las claves primarias (Primary Keys), las claves foráneas (Foreign Keys) y las relaciones entre ellas, sin considerar aún aspectos específicos del motor de base de datos como tipos de datos, índices o restricciones de implementación.

El modelo lógico constituye la transición entre el análisis del negocio y el diseño físico de la base de datos.

---

## Rol

**Descripción**

Representa los diferentes niveles de permisos que pueden asignarse a los usuarios del sistema.

**Atributos**

- PK id
- nombre
- descripcion

---

## Usuario

**Descripción**

Representa las personas que pueden acceder al sistema.

**Atributos**

- PK id
- nombre
- correo
- contraseña
- activo
- FK rol_id

---

## Condominio

**Descripción**

Representa el condominio administrado por el sistema.

**Atributos**

- PK id
- nombre
- direccion

---

## Propietario

**Descripción**

Representa a la persona responsable de una o varias viviendas.

**Atributos**

- PK id
- nombre
- apellido
- telefono
- correo

---

## Casa

**Descripción**

Representa una vivienda perteneciente a un condominio.

**Atributos**

- PK id
- numero
- estado
- FK propietario_id
- FK condominio_id

---

## Periodo

**Descripción**

Representa un ciclo mensual de facturación.

**Atributos**

- PK id
- año
- mes
- fecha_inicio
- fecha_fin
- estado

---

## Factura

**Descripción**

Representa la factura emitida por el proveedor de agua correspondiente a un período.

**Atributos**

- PK id
- numero_factura
- fecha_emision
- monto_total
- consumo_total
- archivo_pdf
- FK periodo_id

---

## Lectura

**Descripción**

Representa la lectura del medidor de una vivienda durante un período.

**Atributos**

- PK id
- lectura_anterior
- lectura_actual
- consumo
- fecha_registro
- FK casa_id
- FK periodo_id

---

## Fotografía

**Descripción**

Representa la evidencia fotográfica utilizada para obtener o validar una lectura.

**Atributos**

- PK id
- ruta_archivo
- fecha_subida
- procesada
- FK lectura_id

---

## Recibo

**Descripción**

Representa el documento generado para una vivienda durante un período.

**Atributos**

- PK id
- monto
- fecha_generacion
- archivo_pdf
- FK casa_id
- FK periodo_id

---

## Envío

**Descripción**

Representa el historial de envío de un recibo mediante correo electrónico o WhatsApp.

**Atributos**

- PK id
- tipo
- fecha
- estado
- mensaje_error
- FK recibo_id
- FK job_id

---

## Job

**Descripción**

Representa una tarea pendiente que será ejecutada por el agente local del sistema.

**Atributos**

- PK id
- tipo
- estado
- fecha_creacion
- fecha_ejecucion