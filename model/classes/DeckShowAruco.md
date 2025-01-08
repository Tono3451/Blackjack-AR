# DeckShowAruco Class

## Descripción

La clase `DeckShowAruco` está diseñada para integrar marcadores ArUco en un contexto de juego interactivo, como un juego de cartas. Utiliza OpenCV para la detección de marcadores, renderización en tiempo real y cálculos necesarios para la proyección 3D, así como lógica del juego para manejar las reglas y resultados.

---

## Características Principales

### 1. **Inicialización**
   - **Diccionario ArUco**: Soporta diferentes diccionarios de marcadores, seleccionados según las necesidades.
   - **Parámetros de Cámara**: Utiliza la matriz de intrínsecos y coeficientes de distorsión para la calibración de cámara y renderización correcta.
   - **Carga de Recursos**: Admite carga de cartas y otros elementos visuales desde archivos locales para su uso en el juego.

### 2. **Renderización en Tiempo Real**
   - **Superposición de Cartas**: Renderiza cartas sobre los marcadores detectados con transformaciones de perspectiva.
   - **Texto Dinámico**: Permite mostrar texto sobre los marcadores con rotación, escalado y proyección 3D coherentes.
   - **Visualización de Ejes**: Incluye opciones de depuración para mostrar ejes 3D sobre los marcadores.

### 3. **Lógica del Juego**
   - **Cálculo del Valor de Manos**: Suma los valores de las cartas, teniendo en cuenta reglas específicas (e.g., ases).
   - **Mostrar Resultados**: Determina y muestra el estado del juego (e.g., "Win", "Lose", "Bust").

### 4. **Opciones de Depuración**
   - Proporciona información visual adicional durante el desarrollo.

---

## Métodos Principales

### Inicialización
- `__init__(camera_matrix, dist_coeffs, card_images, dict_name='DICT_6X6_250')`:
  Inicializa los parámetros de cámara, cartas y configuración de ArUco.

### Renderización
- `_add_image_on_aruco(frame, corners, image)`: Superpone una imagen en un marcador ArUco detectado.
- `_add_text_on_aruco(frame, corners, text, scale=1, color=(255, 255, 255))`: Muestra texto sobre un marcador.
- `_drawDealerHand(frame, dealer_hand, corners_dict)`: Renderiza las cartas del dealer sobre los marcadores correspondientes.
- `_drawPlayerHands(frame, player_hands, corners_dict)`: Renderiza las cartas de cada jugador sobre los marcadores.

### Lógica del Juego
- `_calculate_hand_value(hand)`: Calcula el valor de una mano de cartas según las reglas del juego.
- `show_result(frame, player_hands, dealer_hand, corners_dict)`: Evalúa y muestra el resultado del juego en pantalla.
- `show_game_over(frame)`: Renderiza una pantalla negra con "GAME OVER".