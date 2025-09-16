# -*- coding: utf-8 -*-

"""
==============================================================================
                          MOTOR DE AJEDREZ - VERSIÓN UCI
==============================================================================
Descripción:
Este es un motor de ajedrez compatible con el protocolo UCI (Universal Chess 
Interface). No incluye una interfaz gráfica (GUI), por lo que debe ser 
conectado a un software de ajedrez compatible con UCI (como Arena, Cute Chess,
o Scid vs. PC) para poder jugar contra él.

La lógica de decisión se basa en una jerarquía de reglas:
1.  Si puede dar jaque mate, lo hace.
2.  Si no, busca la mejor captura posible según un sistema de puntuación.
3.  Si no hay capturas, realiza un movimiento legal aleatorio.

Autor: Juan Felipe Garavito Arias.
Fecha: 2025-09-16
==============================================================================
"""

import chess
import random
import math
import sys

# Para depuración, el motor escribirá un log de lo que recibe y envía.
LOG_FILE = "engine_log.txt"

def log(message):
    """Escribe un mensaje en el archivo de log."""
    with open(LOG_FILE, "a") as f:
        f.write(message + "\n")

# ==============================================================================
# LÓGICA DE EVALUACIÓN (Sin cambios respecto a la versión anterior)
# ==============================================================================

PIECE_VALUES_CAPTURE = {
    chess.PAWN: 100, chess.KNIGHT: 300, chess.BISHOP: 300,
    chess.ROOK: 500, chess.QUEEN: 900, chess.KING: 3900
}
PIECE_VALUES_RISK = {
    chess.PAWN: 130, chess.KNIGHT: 390, chess.BISHOP: 390,
    chess.ROOK: 650, chess.QUEEN: 1170, chess.KING: 5070
}
POSITIONAL_SCORES = {}
for square in ['d4', 'e4', 'd5', 'e5']: POSITIONAL_SCORES[chess.parse_square(square)] = 12
for square in ['c3', 'd3', 'e3', 'f3', 'c4', 'f4', 'c5', 'f5', 'c6', 'd6', 'e6', 'f6']: POSITIONAL_SCORES[chess.parse_square(square)] = 6
for square in ['b2', 'c2', 'd2', 'e2', 'f2', 'g2', 'b3', 'g3', 'b4', 'g4', 
               'b5', 'g5', 'b6', 'g6', 'b7', 'c7', 'd7', 'e7', 'f7', 'g7']: POSITIONAL_SCORES[chess.parse_square(square)] = 3

def evaluate_capture(board, move):
    """Calcula la puntuación de una jugada de captura."""
    score = 0
    attacking_piece = board.piece_at(move.from_square)
    captured_piece = board.piece_at(move.to_square)
    if board.is_en_passant(move): captured_piece = chess.Piece(chess.PAWN, not board.turn)
    if attacking_piece is None or captured_piece is None: return -math.inf
    score += PIECE_VALUES_CAPTURE.get(captured_piece.piece_type, 0)
    score += POSITIONAL_SCORES.get(move.to_square, 0)
    temp_board = board.copy()
    temp_board.push(move)
    if temp_board.is_attacked_by(not board.turn, move.to_square):
        score -= PIECE_VALUES_RISK.get(attacking_piece.piece_type, 0)
    own_defenders = len(board.attackers(board.turn, move.to_square))
    score += own_defenders * 24
    opponent_attackers = len(board.attackers(not board.turn, move.to_square))
    score -= opponent_attackers * 25
    if chess.square_distance(board.king(not board.turn), move.to_square) == 1: score += 3
    if chess.square_distance(board.king(board.turn), move.to_square) == 1: score += 3
    return score

def find_best_move(board):
    """Encuentra la mejor jugada (la lógica de decisión no cambia)."""
    legal_moves = list(board.legal_moves)
    for move in legal_moves:
        temp_board = board.copy()
        temp_board.push(move)
        if temp_board.is_checkmate():
            log("Motor: ¡Encontré un jaque mate!")
            return move
    
    best_capture = None
    max_score = -math.inf
    capture_moves = [move for move in legal_moves if board.is_capture(move)]
    
    if capture_moves:
        for move in capture_moves:
            score = evaluate_capture(board, move)
            if score > max_score:
                max_score = score
                best_capture = move
        if best_capture:
            log(f"Motor: Mejor captura encontrada: {board.san(best_capture)} con puntaje: {max_score}")
            return best_capture
            
    log("Motor: No hay mates ni capturas. Realizando un movimiento aleatorio.")
    return random.choice(legal_moves)

# ==============================================================================
# BUCLE PRINCIPAL UCI
# ==============================================================================

def uci_loop():
    """
    Bucle principal que escucha los comandos UCI desde stdin y responde a stdout.
    """
    board = chess.Board()
    log("Motor UCI iniciado.")
    
    while True:
        # Lee un comando de la GUI
        line = sys.stdin.readline().strip()
        log(f"GUI -> Engine: {line}")
        
        if not line:
            continue
            
        if line == "quit":
            log("Motor: Recibido comando 'quit'.")
            break
            
        if line == "uci":
            sys.stdout.write("id name PingunoChess\n")
            sys.stdout.write(f"id author Juan Felipe Garavito Arias\n")
            sys.stdout.write("uciok\n")
            sys.stdout.flush()
        
        elif line == "isready":
            sys.stdout.write("readyok\n")
            sys.stdout.flush()
            
        elif line == "ucinewgame":
            board = chess.Board() # Resetea el tablero para una nueva partida
            
        elif line.startswith("position"):
            parts = line.split()
            # Carga la posición inicial o una desde FEN
            if parts[1] == "startpos":
                board = chess.Board()
                moves_start_index = 2
            elif parts[1] == "fen":
                fen = " ".join(parts[2:8])
                board = chess.Board(fen)
                moves_start_index = 8
            else:
                continue

            # Aplica los movimientos que se han hecho en la partida
            if len(parts) > moves_start_index and parts[moves_start_index] == "moves":
                for move_uci in parts[moves_start_index+1:]:
                    board.push_uci(move_uci)

        elif line.startswith("go"):
            # La GUI pide al motor que piense y encuentre un movimiento
            best_move = find_best_move(board)
            # El motor responde con su mejor jugada en formato UCI (ej: "e2e4")
            sys.stdout.write(f"bestmove {best_move.uci()}\n")
            sys.stdout.flush()

if __name__ == "__main__":
    # Limpia el archivo de log al iniciar
    with open(LOG_FILE, "w") as f:
        f.write("")
    uci_loop()
