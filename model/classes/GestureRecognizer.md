# GestureRecognizer Class

## Descripción
La clase `GestureRecognizer` utiliza la biblioteca MediaPipe Hands para detectar gestos de la mano que corresponden a acciones de Blackjack definidas en la enumeración `BlackjackAction`. Estos gestos se traducen en comandos como pedir carta, plantarse, doblar o dividir.

## Enumeración `BlackjackAction`
- **`NONE`**: Ninguna acción detectada.
- **`HIT`**: Pedir carta (un dedo levantado: índice).
- **`STAND`**: Plantarse (puño cerrado).
- **`DOUBLE`**: Doblar la apuesta (dos dedos levantados: índice y medio).
- **`SPLIT`**: Dividir las cartas (dos dedos levantados: pulgar e índice).

## Métodos Principales
- **`detect_gesture(hand_landmarks)`**: Detecta el gesto de la mano y retorna la acción de Blackjack correspondiente.
- **`count_fingers_up(hand_landmarks)`**: Cuenta los dedos levantados y si es la mano derecha o izquierda.
- **`draw_debug_info(frame, action, hand_landmarks, fingers_up, is_right_hand)`**: Dibuja información de depuración en el frame, incluyendo la acción detectada y el estado de los dedos.
- **`draw_hand_landmarks(frame, hand_landmarks)`**: Dibuja los landmarks de la mano en el frame.

## Métodos Internos (Privados)
- **`_is_hit_gesture(total_fingers, fingers_up)`**: Detecta el gesto para pedir carta.
- **`_is_stand_gesture(total_fingers, fingers_up)`**: Detecta el gesto para plantarse.
- **`_is_double_gesture(total_fingers, fingers_up)`**: Detecta el gesto para doblar la apuesta.
- **`_is_split_gesture(total_fingers, fingers_up)`**: Detecta el gesto para dividir las cartas. 
