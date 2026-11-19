[![Open in MATLAB Online](https://www.mathworks.com/images/responsive/global/open-in-matlab-online.svg)](https://matlab.mathworks.com/open/github/v1?repo=23210714/MSFP4)
# MSFP4
<div align="center">

# 🧬 MODELADO Y CONTROL DEL SISTEMA ENDÓCRINO

### PRÁCTICA 04 · MODELADO DE SISTEMAS FISIOLÓGICOS

**INGENIERÍA BIOMÉDICA · TECNM / INSTITUTO TECNOLÓGICO DE TIJUANA**

![MATLAB](https://img.shields.io/badge/MATLAB-Simulink-0076A8?style=for-the-badge) ![Python](https://img.shields.io/badge/Python-Control-3776AB?style=for-the-badge) ![PID](https://img.shields.io/badge/Control-PID-1F2937?style=for-the-badge) ![Status](https://img.shields.io/badge/Proyecto-Académico-64748B?style=for-the-badge)

*Análisis dinámico · Analogía eléctrica · Funciones de transferencia · Control retroalimentado*

</div>

---

## 01 / FICHA DEL PROYECTO

| Campo | Información |
|:--|:--|
| **Estudiante** | **Maria Luisa Michelle Muñoz Meneses** |
| **Número de control** | 23210714 |
| **Asignatura** | Modelado de Sistemas Fisiológicos (IBF-1020) |
| **Docente** | Dr. Paul Antonio Valle Trujillo |
| **Institución** | Tecnológico Nacional de México · Instituto Tecnológico de Tijuana |
| **Programa** | Ingeniería Biomédica |
| **Ubicación** | Tijuana, Baja California, México |
| **Práctica** | 04 · Modelado y control del sistema endócrino |

> **Objetivo central:** representar la dinámica de un sistema endócrino mediante un circuito eléctrico equivalente, comparar las condiciones de control y caso, y evaluar el efecto de un controlador PID.

## 02 / RESUMEN EJECUTIVO

Se desarrolla un modelo dinámico de segundo orden para describir de forma simplificada los procesos de estímulo, transporte, almacenamiento y respuesta hormonal. El sistema se representa con dos resistencias (**R₁**, **R₂**), una inductancia (**L**) y una capacitancia (**C**). A partir de las leyes de Kirchhoff se obtiene su función de transferencia y se evalúa la respuesta ante una entrada escalón unitario.

Se analizan dos configuraciones de parámetros: **control**, como referencia, y **caso**, como condición modificada. Posteriormente se incorpora un controlador **PID** para aproximar la respuesta del caso a la del control. La práctica se documenta mediante MATLAB/Simulink, Python, una representación BioRender y evidencia de osciloscopio.

**Palabras clave:** sistema endócrino · homeostasis · hipertiroidismo · analogía eléctrica · circuito RLC · función de transferencia · control PID · MATLAB · Simulink · Python · BioRender.

## 03 / OBJETIVOS Y ALCANCE

**Objetivo general.** Modelar y comparar la dinámica del sistema endócrino en las condiciones control y caso, implementando una estrategia de control PID para reducir la diferencia de sus respuestas.

**Objetivos específicos**

- Establecer la correspondencia entre variables fisiológicas y elementos eléctricos.
- Formular las ecuaciones diferenciales y la función de transferencia.
- Evaluar estabilidad, respuesta temporal y error estacionario.
- Implementar el modelo en MATLAB/Simulink y Python.
- Comparar la condición sin compensación con la respuesta bajo control PID.
- Integrar evidencias visuales y experimentales.

**Relación con el temario:** sistemas retroalimentados, modelado matemático mediante analogías eléctricas y diseño de controladores.

## 04 / ARQUITECTURA FISIOLÓGICA

El sistema endócrino regula funciones del organismo mediante la liberación de hormonas. En esta práctica, su comportamiento se aproxima por un sistema de estímulo–respuesta con almacenamiento y retardo dinámico.



<img width="887" height="621" alt="image" src="https://github.com/user-attachments/assets/ecc5fc98-1fda-437d-8cce-f0e54f7b7be3" />


<!-- ![Figura 01. Modelo fisiológico y analogía eléctrica en BioRender](biorender.png) -->

*Figura 01. Comparación ilustrativa entre homeostasis (control) y el caso representado como hipertiroidismo, con su circuito equivalente.*

**Nota de interpretación:** el modelo eléctrico es una analogía académica genérica. La representación de hipertiroidismo es ilustrativa y no equivale a un modelo clínicamente validado de la función tiroidea.

## 05 / MODELO ELÉCTRICO

La entrada **Vₑ(t)** se conecta a **R₁**; el nodo de salida **Vₛ(t)** se vincula a una rama capacitiva **C** y a otra rama formada por **L** y **R₂** en serie.

| Variable | Interpretación simplificada |
|:--|:--|
| `Ve(t)` | Estímulo de entrada |
| `Fe(t)` | Flujo de secreción/transporte |
| `R1` | Oposición al transporte |
| `C` | Almacenamiento temporal |
| `L` | Inercia o retardo de respuesta |
| `R2` | Utilización o eliminación de señal |
| `Fs(t)` | Flujo de respuesta |
| `Vs(t)` | Salida del sistema |

### Parámetros de simulación

| Parámetro | CONTROL | CASO |
|:--|--:|--:|
| R₁ | 1 kΩ | 1 kΩ |
| L | 100 mH | 100 mH |
| C | 1 µF | 1000 µF |
| R₂ | 100 kΩ | 1 kΩ |

## 06 / FORMULACIÓN MATEMÁTICA

### Ecuaciones de Kirchhoff

$$
F_e(t)=C\frac{dV_s(t)}{dt}+F_s(t)
$$

$$
V_e(t)=R_1F_e(t)+V_s(t)
$$

$$
V_s(t)=L\frac{dF_s(t)}{dt}+R_2F_s(t)
$$

### Representación en espacio de estados

$$
\frac{dV_s}{dt}=\frac{1}{C}\left(\frac{V_e-V_s}{R_1}-F_s\right)
$$

$$
\frac{dF_s}{dt}=\frac{V_s-R_2F_s}{L}
$$

### Función de transferencia general

Con condiciones iniciales nulas:

$$
\boxed{G(s)=\frac{V_s(s)}{V_e(s)}=\frac{Ls+R_2}{CLR_1s^2+(CR_1R_2+L)s+(R_1+R_2)}}
$$

**Condición control:**

$$
G_{control}(s)=\frac{0.1s+100000}{0.0001s^2+100.0001s+101000}
$$

**Condición caso:**

$$
G_{caso}(s)=\frac{0.1s+1000}{0.1s^2+1000.1s+2000}
$$

## 07 / ANÁLISIS DINÁMICO

Para una entrada escalón unitario, el valor estacionario se determina mediante la ganancia de continua de cada planta estable:

$$
V_{s,control}(\infty)=\frac{100000}{101000}\approx0.9901
$$

$$
V_{s,caso}(\infty)=\frac{1000}{2000}=0.5
$$

El error respecto a una entrada unitaria **en lazo abierto** es:

$$
e_{ss,control}\approx0.0099,\qquad e_{ss,caso}=0.5
$$

Los polos se calculan a partir de:

$$
CLR_1s^2+(CR_1R_2+L)s+(R_1+R_2)=0
$$

Ambas plantas presentan polos con parte real negativa para los parámetros empleados, aunque sus tiempos de respuesta y valores finales son diferentes.

## 08 / SIMULACIÓN EN MATLAB Y SIMULINK

**Configuración:** entrada escalón unitario; intervalo de 0 a 10 s; solver `ode15s`; paso máximo `1e-3` s.

```matlab
clc; clear; close all; warning('off','all')
open_system('sistema')
parameters.StopTime = '10';
parameters.Solver = 'ode15s';
parameters.MaxStep = '1e-3';
x = sim('sistema',parameters);
plotsignals(x.control,x.CE,x.PID,x.Ve,'Caso')
```



<img width="533" height="275" alt="image" src="https://github.com/user-attachments/assets/37edc490-ee27-45fb-a35a-c7a2e3ababaf" />




## 09 / DISEÑO DEL CONTROLADOR PID

La señal de error se define como la diferencia entre la referencia y la salida del caso:

$$
e(t)=V_{s,control}(t)-V_{s,caso}(t)
$$

La ley de control ideal en el dominio de Laplace es:

$$
K(s)=k_P+\frac{k_I}{s}+k_Ds
$$

| Ganancia | Valor empleado en Python |
|:--|--:|
| **Proporcional** `kP` | 13209.9564 |
| **Integral** `kI` | 32316525.9285 |
| **Derivativa** `kD` | 0.18118 |

La implementación incluida en el programa original utiliza una realización racional del PID y retroalimentación negativa:

```python
kP, kI, kD = 13209.9564, 32316525.9285, 0.18118
Cr = 1E-6
Re = 1/(Cr*kI)
Rr = kP*Re
Ce = kD/Rr
numPID = [Re*Rr*Ce*Cr, Re*Ce+Rr*Cr, 1]
denPID = [Re*Cr, 0]
PID = ctrl.tf(numPID, denPID)
sysPID = ctrl.feedback(ctrl.series(PID, sysCaso), 1, sign=-1)
```

La respuesta del control se emplea como señal de referencia del tratamiento PID en el código Python original.

## 10 / VERIFICACIÓN EN PYTHON

Se utilizan las bibliotecas `numpy`, `matplotlib` y `control` para obtener las funciones de transferencia y simular la respuesta temporal.

```python
def sis(C, R2, nombre):
    R1, L = 1E3, 100E-3
    num = [L, R2]
    den = [C*L*R1, C*R1*R2+L, R1+R2]
    sys = ctrl.tf(num, den)
    print(f"Función de transferencia {nombre}: {sys}\n")
    return sys

sysControl = sis(1E-6, 100E3, "Control")
sysCaso = sis(1000E-6, 1E3, "Caso")
```

### ESPACIO PARA FIGURA 03 · GRÁFICA PYTHON

<img width="536" height="322" alt="image" src="https://github.com/user-attachments/assets/9c31fedc-4947-4900-a03b-57750fc83c6e" />


*Figura 03. Señal de entrada y comparación de las respuestas control, caso y tratamiento PID.*

## 11 / RESULTADOS Y EVIDENCIA

| Escenario | Resultado esperado del modelo |
|:--|:--|
| **Entrada** | Escalón unitario |
| **Control** | Respuesta más rápida, valor final ≈ 0.99 |
| **Caso** | Respuesta más lenta, valor final ≈ 0.50 |
| **Caso con PID** | Respuesta aproximada a la referencia de control |

### ESPACIO PARA FIGURA 04 · OSCILOSCOPIO

<img width="650" height="502" alt="image" src="https://github.com/user-attachments/assets/733b748b-a33f-4fb3-a464-667f6e379c5b" />


*Figura 04. Evidencia de laboratorio.

### Lectura de resultados

La modificación de C y R₂ afecta tanto la rapidez como la amplitud estacionaria de la respuesta. Las simulaciones en MATLAB y Python permiten contrastar los escenarios y evaluar el efecto del PID. La captura de osciloscopio aporta evidencia cualitativa de una transición de entrada y una respuesta gradual; no constituye por sí sola una validación cuantitativa del modelo.

## 12 / CONCLUSIONES

El uso de un circuito eléctrico equivalente permitió expresar un sistema endócrino simplificado mediante ecuaciones diferenciales y una función de transferencia de segundo orden. La comparación entre las condiciones control y caso evidenció cambios en la respuesta temporal y en el valor estacionario. La estrategia PID permitió estudiar la corrección de la respuesta alterada con respecto a la referencia. MATLAB/Simulink y Python facilitaron la verificación computacional, mientras que BioRender y la evidencia experimental complementaron la presentación de resultados. El alcance del trabajo es académico y no constituye una validación clínica de una enfermedad endócrina específica.

## 13 / REFERENCIAS

1. Valle Trujillo, P. A. (2026). *Modelado de Sistemas Fisiológicos (IBF-1020)*, apartado 5.6: «Modelado y control del sistema endócrino». Instituto Tecnológico de Tijuana.
2. Valle Trujillo, P. A. *README de referencia de la asignatura*. Material proporcionado por el docente.
3. [Repositorio académico MSF-IBF1020](https://github.com/DrPaulValle/MSF-IBF1020).

---

<div align="center">

**MODELADO DE SISTEMAS FISIOLÓGICOS · PRÁCTICA 04**

*Ingeniería Biomédica · Instituto Tecnológico de Tijuana*

</div>
