# Módulo 5: Ejercicios Prácticos y Extensión del Motor

¡Felicidades por llegar al último módulo! Ahora que entiendes cómo funciona el protocolo UCI, la arquitectura de PingunoChess y cómo integrarlo con GUIs, es momento de poner a prueba tus conocimientos y llevar el motor al siguiente nivel.

---

## 🚀 Retos y Ejercicios Prácticos

A continuación se presentan una serie de retos de dificultad progresiva para que implementes en `pinguin_chess_motor_uci.py`.

---

### Reto 1: Medidor de Evaluación (Score Info)
**Objetivo:** Transmitir a la GUI la evaluación estimada en centipeones (*cp*) para que la barra de ventaja de la GUI cambie dinámicamente.

**Descripción:**
El protocolo UCI permite que el motor envíe información sobre la evaluación antes de responder con `bestmove`. La sintaxis es:
```text
info score cp <puntuación>
```
1. Edita la función `find_best_move(board)`.
2. Cuando evalúes las jugadas o selecciones la mejor, calcula el puntaje final.
3. Imprime por `sys.stdout.write` la línea de `info score cp <valor>` antes de enviar `bestmove`.

---

### Reto 2: Soporte para Tablas de Transposición / Evitar Repetición de Jugadas
**Objetivo:** Evitar que el motor caiga en tablas por triple repetición cuando va ganando.

**Descripción:**
1. Actualmente, si no hay capturas ni jaque mate, PingunoChess elige una jugada legal aleatoria (`random.choice(legal_moves)`).
2. Si esa jugada provoca una repetición de posición (`board.is_repetition()`), el motor podría empatar involuntariamente una partida ganada.
3. Filtra la lista de `legal_moves` para descartar aquellas jugadas que resulten en repetición de posición a menos que no haya otra opción.

---

### Reto 3: Incorporación de Búsqueda Minimax (Profundidad 2 o más)
**Objetivo:** Permitir que el motor anticipe la respuesta del oponente.

**Descripción:**
Actualmente el motor es de **1-ply** (solo ve su propio turno). Un motor de **2-ply** evalúa: *"Si yo hago el movimiento X, ¿cuál es la mejor respuesta Y de mi oponente?"*.

1. Implementa una función recursiva `minimax(board, depth, is_maximizing)` o un algoritmo **Negamax**.
2. Define una función de evaluación global del tablero (evaluación material total = suma de piezas blancas - suma de piezas negras).
3. Modifica `find_best_move` para llamar a `minimax` con `depth = 2` o `depth = 3`.

---

### Reto 4: Añadir la Opción UCI "Difficulty" o "Style"
**Objetivo:** Crear una opción personalizada configurable desde la GUI.

**Descripción:**
1. En el diccionario `OPTIONS`, agrega una opción como:
   ```python
   "Aggressiveness": {"type": "spin", "default": "50", "min": "0", "max": "100", "value": "50"}
   ```
2. Modifica la ponderación de las capturas en `evaluate_capture()` multiplicando la recompensa por captura según el valor de `Aggressiveness`.

---

## 💡 Recursos Adicionales para Continuar Aprendiendo

- **Documentación oficial de `python-chess`:** [https://python-chess.readthedocs.io/](https://python-chess.readthedocs.io/)
- **Especificación Oficial del Protocolo UCI:** [http://w3.gaviota.org/chess/uci.html](http://w3.gaviota.org/chess/uci.html)
- **Chess Programming Wiki (CPW):** [https://www.chessprogramming.org/](https://www.chessprogramming.org/) - La enciclopedia definitiva sobre desarrollo de motores de ajedrez (Minimax, Poda Alfa-Beta, Bitboards, Transposition Tables).

---

¡Esperamos que hayas disfrutado este curso! Con estos conocimientos estás listo para desarrollar tus propios motores de ajedrez y experimentar con IA aplicada al juego.
