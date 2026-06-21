# PingunoChess

[English Version](README_EN.md)

PingunoChess es un motor de ajedrez básico compatible con el protocolo UCI (Universal Chess Interface), escrito en Python. Este motor está diseñado para ser conectado a interfaces gráficas de ajedrez (GUI) como Arena, Cute Chess o Scid vs. PC.

## Características

- **Compatibilidad UCI:** Soporta los comandos básicos del protocolo UCI, permitiendo su integración con la mayoría de las interfaces de ajedrez modernas.
- **Lógica de Decisión (1-ply):**
  1. **Jaque Mate:** Si encuentra un movimiento que da jaque mate de inmediato, lo realiza.
  2. **Capturas:** Si no hay mate, busca la mejor captura basada en un sistema de puntuación (valor de la pieza capturada, posición resultante y riesgo).
  3. **Movimiento Aleatorio:** Si no hay capturas ni mates, elige un movimiento legal al azar.
- **Soporte de Opciones:** Permite configurar opciones básicas a través del comando `setoption` (ej. `OwnBook`, `Debug Log File`).
- **Manejo de Tiempo:** Procesa parámetros de tiempo en el comando `go` (`wtime`, `btime`, `winc`, `binc`, `movetime`), aunque actualmente responde de forma casi instantánea.
- **Registro de Log:** Genera un archivo `engine_log.txt` para depuración, donde se registran las comunicaciones entre la GUI y el motor.

## Requisitos

- **Python 3.x**
- **Librería `chess` de Python:** Necesaria para el manejo de las reglas y la lógica del tablero.

## Instalación

1. Asegúrate de tener Python instalado en tu sistema.
2. Instala la librería necesaria utilizando pip:

```bash
pip install chess
```

3. Descarga el archivo `pinguin_chess_motor_uci.py` en tu máquina.

## Uso

### Ejecución Directa
Puedes ejecutar el motor desde la terminal para verificar que responde correctamente a los comandos UCI:

```bash
python pinguin_chess_motor_uci.py
```
Una vez ejecutado, puedes escribir `uci` y presionar Enter para ver la identificación del motor.

### Conexión a una GUI
Para jugar contra PingunoChess, debes agregarlo como un nuevo motor en tu software de ajedrez favorito:
1. Abre tu GUI de ajedrez (ej. Arena).
2. Ve a la sección de configuración de motores (Engines -> Install New Engine).
3. Selecciona el ejecutable de Python y pasa el nombre del archivo `pinguin_chess_motor_uci.py` como argumento, o crea un archivo ejecutable/script que lo inicie.
4. Asegúrate de que el protocolo seleccionado sea **UCI**.

## Detalles Técnicos

### Evaluación de Capturas
El motor evalúa las capturas considerando:
- El valor de la pieza capturada.
- Bonificaciones por posición (control del centro).
- Penalizaciones si la pieza atacante queda desprotegida o es de mayor valor que la capturada.
- Bonificaciones por cercanía al rey enemigo.

## Autor
**Juan Felipe Garavito Arias** - *Desarrollador Principal* - 2025-09-16
