# PingunoChess

[Versión en Español](README.md)

PingunoChess is a basic chess engine compatible with the UCI (Universal Chess Interface) protocol, written in Python. This engine is designed to be connected to chess Graphical User Interfaces (GUI) such as Arena, Cute Chess, or Scid vs. PC.

## Features

- **UCI Compatibility:** Supports basic UCI protocol commands, allowing integration with most modern chess interfaces.
- **Decision Logic (1-ply):**
  1. **Checkmate:** If it finds a move that results in an immediate checkmate, it plays it.
  2. **Captures:** If no checkmate is found, it searches for the best capture based on a scoring system (captured piece value, resulting position, and risk).
  3. **Random Move:** If no captures or checkmates are available, it chooses a legal move at random.
- **Options Support:** Allows configuration of basic options via the `setoption` command (e.g., `OwnBook`, `Debug Log File`).
- **Time Management:** Processes time parameters in the `go` command (`wtime`, `btime`, `winc`, `binc`, `movetime`), although it currently responds almost instantaneously.
- **Logging:** Generates an `engine_log.txt` file for debugging, recording communication between the GUI and the engine.

## Requirements

- **Python 3.x**
- **Python `chess` library:** Required for handling chess rules and board logic.

## Installation

1. Ensure Python is installed on your system.
2. Install the required library using pip:

```bash
pip install chess
```

3. Download the `pinguin_chess_motor_uci.py` file to your machine.

## Usage

### Direct Execution
You can run the engine from the terminal to verify it responds correctly to UCI commands:

```bash
python pinguin_chess_motor_uci.py
```
Once running, you can type `uci` and press Enter to see the engine's identification.

### Connecting to a GUI
To play against PingunoChess, you must add it as a new engine in your favorite chess software:
1. Open your chess GUI (e.g., Arena).
2. Go to the engine configuration section (Engines -> Install New Engine).
3. Select the Python executable and pass the `pinguin_chess_motor_uci.py` filename as an argument, or create an executable script to launch it.
4. Ensure the selected protocol is **UCI**.

## Technical Details

### Capture Evaluation
The engine evaluates captures considering:
- The value of the captured piece.
- Positional bonuses (center control).
- Penalties if the attacking piece becomes unprotected or is of higher value than the captured piece.
- Bonuses for proximity to the enemy king.

## Author
**Juan Felipe Garavito Arias** - *Lead Developer* - 2025-09-16
