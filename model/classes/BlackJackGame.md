# BlackjackGame Class

## Descripción
La clase `BlackjackGame` simula un juego de Blackjack, permitiendo al jugador apostar, tomar decisiones como pedir cartas, plantarse, dividir manos, y jugar contra el dealer. Utiliza un sistema de estados (`GameState`) para manejar el flujo del juego.

## Métodos Principales
- **`initialize_deck()`**: Crea y baraja un mazo de cartas.
- **`get_game_state()`**: Devuelve el estado actual del juego en forma de diccionario.
- **`can_split()`**: Determina si el jugador puede dividir su mano.
- **`process_action(action)`**: Procesa una acción del jugador, como pedir carta, plantarse, doblar o dividir.
- **`next_hand()`**: Cambia a la siguiente mano o inicia el turno del dealer.
- **`dealer_turn()`**: Ejecuta el turno del dealer, siguiendo las reglas del Blackjack.
- **`calculate_hand_value(hand)`**: Calcula el valor total de una mano considerando ases.
- **`deal_initial_cards()`**: Reparte las cartas iniciales al jugador y al dealer.
- **`place_bet(amount)`**: Permite al jugador realizar una apuesta.
- **`end_game()`**: Finaliza el juego y calcula las ganancias o pérdidas del jugador.

## Enumeración `GameState`
- **`WAITING_FOR_BET`**: El juego está esperando una apuesta.
- **`PLAYER_TURN`**: Es el turno del jugador.
- **`DEALER_TURN`**: Es el turno del dealer.
- **`GAME_OVER`**: La partida ha terminado.