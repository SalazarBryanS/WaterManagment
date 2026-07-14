# Proceso Actual (AS-IS)

## Objetivo

Este documento describe el proceso actual utilizado por el administrador del condominio para calcular el consumo mensual de agua de cada vivienda, distribuir el costo total del servicio y generar los recibos correspondientes.

La finalidad de este documento es comprender el flujo de trabajo actual, identificar los procesos manuales y detectar oportunidades de automatización que serán consideradas durante el desarrollo del sistema.

---

# Actores

Los actores involucrados en el proceso son:

- Administrador del condominio.
- Municipalidad (Proveedor del servicio de agua).
- Propietarios de las viviendas.

Actualmente el condominio está conformado por **23 viviendas**.

---

# Descripción del proceso actual

## 1. Recepción de la factura del servicio de agua

Una vez al mes, el administrador del condominio recibe en el correo electrónico oficial del condominio la factura correspondiente al servicio de agua emitida por la Municipalidad.

La factura contiene información relevante para el proceso de facturación interna, entre ella:

- Período de facturación.
- Consumo total del condominio (m³).
- Monto total a pagar.

Actualmente esta información es consultada manualmente y posteriormente ingresada en un archivo de Microsoft Excel.

---

## 2. Captura de las lecturas de los medidores

En la fecha de corte del período de facturación, el administrador recorre las 23 viviendas del condominio para registrar el consumo de agua de cada una.

Para cada vivienda se realiza el siguiente procedimiento:

1. Se observa el medidor de agua.
2. Se toma una fotografía del medidor como evidencia de la lectura.
3. Se agrega manualmente el número de la vivienda sobre la fotografía para facilitar su identificación posterior.
4. Las fotografías son enviadas a un grupo de WhatsApp con el objetivo de mantener un respaldo de todas las lecturas realizadas.

Las fotografías constituyen el respaldo oficial utilizado para validar cualquier consulta o reclamo relacionado con una lectura.

---

## 3. Registro de las lecturas

El administrador mantiene un archivo de Microsoft Excel que almacena el historial de consumo de todas las viviendas.

Cada período de facturación corresponde a una hoja independiente dentro del mismo archivo, cuyo nombre generalmente corresponde al mes de facturación.

Ejemplo:

- Enero
- Febrero
- Marzo
- Abril

Una vez obtenidas todas las fotografías, el administrador revisa cada una de ellas e ingresa manualmente la lectura correspondiente en la fila de la vivienda respectiva.

---

## 4. Cálculo del consumo mensual

Después de registrar las nuevas lecturas, el archivo de Excel realiza automáticamente los cálculos necesarios para determinar el consumo mensual de cada vivienda.

Entre los cálculos realizados se encuentran:

- Lectura anterior.
- Lectura actual.
- Diferencia entre ambas lecturas.
- Consumo mensual en metros cúbicos.

---

## 5. Distribución del costo del servicio

Posteriormente el administrador ingresa manualmente en el archivo de Excel la información obtenida de la factura de la Municipalidad.

Los datos ingresados corresponden a:

- Consumo total del condominio (m³).
- Monto total a pagar.

A partir de estos datos, el archivo de Excel calcula automáticamente:

- El porcentaje de consumo correspondiente a cada vivienda.
- El monto que debe cancelar cada propietario.

---

## 6. Generación de los recibos

Una vez verificados todos los datos, el administrador guarda el archivo de Excel y ejecuta un script desarrollado en Python.

El script solicita únicamente:

- La ubicación del archivo Excel.
- El nombre de la hoja correspondiente al período de facturación.

Como resultado, el script genera automáticamente un archivo PDF para cada una de las viviendas del condominio.

---

## 7. Distribución de los recibos

Los archivos PDF generados son enviados inicialmente a un grupo de WhatsApp como respaldo.

Posteriormente, el administrador envía manualmente el recibo correspondiente a cada propietario utilizando WhatsApp.

---

# Herramientas utilizadas actualmente

Actualmente el proceso utiliza las siguientes herramientas:

- Correo electrónico (recepción de la factura).
- Cámara del teléfono celular.
- WhatsApp.
- Microsoft Excel.
- Script desarrollado en Python para la generación de los recibos en formato PDF.

---

# Limitaciones del proceso actual

Durante el análisis del proceso se identifican las siguientes limitaciones:

- La descarga de la factura desde el correo electrónico se realiza manualmente.
- El monto total y el consumo total de la factura deben ingresarse manualmente en el archivo de Excel.
- La lectura de los medidores se transcribe manualmente desde las fotografías.
- La identificación de cada fotografía se realiza agregando manualmente el número de la vivienda.
- Las fotografías y las lecturas no se encuentran centralizadas en un único sistema.
- El historial depende del archivo de Microsoft Excel.
- El envío de los recibos por WhatsApp se realiza manualmente para cada propietario.

---

# Oportunidades de mejora

Con base en el análisis del proceso actual, se identifican oportunidades para automatizar diferentes etapas del flujo de trabajo, entre ellas:

- Obtención automática de la factura desde el correo electrónico.
- Extracción automática de la información contenida en la factura.
- Captura digital de las fotografías desde una aplicación web.
- Asociación automática entre la fotografía y la vivienda correspondiente.
- Lectura automática de los medidores mediante técnicas de OCR.
- Almacenamiento centralizado de la información en una base de datos.
- Generación automática de los recibos.
- Envío automatizado de los recibos mediante WhatsApp.
- Consulta del historial de consumo por vivienda.