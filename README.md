# 🚀 Automatización de Correos con Google Apps Script

Este repositorio contiene dos scripts desarrollados en Google Apps Script para automatizar notificaciones desde Google Sheets. Está pensado especialmente para procesar respuestas provenientes de Google Forms.

## 📦 Scripts Incluidos

El repositorio se divide en dos casos de uso principales:

### 1. Envío Individual (`Mail_por_fila.gs` / o nombre de tu archivo)

Envía un correo electrónico personalizado por cada nueva fila que entra en la hoja de cálculo.

* **Caso de uso ideal:** Enviar un certificado de asistencia, un mensaje de bienvenida o una confirmación de registro a un alumno.
* **Disparador recomendado:** `Al enviar el formulario` (On Form Submit).
* **Características:**
  * Lee los datos de la última fila añadida.
  * Personaliza el asunto y el cuerpo del correo utilizando variables (ej. Nombre, Curso, DNI).
  * Puede marcar en una columna específica (ej. "Estado") si el correo ya fue enviado para evitar duplicados.

### 2. Reporte Consolidado (`Mail_con_tabla.gs` / o nombre de tu archivo)

Recopila varias filas de la hoja de cálculo y genera una única tabla en formato HTML que se envía por correo.

* **Caso de uso ideal:** Enviar un resumen semanal o diario a la coordinación académica con todos los alumnos inscritos recientemente.
* **Disparador recomendado:** `Basado en el tiempo` (Time-driven), por ejemplo: todos los viernes a las 15:00h.
* **Características:**
  * Filtra los datos (ej. solo recoge las filas de esta semana o las que no tienen la marca de "Notificado").
  * Construye una tabla HTML con diseño limpio.
  * Envía un solo correo a una o varias direcciones de administradores.

## 🛠️ Configuración e Instalación

Para utilizar estos scripts en tu propio documento de Google Sheets, sigue estos pasos:

1. Abre la hoja de cálculo de Google donde caen las respuestas de tu formulario.
2. En el menú superior, haz clic en **Extensiones > Apps Script**.
3. Se abrirá el editor de código. Borra cualquier código existente (por defecto `function myFunction() {}`).
4. Copia y pega el código del script que desees utilizar de este repositorio.
5. Haz clic en el icono del disquete 💾 para guardar el proyecto.

## ⚙️ Personalización (Variables a modificar)

Antes de ejecutar el código, asegúrate de adaptar las variables a la estructura de tu tabla:

* **Índices de columnas:** Recuerda que en Apps Script los arrays empiezan en `0`. Si tu columna "Nombre" es la C, su índice en el código será `2`.
* **Nombres de las hojas:** Verifica si el código hace referencia a `"Respuestas de formulario 1"`. Si tu hoja tiene otro nombre, cámbialo en el código (`getSheetByName('TU_NOMBRE_DE_HOJA')`).
* **Direcciones de correo:** En el reporte consolidado, actualiza la variable de correo destino (ej. `coordinacion@tuinstitucion.edu`). En el envío individual, asegúrate de estar apuntando al índice correcto donde el alumno dejó su correo.

## ⏰ Configuración de Disparadores (Triggers)

Para que los scripts funcionen automáticamente, debes configurar los disparadores:

1. En el editor de Apps Script, ve al menú izquierdo y haz clic en el icono del reloj ⏱️ (**Disparadores**).
2. Haz clic en el botón azul abajo a la derecha: **Añadir disparador**.
3. **Para el Envío Individual:**
   * Elige la función a ejecutar (ej. `enviarCorreoIndividual`).
   * Selecciona la fuente del evento: `En la hoja de cálculo`.
   * Selecciona el tipo de evento: `Al enviar el formulario`.
4. **Para el Reporte Consolidado:**
   * Elige la función a ejecutar (ej. `enviarReporteTabla`).
   * Selecciona la fuente del evento: `Según el tiempo`.
   * Configura la frecuencia (por horas, días o semanas) según tus necesidades.
5. Guarda y autoriza los permisos de Google.

## ⚠️ Posibles Errores Comunes

* **Permisos bloqueados:** La primera vez que ejecutes el código, Google te pedirá autorizar el acceso. Debes hacer clic en *Avanzado* > *Ir a [Nombre del Script] (no seguro)*.
* **Límites de envíos:** Las cuentas gratuitas de Gmail permiten enviar hasta 100 correos diarios a través de Apps Script (1500 si es cuenta Workspace educativa/empresarial).
* **Error de índice (undefined):** Si la tabla que llega al correo tiene datos vacíos o pone `undefined`, revisa que los números de índice de las columnas coincidan con tu Google Sheet real.

---
*Creado para facilitar la gestión educativa y administrativa mediante automatización.*
