# Módulo 2: El Protocolo UCI (Universal Chess Interface)

En este módulo aprenderemos qué es el protocolo **UCI**, cómo funciona la comunicación entre una interfaz gráfica (GUI) y el motor, y cómo puedes interactuar manualmente con el motor mediante comandos UCI.

---

## 1. ¿Qué es el Protocolo UCI?

El **Universal Chess Interface (UCI)** es un protocolo estándar basado en texto creado por Stefan Meyer-Kahlen en 2000. Permite que cualquier interfaz gráfica de ajedrez (como Arena, Cute Chess, Fritz, ChessBase) pueda comunicarse e interactuar con cualquier motor de ajedrez compatible.

### Principios clave de UCI:
- **Separación de responsabilidades:** La GUI maneja la parte visual, el reloj y las entradas del usuario. El motor únicamente calcula movimientos y evalúa posiciones.
- **Comunicación asíncrona mediante Streams:** La GUI envía comandos por línea de texto (`stdin`) y el motor responde con líneas de texto (`stdout`).
- **Sin Estado Persistente en memoria externa:** El motor mantiene el estado del tablero internamente durante la sesión, pero la GUI le envía en cada turno la secuencia de jugadas o la posición actual en formato FEN.

---

## 2. Los Comandos Principales de UCI

A continuación se resumen los comandos esenciales que implementa PingunoChess:

| Comando enviado por la GUI | Respuesta del Motor / Propósito |
| :--- | :--- |
| `uci` | Responde con `id name`, `id author`, las opciones soportadas y finaliza con `uciok`. |
| `isready` | Pregunta si el motor está listo. Responde con `readyok`. |
| `setoption name <Nombre> value <Valor>` | Cambia el valor de una configuración del motor (ej. `setoption name OwnBook value true`). |
| `ucinewgame` | Informa que comenzará una nueva partida para que el motor reinicie sus estructuras. |
| `position startpos [moves e2e4 e7e5 ...]` | Configura el tablero en la posición inicial y aplica la lista opcional de movimientos. |
| `position fen <cadena_fen>` | Configura el tablero a partir de una notación FEN concreta. |
| `go [wtime X] [btime Y] [movetime Z]` | Inicia el cálculo de la jugada. |
| `bestmove <movimiento_uci>` | Salida enviada por el motor tras procesar `go` (ej. `bestmove e2e4` o `bestmove g1f3`). |
| `stop` | Solicita al motor detener la búsqueda de inmediato y devolver el `bestmove`. |
| `quit` | Solicita al motor cerrar el proceso de forma limpia. |

---

## 3. Demostración Práctica Paso a Paso

Sigue esta secuencia de comandos manual en tu terminal para simular una partida contra PingunoChess:

### Paso 1: Iniciar el motor
```bash
python pinguin_chess_motor_uci.py
```

### Paso 2: Inicializar el protocolo
Escribe:
```text
uci
```
*Respuesta recibida:*
```text
id name PingunoChess
id author Juan Felipe Garavito Arias
option name OwnBook type check default false
option name Debug Log File type string default
uciok
```

Escribe:
```text
isready
```
*Respuesta recibida:*
```text
readyok
```

### Paso 3: Indicar una nueva partida y la posición inicial
Escribe:
```text
ucinewgame
position startpos
```

### Paso 4: Pedir al motor que elija una jugada para las Blancas
Escribe:
```text
go wtime 300000 btime 300000
```
*Respuesta recibida (el movimiento específico puede variar si es aleatorio o según la lógica):*
```text
bestmove e2e4
```

### Paso 5: Simular la respuesta de las Negras y pedir nueva jugada
Supongamos que las negras responden con `e7e5`. Le enviamos al motor la historia del tablero:
```text
position startpos moves e2e4 e7e5
go wtime 295000 btime 298000
```
*Respuesta recibida:*
```text
bestmove g1f3
```

### Paso 6: Cerrar sesión
```text
quit
```

---

## 🧪 Ejercicio Práctico del Módulo 2

1. Inicia `pinguin_chess_motor_uci.py` en la terminal.
2. Utiliza una posición FEN de prueba con el comando `position fen`. Por ejemplo, la famosa posición de "Mate del Pasillo" o de una captura sencilla:
   ```text
   position fen r1bqkbnr/pppp1ppp/2n5/4p3/4P3/5N2/PPPP1PPP/RNBQKB1R w KQkq - 2 3
   ```
3. Ejecuta `go` y observa qué movimiento elige el motor (`bestmove`).
4. Revisa en `engine_log.txt` cómo se han registrado las interacciones.

---

¡Excelente! Ahora entiendes el flujo de comunicación UCI. Pasa al **[Módulo 3: Arquitectura y Lógica Interna](03_arquitectura_pinguinochess.md)**.
