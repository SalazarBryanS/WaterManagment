# Proceso Futuro (TO-BE)

## Objetivo

El objetivo del sistema es automatizar el proceso completo de administración del consumo de agua del condominio, reduciendo al mínimo la intervención manual del administrador y centralizando toda la información en una única plataforma.

El sistema permitirá administrar las viviendas del condominio, registrar las lecturas de los medidores, procesar automáticamente la factura mensual del servicio de agua, generar los recibos individuales y distribuirlos automáticamente a cada propietario.

---

# Objetivos del sistema

El sistema deberá permitir:

- Centralizar toda la información del condominio.
- Automatizar la mayor cantidad posible de procesos.
- Mantener un historial completo de todas las operaciones.
- Reducir errores ocasionados por procesos manuales.
- Facilitar el trabajo del administrador.
- Permitir futuras ampliaciones del sistema.

---

# Flujo General

El sistema estará compuesto por una aplicación web accesible desde cualquier dispositivo con acceso a Internet.

Toda la información será almacenada en una base de datos centralizada.

Los documentos y fotografías serán almacenados en un servicio de almacenamiento en la nube.

Algunas tareas automáticas serán ejecutadas por un Agente de Automatización que inicialmente se ejecutará desde una computadora personal.

---

# 1. Inicio de sesión

Todo usuario deberá autenticarse antes de ingresar al sistema.

Cada usuario contará con:

- Correo electrónico o número de teléfono.
- Contraseña.

El sistema identificará automáticamente el rol del usuario para habilitar únicamente las funcionalidades correspondientes.

Inicialmente existirán los siguientes roles:

- Administrador
- Desarrollador
- Usuario

Cada rol contará con diferentes permisos dentro del sistema.

---

# 2. Dashboard

Después de iniciar sesión, el usuario visualizará un panel principal con el estado general del sistema.

El Dashboard mostrará información como:

- Estado de la factura del mes.
- Cantidad de viviendas registradas.
- Estado de las lecturas.
- Cantidad de recibos generados.
- Cantidad de recibos enviados.
- Trabajos pendientes.
- Última sincronización del sistema.

Este panel permitirá conocer rápidamente el estado del proceso mensual.

---

# 3. Procesamiento automático de la factura

El sistema revisará periódicamente el correo electrónico oficial del condominio.

Cuando se detecte una nueva factura del servicio de agua:

- Descargará automáticamente el archivo adjunto.
- Almacenará el documento original en la nube.
- Extraerá automáticamente la información relevante.
- Registrará la información en la base de datos.

Entre los datos que podrán extraerse se encuentran:

- Fecha de emisión.
- Período de facturación.
- Consumo total.
- Monto total.
- Número de factura.
- Fecha de vencimiento.

El administrador podrá modificar manualmente cualquier dato en caso de ser necesario.

---

# 4. Administración de períodos de facturación

El sistema permitirá consultar el historial completo de todos los períodos registrados.

Para cada período será posible visualizar:

- Mes.
- Año.
- Consumo total.
- Monto total.
- Estado del período.
- Fecha de creación.

El administrador podrá crear, editar o corregir la información del período.

---

# 5. Administración de viviendas

El sistema permitirá administrar toda la información correspondiente a cada vivienda.

Cada vivienda podrá almacenar información como:

- Número de vivienda.
- Propietario.
- Teléfono.
- Correo electrónico.
- Estado.
- Observaciones.

El administrador podrá:

- Registrar viviendas.
- Editar información.
- Eliminar viviendas.
- Consultar el historial completo de consumo.

---

# 6. Registro de lecturas

Para cada período de facturación el administrador registrará la lectura correspondiente a cada vivienda.

El sistema mostrará una lista de todas las viviendas.

Para cada una será posible:

- Subir una fotografía del medidor.
- Ejecutar automáticamente OCR.
- Detectar la lectura del medidor.
- Mostrar el resultado obtenido.
- Permitir la corrección manual antes de guardar.

Una vez validada la información:

- La fotografía será almacenada en la nube.
- La lectura será registrada en la base de datos.
- Se asociará automáticamente con la vivienda y el período correspondiente.

---

# 7. Cálculo automático del consumo

Una vez registradas todas las lecturas y procesada la factura del proveedor, el sistema calculará automáticamente:

- Consumo mensual de cada vivienda.
- Porcentaje del consumo total.
- Monto correspondiente a cada propietario.

Todos los cálculos serán almacenados para futuras consultas.

---

# 8. Generación de recibos

El administrador podrá generar los recibos correspondientes al período seleccionado.

El sistema generará automáticamente un archivo PDF para cada vivienda.

Cada recibo contendrá la información correspondiente al propietario.

Los archivos generados serán almacenados automáticamente.

---

# 9. Distribución de recibos

Una vez generados los recibos, el sistema permitirá enviarlos automáticamente utilizando los medios configurados.

Inicialmente se contempla el envío mediante:

- WhatsApp.
- Correo electrónico.

Cada propietario recibirá únicamente la información correspondiente a su vivienda.

El sistema registrará el resultado de cada envío.

---

# 10. Historial

El sistema conservará un historial completo de:

- Facturas.
- Lecturas.
- Fotografías.
- Consumos.
- Recibos generados.
- Recibos enviados.

Toda la información permanecerá disponible para futuras consultas.

---

# 11. Agente de Automatización

Existirá un componente independiente denominado **Agente de Automatización**.

Su objetivo será ejecutar automáticamente tareas que requieran una computadora local.

Inicialmente el agente se ejecutará desde la computadora del desarrollador.

Entre sus responsabilidades estarán:

- Detectar trabajos pendientes.
- Descargar archivos necesarios.
- Enviar automáticamente los recibos por WhatsApp.
- Enviar automáticamente los recibos por correo electrónico.
- Actualizar el estado de cada tarea en la base de datos.

Durante la primera versión el agente funcionará desde una terminal (consola), mostrando en tiempo real el progreso de cada operación.

En versiones futuras podrá evolucionar hacia una aplicación de escritorio con interfaz gráfica.

---

# 12. Estado de las tareas

Cada proceso automático del sistema será tratado como una tarea.

Cada tarea podrá encontrarse en alguno de los siguientes estados:

- Pendiente.
- En proceso.
- Completada.
- Error.

Esto permitirá conocer en todo momento el estado del sistema.

---

# 13. Notificaciones

El sistema deberá informar al administrador cuando ocurran eventos importantes.

Ejemplos:

- Factura recibida.
- OCR completado.
- Recibos generados.
- Recibos enviados.
- Errores durante el procesamiento.
- Trabajos pendientes.

---

# Seguridad

El sistema deberá garantizar que:

- Solo usuarios autenticados puedan acceder.
- Cada usuario visualice únicamente la información permitida según su rol.
- Todas las operaciones importantes queden registradas.
- El historial de modificaciones permanezca disponible para auditoría.

---

# Escalabilidad

Aunque inicialmente el sistema será utilizado por un único condominio con 23 viviendas, la arquitectura deberá diseñarse de manera que permita, en el futuro:

- Administrar múltiples condominios.
- Incrementar la cantidad de viviendas.
- Incorporar nuevos métodos de envío.
- Integrar nuevos módulos sin modificar la arquitectura principal.