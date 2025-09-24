# Logica Combinacional de Ladder – Monitoreo de un tanque de líquidos

## 1. Introducción  
Este proyecto aborda el diseño e implementación de un sistema de **automatización industrial** para el **monitoreo de niveles de un tanque de líquido químico**.  
El sistema utiliza **tres sensores de nivel** y lógica combinacional para identificar el estado del tanque, representándolo en una **HMI diseñada en CODESYS** y validándolo posteriormente con **OPENPLC y hardware real**.  

**Objetivo general:**  
- Desarrollar una solución de monitoreo que detecte el nivel del líquido en un tanque, mostrando estados correctos y errores en una HMI.  

**Objetivos específicos:**  
- Diseñar la lógica combinacional en ladder diagram.  
- Implementar y simular la solución en CODESYS.  
- Validar el diseño mediante OPENPLC y un prototipo con sensores.  
- Documentar el proceso en un Wiki y realizar una demostración en video.  

---

## 2. Marco Teórico  

### 2.1. HMI (Human-Machine Interface)  
Una HMI es la pantalla o panel gráfico que conecta a las personas con una máquina o proceso industrial. Gracias a ella, el operador puede ver lo que está ocurriendo en el sistema y también interactuar con él. En pocas palabras, la HMI traduce la información técnica de un proceso en gráficos fáciles de entender y manipular. En este proyecto, se representa gráficamente un tanque y sus niveles de llenado.  

### 2.2. CODESYS  
CODESYS es un software ampliamente usado en la industria para programar y simular controladores lógicos programables (PLC). Su importancia radica en que permite diseñar la lógica que controla las máquinas, pero también ofrece la posibilidad de crear interfaces gráficas (HMIs) dentro del mismo entorno. De esta forma, se puede construir y probar todo el sistema de automatización en un solo lugar, lo cual lo convierte en una herramienta flexible para cualquier persona que la use.
### 2.3. OPENPLC  
OPENPLC es una plataforma de automatización que funciona como un controlador lógico programable (PLC), pero en formato de software. En cuanto a su funcionamiento, OPENPLC recibe entradas y, a partir de la lógica programada, genera salidas. Puede correr en un computador, en modo simulador, o en hardware sencillo como Arduino, ESP32, entre otros, permitiendo conectar entradas y salidas reales. De esta forma, se convierte en una herramienta práctica para probar, validar y ejecutar sistemas de automatización de manera flexible y económica.
### 2.4. Sensores de Nivel  
Se emplean tres sensores digitales:  
- **Sensor bajo (S1)** → detecta nivel mínimo.  
- **Sensor medio (S2)** → detecta nivel intermedio.  
- **Sensor alto (S3)** → detecta nivel máximo.  

### 2.5. Lógica combinacional  
La determinación del estado del tanque se basa en la siguiente **tabla de verdad**:  

| SB | SM | SA | Estado del tanque |
|----|----|----|-------------------|
| 0  | 0  | 0  | Vacío             |
| 1  | 0  | 0  | Bajo              |
| 1  | 1  | 0  | Normal            |
| 1  | 1  | 1  | Alto              |
| Otro caso | Otro caso | Otro caso | Error |

---

## 3. Diseño de la Solución  

### 3.1. Lógica en Ladder Diagram  
El sistema se implementa en **ladder diagram**.  
- Cada sensor es una entrada digital (S1, S2, S3).  
- Cada estado del tanque es una salida (EMP: vacío, LO: bajo, NOR: normal, HI: alto, ERR: error).  

<img width="1228" height="757" alt="image" src="https://github.com/user-attachments/assets/aee9893e-ee19-4d7d-8dd6-476334877e14" />


### 3.2. HMI en CODESYS  
- Representación gráfica de un tanque.  
- Tres indicadores de nivel (vacío, bajo, normal, alto).  
- Indicador adicional para error.
  - Ejemplo de nivel bajo para el HMI:
<img width="1158" height="659" alt="image" src="https://github.com/user-attachments/assets/b2400886-da24-4855-bb76-b93e0bf9e4db" />


### 3.3. Hardware propuesto  
- PLC (o simulador en OPENPLC).  
- 3 sensores de nivel (pueden ser flotadores, capacitivos o pulsadores para prototipo).  
- Salidas visualizadas en LEDs o indicadores virtuales.  

*(Aquí se incluye un diagrama eléctrico con los tres sensores como entradas y las salidas como LEDs/indicadores)*  

---

## 4. Implementación  

### 4.1. Simulación en CODESYS  
- Configuración de las entradas digitales como sensores.  
- Asignación de variables a los objetos gráficos en la HMI.  
- Ejecución de la simulación mostrando los distintos estados del tanque.  

### 4.2. Validación con OPENPLC y prototipo real  
- Exportación del programa a formato OPENPLC.  
- Carga en un controlador (En este caso un ESP32).  
- Conexión de sensores físicos y LEDs de salida.  
- Pruebas de funcionamiento con activación de los sensores.  

---

## 5. Resultados y Pruebas  

- **Prueba 1:** Ningún sensor activado → tanque vacío.  
- **Prueba 2:** Solo S1 activado → nivel bajo.  
- **Prueba 3:** S1 + S2 activados → nivel normal.  
- **Prueba 4:** S1 + S2 + S3 activados → nivel alto.  
- **Prueba 5:** Combinación inválida (ej: SM sin SB) → error.  

*(Aquí se documentan capturas de pantalla de la simulación en CODESYS y fotos del prototipo con OPENPLC)*  

---

## 6. Video de Demostración  

🎥 [Enlace al video en YouTube/Teams]  

Contenido del video:  
1. Explicación breve del sistema.  
2. Simulación en CODESYS (HMI + Ladder).  
3. Validación con OPENPLC y prototipo real.  
4. Conclusiones.  

---

## 7. Conclusiones  

- Se diseñó una lógica combinacional que permite monitorear de manera confiable los niveles del tanque.  
- La implementación en CODESYS facilita la visualización del proceso mediante un HMI interactivo.  
- La validación con OPENPLC demuestra la factibilidad del sistema con hardware real.  
- El proyecto puede ampliarse integrando alarmas, comunicación SCADA o control automático de bombas.  

---

## 8. Referencias  

- IEC 61131-3 Standard – Programmable Controllers.  
- CODESYS Documentation.  
- OPENPLC Project – [https://www.openplcproject.com/](https://www.openplcproject.com/)  
- Libros y recursos de automatización industrial.  
