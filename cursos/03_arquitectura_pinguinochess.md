# Módulo 3: Arquitectura y Lógica Interna de PingunoChess

En este módulo examinaremos minuciosamente el código fuente de `pinguin_chess_motor_uci.py`. Entenderás cómo se estructuran las funciones, el sistema de evaluación de capturas 1-ply y la jerarquía de toma de decisiones del motor.

---

## 1. Estructura General del Código

El archivo `pinguin_chess_motor_uci.py` contiene aproximadamente 180 líneas de código organizadas en 3 secciones principales:

1. **Configuración y Logging (`log()`):** Manejo del archivo `engine_log.txt`.
2. **Lógica de Evaluación (`evaluate_capture()`, `find_best_move()`):** Criterio ajedrecístico del motor.
3. **Bucle UCI (`uci_loop()`):** Procesador de comandos de entrada y formateador de salidas.

---

## 2. El Sistema de Evaluación (1-ply)

Un motor de ajedrez básico de "1-ply" analiza únicamente las jugadas legales en el turno actual (1 medio-movimiento hacia adelante), sin simular las posibles respuestas profundas del oponente.

PingunoChess utiliza las siguientes tablas de puntuación:

### Valores Materiales de las Piezas
```python
PIECE_VALUES_CAPTURE = {
    chess.PAWN: 100,
    chess.KNIGHT: 300,
    chess.BISHOP: 300,
    chess.ROOK: 500,
    chess.QUEEN: 900,
    chess.KING: 3900
}
```

### Bonificaciones Posicionales (Control del Centro)
El motor favorece casillas centrales (`d4`, `e4`, `d5`, `e5`) otorgando +12 puntos, casillas circundantes +6 puntos, y casillas secundarias +3 puntos.

```python
POSITIONAL_SCORES = {}
for square in ['d4', 'e4', 'd5', 'e5']:
    POSITIONAL_SCORES[chess.parse_square(square)] = 12
# ... casillas circundantes ...
```

---

## 3. Función `evaluate_capture(board, move)`

Esta función calcula un puntaje para cada jugada de captura disponible. Considera:

1. **Valor de la pieza capturada:** Suma los puntos materiales (`PIECE_VALUES_CAPTURE`).
2. **Bonificación posicional:** Evalúa el valor de la casilla destino (`POSITIONAL_SCORES`).
3. **Riesgo y Contra-ataque:**
   - Hace una simulación previa de la jugada (`temp_board.push(move)`).
   - Si la casilla destino queda atacada por el rival, descuenta una penalización por riesgo (`PIECE_VALUES_RISK`).
   - Ajusta según el número de defensores propios (+24 por defensor) y atacantes rivales (-25 por atacante).
   - Otorga una pequeña bonificación (+3) por cercanía a los reyes.

---

## 4. Jerarquía de Toma de Decisiones: `find_best_move(board)`

Cuando la GUI le ordena al motor calcular una jugada mediante el comando `go`, se invoca `find_best_move(board)`. Esta función sigue un orden estricto de prioridades:

```text
               ┌─────────────────────────────┐
               │    Obtener jugadas legales  │
               └──────────────┬──────────────┘
                              │
               ┌──────────────▼──────────────┐
               │  ¿Existe un Jaque Mate      │ ─── SÍ ───► Realizar Mate
               │       inmediato?            │
               └──────────────┬──────────────┘
                              │ NO
               ┌──────────────▼──────────────┐
               │   ¿Existen Capturas?        │ ─── SÍ ───► Evaluar con evaluate_capture()
               └──────────────┬──────────────┘              y elegir la de mayor puntaje.
                              │ NO
               ┌──────────────▼──────────────┐
               │ Elegir Movimiento Aleatorio │
               │   dentro de las legales     │
               └─────────────────────────────┘
```

---

## 5. El Bucle Principal `uci_loop()`

Esta función se ejecuta indefinidamente en un bucle `while True:`.
- Utiliza `sys.stdin.readline().strip()` para leer cada línea recibida.
- Cada interacción recibida o respuesta enviada queda grabada en `engine_log.txt` a través de la función `log()`.
- Procesa el comando `position` reescribiendo la variable `board` (`chess.Board()`), y aplicando la secuencia de jugadas pasadas mediante `board.push_uci(move_uci)`.

---

## 🧪 Ejercicio Práctico del Módulo 3

1. Abre `pinguin_chess_motor_uci.py` en tu editor.
2. Localiza el diccionario `PIECE_VALUES_CAPTURE`.
3. ¿Qué sucedería si cambiáramos el valor de `chess.KNIGHT` a `400` y el del alfil a `300`?
4. Modifica temporalmente la bonificación por cercanía al rey enemigo a `+20` en lugar de `+3` y prueba cómo responde el motor ante situaciones con el rey expuesto.

---

¡Excelente! Ya entiendes las entrañas de PingunoChess. Pasa al **[Módulo 4: Conexión con GUIs](04_conexion_gui.md)**.
