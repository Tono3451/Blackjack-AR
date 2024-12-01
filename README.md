# Blackjack-AR

## Instalar el entorno de python para el proyecto

### Crear el entorno

Abre tu terminal o consola y ejecuta el siguiente comando para crear un nuevo entorno con un nombre específico, por ejemplo, `BlackjackAR`: acncahfuaehfuief

```bash
conda create --name=BlackjackAR python=3.11.5
```

### Activar el entorno

Una vez creado el entorno, actívalo con:

```bash
conda activate BlackjackAR
```

### Instalar los paquetes

Instala los paquetes en el entorno activado:

#### Instalar `numpy`

```bash
conda install numpy
```

#### Instalar `cv2` (OpenCV)

Para instalar OpenCV, puedes usar conda-forge:

```bash
conda install -c conda-forge opencv
```

#### Instalar `mediapipe`

Como `mediapipe` no está disponible en los canales de Conda, debes instalarlo usando `pip`:

```bash
pip install mediapipe
```

ffhuishsruigruigherig
