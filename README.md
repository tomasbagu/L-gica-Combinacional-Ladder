# Lógica Combinacional en Ladder – Monitoreo de un Tanque de Líquidos

## 1. Introducción  

Este proyecto desarrolla el diseño e implementación de un sistema de **automatización industrial** orientado al **monitoreo de niveles en un tanque de líquido químico**.  

La propuesta emplea **tres sensores de nivel** y un esquema de **lógica combinacional** para determinar el estado del tanque. Dicho estado se visualiza en una **HMI (Human-Machine Interface)** diseñada en **CODESYS** y se valida posteriormente mediante **OPENPLC y hardware real**.  

**Objetivo general:**  
- Diseñar e implementar una solución de monitoreo que detecte de forma confiable los niveles de un tanque, mostrando estados correctos y posibles errores en una HMI.  

**Objetivos específicos:**  
- Elaborar la lógica combinacional en lenguaje ladder.  
- Implementar y simular la solución en CODESYS.  
- Validar el diseño con OPENPLC y un prototipo físico.  
- Documentar el proceso en formato Wiki y presentar una demostración en video.  

---

## 2. Marco Teórico  

### 2.1. HMI (Human-Machine Interface)  
Una HMI es la interfaz gráfica que conecta al operador con una máquina o proceso industrial. Su función es traducir datos técnicos en representaciones visuales claras y manipulables, facilitando la supervisión y control del sistema. En este proyecto, la HMI representa un tanque con indicadores de nivel.  

### 2.2. CODESYS  
CODESYS es un software ampliamente usado en la industria para programar y simular controladores lógicos programables (PLC). Su importancia radica en que permite diseñar la lógica que controla las máquinas, pero también ofrece la posibilidad de crear interfaces gráficas (HMIs) dentro del mismo entorno. De esta forma, se puede construir y probar todo el sistema de automatización en un solo lugar, lo cual lo convierte en una herramienta flexible para cualquier persona que la use.
### 2.3. OPENPLC  
OPENPLC es un PLC de código abierto que permite ejecutar programas basados en diferentes plataformas, incluyendo computadoras y hardware de bajo costo como por ejemplo Arduino o ESP32. Su principal ventaja es la flexibilidad para conectar entradas y salidas físicas y validar sistemas de control sin necesidad de hardware industrial costoso.  

### 2.4. Sensores de Nivel  
El sistema emplea **tres sensores digitales**:  
- **S1 (sensor bajo):** Detecta el nivel mínimo.  
- **S2 (sensor medio):** Detecta el nivel intermedio.  
- **S3 (sensor alto):** Detecta el nivel máximo.  

### 2.5. Lógica combinacional  
La determinación del estado del tanque se establece mediante la siguiente tabla de verdad:  

| S1 | S2 | S3 | Estado del tanque |
|----|----|----|-------------------|
| 0  | 0  | 0  | Vacío             |
| 1  | 0  | 0  | Bajo              |
| 1  | 1  | 0  | Normal            |
| 1  | 1  | 1  | Alto              |
| Otro caso | Otro caso | Otro caso | Error |

Este modelo asegura una lectura consistente del tanque y detecta condiciones anómalas.  

---

## 3. Diseño de la Solución  

### 3.1. Lógica en Ladder Diagram  
El sistema fue implementado en **ladder diagram**.  
- Cada sensor corresponde a una entrada digital (S1, S2, S3).  
- Cada estado del tanque corresponde a una salida (EMP: vacío, LO: bajo, NOR: normal, HI: alto, ERR: error).  

<img width="1228" height="757" alt="image" src="https://github.com/user-attachments/assets/aee9893e-ee19-4d7d-8dd6-476334877e14" />

### 3.2. HMI en CODESYS  
La HMI representa gráficamente el tanque y sus niveles:  
- Indicadores para vacío, bajo, normal y alto.  
- Un indicador adicional para estados erróneos.  

Ejemplo con el tanque en nivel bajo:  

<img width="1158" height="659" alt="image" src="https://github.com/user-attachments/assets/b2400886-da24-4855-bb76-b93e0bf9e4db" />

### 3.3. Hardware propuesto  
- PLC físico o simulador en OPENPLC.  
- Tres sensores de nivel (flotadores, capacitivos o pulsadores en prototipo).  
- Salidas visualizadas mediante LEDs o indicadores virtuales.  
-Conexiones en OpenPLC
<img width="1329" height="503" alt="image" src="https://github.com/user-attachments/assets/f5337c6b-d1b6-45a3-8c7e-4faaee395467" />
- Físico
<img width="1595" height="756" alt="image" src="https://github.com/user-attachments/assets/77f2f599-2b50-4665-b050-7074cb880fbc" />


---

## 4. Implementación  

### 4.1. Simulación en CODESYS  
- Configuración de entradas digitales como sensores.  
- Asociación de variables a los objetos gráficos de la HMI.  
- Ejecución de la simulación y verificación de los diferentes estados.  

### 4.2. Validación con OPENPLC y prototipo real  
- Exportación del programa a formato compatible con OPENPLC.  
- Carga en un controlador (ejemplo: ESP32).  
- Conexión de sensores físicos y LEDs de salida.  
- Ejecución de pruebas con activación progresiva de sensores.  

---

## 5. Resultados y Pruebas  

Se realizaron pruebas tanto en simulación (CODESYS) como en hardware real (OPENPLC):  

- **Prueba 1:** Ningún sensor activado → tanque vacío.  
- **Prueba 2:** Solo S1 activado → nivel bajo.  
- **Prueba 3:** S1 + S2 activados → nivel normal.  
- **Prueba 4:** S1 + S2 + S3 activados → nivel alto.  
- **Prueba 5:** Combinación inválida (ejemplo: S2 sin S1) → error.  

### 5.1 Resultados en CODESYS  
*(Evidencias gráficas de la simulación en distintos estados)*  

### 5.2 Resultados en OPENPLC (Hardware real)  
*(Documentación de las pruebas con sensores y LEDs físicos)*  

---

## 6. Video de Demostración  

🎥 [Enlace al video en YouTube o Teams]  

Contenido:  
1. Presentación breve del sistema.  
2. Simulación en CODESYS (HMI + Ladder).  
3. Validación en OPENPLC con prototipo real.  
4. Conclusiones del proyecto.  

---

## 7. Conclusiones  

- Se implementó con éxito una **lógica combinacional** que permite monitorear los niveles de un tanque mediante tres sensores digitales.  
- La **HMI en CODESYS** permitió visualizar de manera clara los estados del sistema.  
- La **validación en OPENPLC** confirmó la viabilidad de trasladar la lógica a un entorno físico.  
- El proyecto puede ampliarse hacia sistemas más complejos, integrando **alarmas automáticas, comunicación SCADA o control de bombas**.  

---

## 8. Referencias  

- IEC 61131-3: International Electrotechnical Commission. *Programmable controllers – Part 3: Programming languages*. IEC, 2013.  
- CODESYS Group. *CODESYS Development System V3 Documentation*. Disponible en: [https://www.codesys.com](https://www.codesys.com)  
- OPENPLC Project. *Official Documentation*. Disponible en: [https://www.openplcproject.com](https://www.openplcproject.com)  
- Bolton, W. *Programmable Logic Controllers*. 6th ed. Elsevier, 2015.  
- Petruzella, F. *Programmable Logic Controllers*. McGraw-Hill, 2010.  
