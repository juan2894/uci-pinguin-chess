# Módulo 4: Conexión con GUIs de Ajedrez

Jugar al ajedrez escribiendo comandos UCI en la consola puede ser interesante para aprender, pero no es la forma más cómoda de disputar una partida. En este módulo aprenderás a integrar **PingunoChess** con las interfaces gráficas (GUIs) de ajedrez más populares.

---

## 1. GUIs Compatibles Recomendadas

Cualquier programa que soporte el protocolo UCI sirve para conectar PingunoChess. Las opciones más recomendadas y gratuitas son:

1. **Arena Chess GUI** (Windows/Linux) - Muy popular, liviana y llena de herramientas de análisis.
2. **Cute Chess** (Windows/macOS/Linux) - Excelente para torneos entre motores y partidas rápidas.
3. **Scid vs. PC** (Windows/macOS/Linux) - Base de datos de ajedrez potente con soporte para motores UCI.
4. **Bankia / Nibbler / PyChess** - Otras interfaces compatibles con Python/UCI.

---

## 2. Configuración en Arena Chess GUI (Ejemplo Paso a Paso)

### Paso 1: Descargar e Instalar Arena
Descarga Arena gratuitamente desde su sitio oficial (o usa la versión portable).

### Paso 2: Añadir un Nuevo Motor UCI
1. Abre Arena.
2. En el menú superior, ve a **Engines** -> **Install New Engine...** (o presione `Ctrl + F2`).
3. Aparecerá una ventana de exploración de archivos.
4. Tienes dos opciones principales para configurar la ruta:

#### Opción A: Archivo Batch/Script (Recomendado en Windows)
Crea un archivo llamado `run_pinguino.bat` en la misma carpeta que el proyecto con el contenido:
```cmd
@echo off
python "C:\ruta\a\tu\proyecto\pinguin_chess_motor_uci.py"
```
Selecciona `run_pinguino.bat` en Arena.

#### Opción B: Seleccionar Python directamente
1. Selecciona el ejecutable `python.exe`.
2. En la ventana de configuración del motor en Arena, en el campo **Command line parameters** o **Arguments**, escribe el nombre del script: `pinguin_chess_motor_uci.py`.

### Paso 3: Selección de Protocolo
Arena detectará el protocolo. Asegúrate de que esté marcado **UCI**.

### Paso 4: ¡Iniciar Partida!
1. Ve al menú **Game** -> **New Game**.
2. Selecciona **PingunoChess** como jugador Blanco o Negro.
3. ¡Comienza a hacer tus jugadas en el tablero gráfico!

---

## 3. Configuración en Cute Chess

En Cute Chess la configuración es aún más sencilla:

1. Ve a **Tools** -> **Settings** -> **Engines**.
2. Haz clic en el botón **+** (Add).
3. Configura los campos:
   - **Name:** PingunoChess
   - **Command:** `python` (o la ruta completa a tu ejecutable de Python)
   - **Arguments:** `pinguin_chess_motor_uci.py`
   - **Working Directory:** La carpeta donde se encuentra `pinguin_chess_motor_uci.py`.
   - **Protocol:** UCI
4. Haz clic en **OK**.
5. Para jugar, ve a **Game** -> **New Game**, selecciona PingunoChess y juega.

---

## 4. Inspección de Logs en Tiempo Real

Cuando juegas mediante una GUI, el archivo `engine_log.txt` se irá actualizando en tiempo real. Puedes abrir una terminal paralela para ver la comunicación en vivo:

En Linux / macOS:
```bash
tail -f engine_log.txt
```

En Windows (PowerShell):
```powershell
Get-Content engine_log.txt -Wait
```

Verás exactamente cómo la GUI envía comandos `position` y `go`, y cómo PingunoChess responde con `bestmove`.

---

## 🧪 Ejercicio Práctico del Módulo 4

1. Instala Cute Chess o Arena en tu computadora.
2. Agrega `pinguin_chess_motor_uci.py` como motor UCI.
3. Juega una partida de 5 minutos contra PingunoChess.
4. Revisa `engine_log.txt` al terminar la partida para analizar todas las jugadas enviadas por la GUI.

---

¡Excelente trabajo! Ahora sabes cómo usar PingunoChess como un motor real en cualquier programa de ajedrez. Pasa al módulo final: **[Módulo 5: Ejercicios y Extensión](05_ejercicios_extension.md)**.
