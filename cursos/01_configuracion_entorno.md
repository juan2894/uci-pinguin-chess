# Módulo 1: Configuración del Entorno y Primer Vistazo

Bienvenido al primer módulo del curso. En esta lección prepararemos el entorno de desarrollo necesario para ejecutar **PingunoChess** y realizaremos nuestra primera prueba interactiva.

---

## 1. Requisitos Previos

Para ejecutar y modificar este proyecto necesitas:

1. **Python 3.8 o superior** instalado en tu sistema operativo (Windows, macOS o Linux).
2. Un editor de código (como VS Code, PyCharm o un terminal de texto).
3. Conocimientos básicos del uso de la línea de comandos (terminal o PowerShell).

### Verificación de Python
Abre tu terminal y ejecuta:

```bash
python --version
# o en algunos sistemas:
python3 --version
```

Asegúrate de que la versión mostrada sea igual o superior a 3.8.

---

## 2. Instalación de la Librería `python-chess`

**PingunoChess** utiliza la librería de código abierto [`python-chess`](https://python-chess.readthedocs.io/), la cual administra las reglas del juego, la validación de movimientos legales, la generación de posiciones en formato FEN y el estado del tablero.

Instálala usando `pip`:

```bash
pip install chess
```

> **Nota:** En algunos entornos el paquete se llama `python-chess` o `chess`. El comando estándar de instalación es `pip install chess`.

---

## 3. Descarga / Estructura del Repositorio

Asegúrate de tener los archivos del proyecto en tu directorio de trabajo. La estructura básica debe verse así:

```text
pinguinochess/
├── pinguin_chess_motor_uci.py   # Código fuente principal del motor UCI
├── README.md                    # Documentación general
├── README_EN.md                 # Documentación en inglés
└── cursos/                      # Archivos de este curso
```

---

## 4. Primera Ejecución Interactiva

A diferencia de la mayoría de programas en Python con interfaz de usuario o salidas enriquecidas, un motor de ajedrez UCI se comunica leyendo líneas de texto por **entrada estándar (`stdin`)** y respondiendo por **salida estándar (`stdout`)**.

Ejecuta el archivo del motor desde la terminal:

```bash
python pinguin_chess_motor_uci.py
```

Al hacerlo, notarás que la consola se queda en espera sin mostrar ningún mensaje de bienvenida vistoso. Esto es normal: el motor está esperando un comando UCI.

Escribe el comando:
```text
uci
```
y presiona **Enter**.

Deberías ver una respuesta similar a esta:
```text
id name PingunoChess
id author Juan Felipe Garavito Arias
option name OwnBook type check default false
option name Debug Log File type string default
uciok
```

Escribe ahora:
```text
quit
```
y presiona **Enter** para finalizar el programa.

---

## 🧪 Ejercicio Práctico del Módulo 1

1. Abre tu terminal y ejecuta `python pinguin_chess_motor_uci.py`.
2. Envía el comando `uci` y observa la respuesta.
3. Revisa la carpeta de tu proyecto: deberías ver que se ha creado un archivo llamado `engine_log.txt`.
4. Abre `engine_log.txt` con un editor de texto y comprueba que se hayan registrado los comandos `uci` y `quit`.

---

¡Felicidades! Has completado el Módulo 1. Continúa con el **[Módulo 2: El Protocolo UCI](02_protocolo_uci.md)** para aprender a comunicarte con el motor.
