# BettingSystem Class

## Descripción
El `BettingSystem` es un sistema diseñado para gestionar apuestas en un juego. Utiliza un conjunto de valores de fichas (`ChipValue`) y estados (`BettingState`) para modelar las interacciones del usuario con una interfaz gráfica.

---

## Clases y Enumeraciones

### `BettingState`
Enumera los posibles estados del sistema de apuestas:
- **`WAITING`**: El sistema espera interacción del usuario.
- **`HOVERING`**: El usuario está seleccionando un chip o botón.
- **`SELECTED`**: Un chip ha sido seleccionado.
- **`CONFIRMING`**: Se está confirmando la apuesta.
- **`CONFIRMED`**: La apuesta ha sido confirmada.
- **`RESETTING`**: El sistema está reseteando la apuesta.

---

### `ChipValue`
Define los valores de las fichas disponibles para apostar:
- **`CHIP_100`**: Ficha de 100.
- **`CHIP_500`**: Ficha de 500.
- **`CHIP_1000`**: Ficha de 1000.
- **`CHIP_5000`**: Ficha de 5000.
- **`ALL_IN`**: Apuesta todo el balance.
- **`CONFIRM`**: Confirmar la apuesta.
- **`RESET`**: Resetear la apuesta.

---

### `BettingSystem`
El sistema principal que gestiona las apuestas. Sus funcionalidades incluyen:
- Manejar estados de apuestas.
- Detectar la posición de la mano para interacción.
- Mostrar una interfaz visual de apuestas.

---

## Métodos Principales

### `__init__(initial_balance)`
- **Parámetros:**
  - `initial_balance`: Balance inicial del jugador.
- **Descripción:** Inicializa el sistema con el balance proporcionado y configura el estado inicial.

---

### `setup_button_positions(frame_width, frame_height)`
- **Parámetros:**
  - `frame_width`: Ancho del marco de la interfaz.
  - `frame_height`: Altura del marco de la interfaz.
- **Descripción:** Configura las posiciones de los botones de `CONFIRM` y `RESET`.

---

### `process_hand_position(hand_landmarks, frame)`
- **Parámetros:**
  - `hand_landmarks`: Coordenadas de la posición de la mano detectada.
  - `frame`: Imagen o frame actual de la interfaz.
- **Descripción:** Determina qué chip o botón está siendo seleccionado en función de la posición de la mano.

---

### `draw_betting_ui(frame)`
- **Parámetros:**
  - `frame`: Frame donde se dibujará la interfaz gráfica.
- **Descripción:** Dibuja los elementos de la interfaz gráfica (fichas, botones, balance y apuesta actual).

---

### `reset_bet()`
- **Descripción:** Resetea la apuesta actual y devuelve el estado a `WAITING`.

---

### `get_current_bet()`
- **Retorno:** El valor de la apuesta actual.
- **Descripción:** Devuelve la cantidad apostada actualmente por el usuario.

---

## Flujo de Estados
1. **`WAITING`**: Espera a que el usuario interactúe con una ficha o botón.
2. **`HOVERING`**: La mano está posicionada sobre una ficha o botón.
3. **`SELECTED`**: Se selecciona una ficha y se actualiza la apuesta.
4. **`CONFIRMING`**: Se selecciona el botón de confirmar.
5. **`CONFIRMED`**: La apuesta es confirmada.
6. **`RESETTING`**: La apuesta es reseteada.