# Guía para Conectar con un Servidor MQTT Online con Adafruit

Esta guía detalla los pasos para configurar y conectar un PLC S7-1200 con un servidor MQTT online utilizando la librería MQTT de Siemens y Adafruit IO como broker.

> ℹ️ **Nota**: Este ejemplo utiliza **TIA Portal V19** y un controlador **S7-1200**.

## Tabla de Contenidos
- [Introducción](#introducción)
- [Descarga e Instalación de la Librería MQTT](#descarga-e-instalación-de-la-librería-mqtt)
- [Configuración del Bloque MQTT en TIA Portal](#configuración-del-bloque-mqtt-en-tia-portal)
- [Configuración de la Cuenta en Adafruit IO](#configuración-de-la-cuenta-en-adafruit-io)
- [Integración del PLC con Adafruit IO](#integración-del-plc-con-adafruit-io)
- [Conclusión](#conclusión)
- [Referencias](#referencias)

---

## Introducción
En esta guía, aprenderás a:
1. Descargar y configurar la librería MQTT para controladores Siemens.
2. Configurar bloques y parámetros en TIA Portal.
3. Crear una cuenta y configurar feeds en Adafruit IO.
4. Integrar el PLC con el servidor MQTT de Adafruit IO.

---

## Descarga e Instalación de la Librería MQTT
1. Descarga la librería MQTT desde el sitio oficial de Siemens:
   - [Enlace a la librería MQTT](https://support.industry.siemens.com/cs/document/109780503/libraries-for-communication-for-simatic-controllers?dti=0&lc=en-ES)
   - **Nota**: Asegúrate de descargar la versión compatible con TIA Portal V19.
   
   ![Descarga de la librería MQTT](#)

2. Una vez descargada, extrae el contenido del archivo ZIP.

3. Abre TIA Portal y dirígete a la pestaña **Librerías** (ícono de libro con una flecha verde). 
   - Selecciona el archivo extraído de la librería.

   ![Importar librería en TIA Portal](#)

---

## Configuración del Bloque MQTT en TIA Portal
1. Localiza la carpeta `LMQTT` dentro de la librería importada y selecciona el bloque `LMQTT_Client`.
   
   ![Selección del bloque LMQTT_Client](#)

2. Inserta el bloque en tu programa y asigna las entradas y salidas del bloque a un DB correspondiente.

3. Añade dos segmentos adicionales como se muestra en la siguiente imagen:
   
   ![Configuración de segmentos](#)

4. Configura un segmento adicional en la parte superior para inicializar los parámetros.

### Parámetros del Bloque MQTT
Completa la configuración de los parámetros del bloque según la siguiente tabla:

| **Nombre**            | **Tipo**        | **Descripción**                                                                                       |
|------------------------|-----------------|-------------------------------------------------------------------------------------------------------|
| `enable`              | Input Bool      | TRUE: Conexión al broker MQTT establecida. FALSE: La conexión está rota.                              |
| `publish`             | Input Bool      | Publica `publishMsgPayload` en `mqttTopic` con `retain` y `qos`.                                      |
| `subscribe`           | Input Bool      | Suscribe a `mqttTopic` con `qos`.                                                                     |
| `retain`              | Input Bool      | TRUE: Mensaje retenido. FALSE: Sin retención.                                                         |
| `qos`                 | Input USInt     | Nivel de calidad de servicio (0, 1, 2).                                                               |
| `publishMsgLen`       | Input UDInt     | Tamaño del mensaje a publicar.                                                                        |
| `timeOut`             | Input Time      | Tiempo de espera para operaciones.                                                                    |
| `valid`               | Output Bool     | TRUE: Bloque funcionando sin errores.                                                                 |
| `status`              | Output Word     | Código de estado o error.                                                                             |

---

## Configuración de la Cuenta en Adafruit IO
1. Abre tu navegador web (por ejemplo, Brave) y accede a [Adafruit IO](https://io.adafruit.com/).

2. Regístrate o inicia sesión en tu cuenta.

   ![Página de inicio de sesión de Adafruit IO](#)

3. Ve a la pestaña **Feeds** y selecciona **New Feed** para crear un nuevo feed:
   - Introduce un nombre para el feed.
   - Haz clic en **Crear**.

   ![Creación de un feed](#)

4. Dirígete a la pestaña **Dashboards** y selecciona **New Dashboard**:
   - Asigna un nombre al dashboard.
   - Haz clic en **Crear**.

   ![Creación de un dashboard](#)

5. Abre el dashboard creado, haz clic en el ícono de engranaje en la parte superior derecha y selecciona **Create New Block**:
   - Elige la opción **Stream** y selecciona el feed que creaste previamente.
   - Configura el bloque con un título y diseño personalizado o utiliza la configuración predeterminada.

   ![Configuración de bloques en el dashboard](#)

6. Guarda los cambios haciendo clic en **Save Layout**.

---

## Integración del PLC con Adafruit IO
1. Configura la IP o DNS del servidor MQTT en el PLC. Para Adafruit IO, usa las siguientes credenciales:
   - **Servidor DNS**: `io.adafruit.com`
   - **Tópico**: `<nombre_usuario>/f/<nombre_feed>` (ejemplo: `Aitor_Perez/f/ejemplo`).

2. Encuentra tu **Username** y **Active Key**:
   - Haz clic en el ícono de llave amarilla en la esquina superior derecha.
   - Copia tu **Username** y **Active Key**.

   ![Obtención de credenciales en Adafruit IO](#)

3. Configura el bloque `LMQTT_Client` en TIA Portal con estas credenciales.

4. Define el largo de los caracteres y el mensaje a enviar. Verifica la conexión con el servidor.

---

## Conclusión
Siguiendo estos pasos, habrás configurado un PLC Siemens S7-1200 para comunicarse con el servidor MQTT de Adafruit IO. Puedes visualizar los datos en tiempo real a través del dashboard de Adafruit.

---

## Referencias
- [Librería MQTT para Siemens](https://support.industry.siemens.com/cs/document/109780503/libraries-for-communication-for-simatic-controllers?dti=0&lc=en-ES)
- [Adafruit IO](https://io.adafruit.com/)
- [Documentación Completa en PDF](https://mega.nz/folder/hygSxYIZ#nCYbpJVOV0Q0RaLuluCMSw)
