# Curso Interactivo: Aprende Ajedrez con Python y PingunoChess

¡Bienvenido al curso de **PingunoChess**! Este curso está diseñado estilo tutorial/paso a paso para enseñarte cómo funciona un motor de ajedrez escrito en Python, cómo implementa el protocolo Estándar de Interfaz Universal de Ajedrez (**UCI**), y cómo puedes extenderlo o conectarlo a GUIs (interfaces gráficas) de ajedrez.

---

## 📚 Estructura del Curso

El curso está organizado en 5 módulos secuenciales. Cada módulo incluye teoría, explicaciones detalladas del código, pruebas prácticas en consola y retos/ejercicios al final:

1. **[Módulo 1: Configuración del Entorno](01_configuracion_entorno.md)**
   - Requisitos previos (Python 3.x).
   - Instalación de dependencias (`python-chess`).
   - Verificación y ejecución directa en terminal.

2. **[Módulo 2: El Protocolo UCI (Universal Chess Interface)](02_protocolo_uci.md)**
   - ¿Qué es el protocolo UCI y cómo funciona?
   - Comunicación entrada/salida estándar (`stdin` / `stdout`).
   - Comandos principales: `uci`, `isready`, `position`, `go`, `stop`, `setoption`, `quit`.
   - Práctica interactiva desde la línea de comandos.

3. **[Módulo 3: Arquitectura y Lógica Interna de PingunoChess](03_arquitectura_pinguinochess.md)**
   - Desglose del código `pinguin_chess_motor_uci.py`.
   - Evaluación de capturas (1-ply) y tabla de valores de piezas.
   - Evaluación posicional y gestión de riesgo.
   - Jerarquía de toma de decisiones (Mate -> Captura -> Aleatorio).
   - Sistema de logging y depuración (`engine_log.txt`).

4. **[Módulo 4: Conexión con GUIs de Ajedrez](04_conexion_gui.md)**
   - Configuración en software de ajedrez popular (Arena, Cute Chess, Scid vs. PC).
   - Simulación de partidas contra el motor.
   - Inspección de logs en tiempo real.

5. **[Módulo 5: Ejercicios Prácticos y Extensión del Motor](05_ejercicios_extension.md)**
   - Retos prácticos para mejorar el motor.
   - Introducción a la búsqueda en profundidad (Minimax y Poda Alfa-Beta).
   - Implementación de nuevas heurísticas posicionales y libros de apertura.

---

## 🎯 ¿A quién va dirigido este curso?

- Estudiantes de programación y entusiastas de Python.
- Aficionados al ajedrez interesados en saber cómo "piensan" las computadoras.
- Desarrolladores que desean entender protocolos de comunicación entre software de ajedrez.

---

## 🚀 ¿Cómo tomar este curso?

Sigue los módulos en orden correlativo del 1 al 5. Se recomienda tener abierto tu editor de código o terminal a la par de las lecturas para ir probando los comandos e implementando los ejercicios prácticos.

¡Comienza ya con el **[Módulo 1: Configuración del Entorno](01_configuracion_entorno.md)**!
