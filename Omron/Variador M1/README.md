# Cómo Conectar Correctamente un M1 a un PLC NX102

En esta guía, usaremos los siguientes dispositivos:  
- Variador **3G3M1-A4007**  
- PLC **NX102-9020**  
- Tarjeta **PF0730**  
- CPU de seguridad **SL 3300**  
- Tarjeta **SID800**  

---

## Configuración del Bastidor

En el bastidor, colocamos los dispositivos en la siguiente disposición:  

![Disposición del bastidor](./images/Step1Rack.png)

Conectamos el variador al PLC mediante **EtherCAT**. Asegúrate de que los nodos están correctamente configurados tanto en el software como en el hardware. En este ejemplo, usamos un **3G3M1**.

---

## Configuración de la CPU de Seguridad

1. Ve a la CPU de seguridad y selecciona la tarjeta de entradas en los parámetros.
2. Asigna nombres a las entradas para el botón de paro y el botón de reinicio:
   - Botón de paro: **EStop**  
   - Botón de reinicio: **Reset Button**  

   *(Nota: Aunque el botón de paro tiene dos interruptores, basta con nombrar uno).*

La configuración se verá de esta manera:  

![Configuración de la CPU de seguridad](./images/Step2_Entradas.png)

El cableado real debería lucir similar a esto:  

![Cableado del sistema](./images/Step3_Cableado.jpeg)

---

## Modificación del Mapa de PDOs del Variador

1. Ve al PLC y accede a la configuración de EtherCAT.  
2. Selecciona el botón **Configuración de Asignación**.

![Acceso a la configuración de asignación](./images/Step4_Ethercat.png)

Asigna los parámetros del mapa de PDOs según las siguientes imágenes:

![Configuración del PDOs (1)](./images/Step5_Parametros1.jpeg)  
![Configuración del PDOs (2)](./images/Step6_Parametros2.jpeg)  
![Configuración del PDOs (3)](./images/Step7_Parametros3.jpeg)  
![Configuración del PDOs (4)](./images/Step8_Parametros4.jpeg)  

---

## Configuración del Mapa de Entradas/Salidas en la CPU de Seguridad

En el mapa de entradas/salidas de la CPU de seguridad, configura los valores según esta imagen:  

![Mapa de E/S en la CPU de seguridad](./images/Step9_Ajustes.png)

---

## Programación de la CPU de Seguridad

En la sección de programación de la CPU de seguridad, añade el siguiente bloque:  

![Bloque de programación](./images/Step10_Seguridad.png)

---

## Configuración de Parámetros FSoE

1. Ve a **Parámetros** y busca el número **H483**.
2. Asigna la dirección **FSoE** deseada (en este ejemplo, usamos el valor `3`).  
   *(Asegúrate de que no interfiera con otras configuraciones).*

3. Comprueba que la dirección coincida con la de la CPU de seguridad.  

Ejemplo de configuración:  

![Configuración de parámetros (1)](./images/Step11_Data1.jpeg)  
![Configuración de parámetros (2)](./images/Step12_Data2.jpeg)

---

## Referencia Adicional

Si encuentras problemas al seguir esta guía, puedes consultar este tutorial en video:  
[Guía en YouTube](https://www.youtube.com/watch?v=lT8H641sjLI)
