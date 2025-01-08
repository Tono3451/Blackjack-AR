## Descipción de las clases que componen el modelo de BlackJackAR

- [Card](classes/Card.md)
- [BlackJackGame](classes/BlackJackGame.md)
- [BettingSystem](classes/BettingSystem.md)
- [GestureRecognizer](classes/GestureRecognizer.md)
- [DeckShowAruco](classes/DeckShowAruco.md)


## Código depurado

Esta versión del código, muestra el estado del juego por consola y permite ver las detecciones visuales usadas para el funcionamiento del juego: detección del aruco, landmarks de la mano y que poses esta accionando el jugador.


### Inicialización de las partes
Se procede a inicializar cada herramienta que se usará para el funcionamiento del juego y muestra la cantidad de fichas inicial del usuario por consola.

```bash
    deckShowAruco = DeckShowAruco(True)                                                 # Clase para detectar aruco y visualizar cartas
    game = BlackjackGame()                                                              # Inicializar el juego
    gesture_recognizer = GestureRecognizer()                                            # Inicializar el reconocedor de movimientos
    betting_system = BettingSystem(game.player_chips)                                   # Inicializar la interfaz para apostar                   
    
    action_cooldown = 0
    flag_game_over = False
    show_result = True
    
    print("\n¡Bienvenido al Blackjack!")
    print(f"Tienes {game.player_chips} fichas.")
```

### Capturación de la cámara
Analiza frame por frame la cámara comprobando si hay una mano.

```bash
cap = cv2.VideoCapture(0)
    
    with gesture_recognizer.mp_hands.Hands(
            model_complexity=0,
            min_detection_confidence=0.5,
            min_tracking_confidence=0.5) as hands:

        while True:
            ret, frame = cap.read()
            if not ret:
                break
            
            frame_RGB = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)
            results = hands.process(frame_RGB)
            
            current_action = BlackjackAction.NONE
```


### Espera que el jugador introduzca una apuesta.
Habiendo inicializado el procesamiento de la mano, detecta el punto más alto del dedo índice. Según la posición de dicho punto en la pantalla se elige la apuesta introducida. También en todo momento se muestra los landmarks de la mano, y a través de la consola se informa de la apuesta indicada.

```bash
            if game.game_state == GameState.WAITING_FOR_BET: 
                betting_system.draw_betting_ui(frame)

            if results.multi_hand_landmarks:
                for hand_landmarks in results.multi_hand_landmarks:

                    # Dibujar información de los landmarks de la mano
                    num_fingers_up, fingers_up, is_right_hand = gesture_recognizer.count_fingers_up(hand_landmarks)
                    gesture_recognizer.draw_hand_landmarks(frame, hand_landmarks)

                    # Espera a que el jugador introduzca una apuesta
                    if game.game_state == GameState.WAITING_FOR_BET:
                        bet_state = betting_system.process_hand_position(hand_landmarks, frame)
                        if bet_state == BettingState.CONFIRMED:
                            amount = betting_system.get_current_bet()
                            success = game.place_bet(amount)
                            if not success:
                                print("Error al colocar la apuesta inicial")
                                return
                            print(f"Apuesta inicial de {amount} fichas colocada.")

                            print_game_state(game)
```


### Detección de movimientos y acciones del jugador.
En esta parte del código, se detecta que gesto está haciendo el jugador y se realiza la acción del juego que corresponda. Muestra dichas acciones en el frame y por consola se informa de las desiciones tomadas y las consecuencias de las mismas en el juego. También se aplica un enfriamiento de 15 frames para introducir una nueva acción.

```bash
                    # Detecta los movimientos del jugador y realiza la acción correspondiente
                    elif game.game_state == GameState.PLAYER_TURN:
                        current_action = gesture_recognizer.detect_gesture(hand_landmarks)
                        gesture_recognizer.draw_debug_info(frame, current_action, hand_landmarks, fingers_up, is_right_hand)

                        if (current_action != BlackjackAction.NONE and action_cooldown == 0):
                            success, message = game.process_action(current_action)
                            if success:
                                print(f"\n{message}")
                                print_game_state(game)
                                action_cooldown = 15  # Esperar 15 frames antes de aceptar otra acción
```

### Muestreo del resultado de las acciones
Muestra el resultado de las acciones del jugador y reduce el enfriamiento para introducir una nueva acción.

```bash
            if game.game_state == GameState.PLAYER_TURN:
                frame = deckShowAruco.drawCards(frame, game.dealer_hand, game.player_hands)

            # Reducir el cooldown
            if action_cooldown > 0:
                action_cooldown -=1
```

### Resultados del juego
En caso de que el juego haya terminado, se muestran los resultados tanto en consola como en el frame.
```bash
            # Si el juego ha terminado, mostrar resultados y reiniciar
            if game.game_state == GameState.GAME_OVER:
                frame = deckShowAruco.drawCards(frame, game.dealer_hand, game.player_hands, True)
                if show_result:
                    print("\n¡Juego terminado!")
                    print(f"Tus fichas: {game.player_chips}")
                    show_result = False
```

### Jugar nueva partida
Si se supera la cantidad de la apuesta mínima, se repite el proceso anterior de introducir la cantidad a apostar y se vuelve a jugar.

```bash
                # Enter para jugar otra mano
                if cv2.waitKey(1) & 0xFF == 13:
                    if game.player_chips >= 100:                # Asegurar que tiene suficientes fichas
                        chips = game.player_chips
                        game = BlackjackGame()
                        game.player_chips = chips               # Mantener las fichas ganadas
                        betting_system = BettingSystem(game.player_chips)
```

### Terminación de la partida
En caso de que el jugador no disponga de la apuesta mínima, se muestra una pantalla indicando que es el fin del juego y acaba.

```bash
                    else:
                        while True:
                            frame = deckShowAruco.show_game_over(frame)
                            cv2.imshow('Blackjack AR', frame)
                            if cv2.waitKey(1) & 0xFF == ord('q'):
                                flag_game_over = True
                                break
            
            if (flag_game_over):
                break

            cv2.imshow('Blackjack AR', frame)
            
            if cv2.waitKey(1) & 0xFF == ord('q'):
                break
    
    cap.release()
    cv2.destroyAllWindows()
```


## Vídeo ejemplo del código depurado

    PONER VIDEO Y FOTOS DE LA CONSOLA CON EL ESTADO DEL JUEGO