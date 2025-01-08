# Blackjack-AR

## Instalación del entorno

### Crear el entorno

Dentro de la consola de anaconda se crea un entorno con el nombre `BlackjackAR`:

```bash
conda create --name=BlackjackAR python=3.11.5
```

### Activar el entorno

Una vez creado el entorno, se activa mediante:

```bash
conda activate BlackjackAR
```

### Instalar los paquetes

Instalar los paquetes en el entorno activado:

#### Instalar `numpy`

```bash
conda install numpy
```

#### Instalar `cv2` (OpenCV)

Instalar la versión de openCV que contiene las utilidades para manejar ArUco:

```bash
pip3 install opencv-contrib-python==4.6.0.66
```

#### Instalar `mediapipe`

Instalar `mediapipe` encargado del reconocimiento de manos:

```bash
pip install mediapipe
```

## Reglas del Blackjack

Para esta demostración, el juego seguirá las reglas básicas del Blackjack que se encuentran en [la página de Wikipedia](https://es.wikipedia.org/wiki/Blackjack) con ciertas restricciones.

-----------------------

## Vídeo de demostracción

Se presenta un vídeo en el cual se puede apreciar una partida normal. (poner link del vídeo aquí coño de youtube)
