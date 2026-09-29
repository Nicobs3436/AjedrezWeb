# Ajedrez Web con IA

Aplicación web de ajedrez desarrollada con **React** y **JavaScript**, con un motor propio para gestionar el tablero, validar movimientos y jugar contra una inteligencia artificial basada en **Minimax con poda alfa-beta**.

El jugador controla las piezas blancas y la IA juega con negras.

---

## Características

- Tablero de ajedrez interactivo en el navegador.
- Selección de piezas mediante clic.
- Marcado visual de movimientos disponibles.
- Validación de movimientos según el tipo de pieza.
- Alternancia automática de turnos.
- Partidas **Humano vs IA**.
- Motor de ajedrez separado de la interfaz gráfica.
- IA basada en búsqueda Minimax con poda alfa-beta.
- Evaluación posicional de las posiciones.
- Tablas de transposición para reutilizar posiciones ya analizadas.
- Interfaz implementada completamente en React.

---

## Inteligencia artificial

La IA se encuentra en:

```text
frontend/src/core/AlfaBeta.js
```

Utiliza una búsqueda **Minimax con poda alfa-beta** para explorar posibles jugadas.

En la interfaz web actual se instancia con una profundidad de:

```text
3
```

### Función de evaluación

La evaluación de una posición tiene en cuenta varios factores:

- valor material de las piezas;
- tablas pieza-casilla;
- estructura de peones;
- peones pasados y aislados;
- seguridad del rey;
- piezas atacadas;
- control del centro;
- movilidad;
- actividad del rey durante el final.

Los valores base utilizados son aproximadamente:

| Pieza | Valor |
|---|---:|
| Peón | 100 |
| Caballo | 320 |
| Alfil | 330 |
| Torre | 500 |
| Dama | 900 |
| Rey | 20000 |

La IA también utiliza una **tabla de transposición** para almacenar evaluaciones de posiciones ya calculadas y evitar repetir parte del trabajo de búsqueda.

---

## Arquitectura

El proyecto separa la interfaz React de la lógica del juego.

```text
AjedrezWeb/
├── frontend/
│   ├── public/
│   └── src/
│       ├── App.js
│       ├── ChessBoard.js
│       ├── ChessBoard.css
│       └── core/
│           ├── AjedrezCore.js
│           ├── AlfaBeta.js
│           ├── ComprobarMovFichas.js
│           ├── EstadoAjedrez.js
│           ├── Humano.js
│           ├── Tablero.js
│           ├── funciones.js
│           └── jugar.js
├── .gitignore
└── README.md
```

### `ChessBoard.js`

Gestiona la interfaz del tablero:

- dibuja las piezas mediante caracteres Unicode;
- mantiene la selección actual;
- muestra movimientos disponibles;
- ejecuta la jugada del jugador;
- solicita inmediatamente la respuesta de la IA;
- muestra el estado final de la partida.

### `AjedrezCore.js`

Expone una interfaz sencilla sobre el motor:

- consulta del tablero;
- ejecución de movimientos;
- obtención de movimientos válidos;
- consulta del estado de la partida.

### `EstadoAjedrez.js`

Gestiona:

- el jugador actual;
- generación de estados sucesores;
- cambios de turno;
- aplicación de movimientos;
- detección del final según las reglas implementadas actualmente.

### `ComprobarMovFichas.js`

Contiene la lógica de movimiento para:

- peón;
- caballo;
- alfil;
- torre;
- dama;
- rey.

También verifica obstáculos para las piezas que se desplazan en línea.

---

## Tecnologías

- **React 19**
- **JavaScript**
- **CSS**
- **Create React App / react-scripts**
- Algoritmos de búsqueda adversaria
- Minimax
- Poda alfa-beta

El proyecto no necesita backend para ejecutar una partida.

---

## Instalación

Clona el repositorio:

```bash
git clone https://github.com/Nico3246/AjedrezWeb.git
cd AjedrezWeb/frontend
```

Instala las dependencias:

```bash
npm install
```

---

## Ejecución

Desde la carpeta `frontend`:

```bash
npm start
```

La aplicación se abrirá en el navegador utilizando el servidor de desarrollo de React.

Para generar una versión de producción:

```bash
npm run build
```

---

## Cómo jugar

1. El jugador comienza con las piezas blancas.
2. Selecciona una pieza haciendo clic sobre ella.
3. Las casillas consideradas válidas por el motor se resaltan.
4. Haz clic en la casilla de destino para realizar el movimiento.
5. Si el movimiento es válido, la IA calcula automáticamente su respuesta.
6. El proceso continúa hasta alcanzar la condición de final implementada por el motor.

---

## Estado actual y limitaciones

Este proyecto implementa un **motor de ajedrez simplificado** y está orientado principalmente al desarrollo y experimentación con algoritmos de IA.

Actualmente:

- el final de partida se determina por la captura de uno de los reyes;
- no se implementa todavía una detección reglamentaria completa de jaque y jaque mate;
- no se controla si un movimiento deja al propio rey en jaque;
- no están implementados el enroque, la captura al paso ni la promoción de peones;
- no existe selector de dificultad en la interfaz;
- no hay juego multijugador online;
- no hay backend ni persistencia de partidas.

Por tanto, el proyecto no pretende sustituir un motor de ajedrez completo, sino servir como implementación práctica de lógica de juego y búsqueda adversaria.

---

## Objetivo del proyecto

El objetivo principal es aplicar conceptos de **Inteligencia Artificial** a un entorno interactivo, especialmente:

- representación de estados;
- generación de sucesores;
- funciones heurísticas;
- Minimax;
- poda alfa-beta;
- optimización mediante tablas de transposición;
- integración de un motor lógico con una interfaz web.

---

## Posibles mejoras

- implementar jaque y jaque mate reglamentarios;
- añadir enroque, promoción y captura al paso;
- impedir movimientos que dejen al rey en jaque;
- añadir niveles de dificultad configurables;
- mejorar el ordenamiento de jugadas;
- incorporar iterative deepening;
- añadir historial de movimientos;
- permitir reiniciar una partida desde la interfaz;
- añadir modo Humano vs Humano;
- añadir pruebas automáticas del motor.
