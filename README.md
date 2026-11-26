# Quiz CLI

Aplicación interactiva de preguntas de opción múltiple para terminal. Permite practicar conceptos de JavaScript, Node.js y programación general mediante cuestionarios organizados por categorías.

## Características

- Selección interactiva de categoría y cantidad de preguntas.
- Preguntas seleccionadas al azar mediante el algoritmo Fisher–Yates.
- Barra de progreso, puntuación, explicaciones y repaso de respuestas incorrectas.
- Interfaz de consola con colores ANSI, sin dependencias externas.
- Opción para volver a jugar al finalizar.

## Requisitos

- Node.js **18.0.0 o superior**.
- npm para ejecutar los scripts definidos en el paquete.
- Una terminal interactiva.

## Instalación

Desde la raíz del repositorio, cambia al directorio que contiene `package.json`:

```bash
cd test-app/test-app
```

No hace falta instalar dependencias adicionales: el proyecto utiliza módulos integrados de Node.js y `package.json` no declara dependencias npm de terceros.

## Uso

Inicia el cuestionario desde `test-app/test-app`:

```bash
npm start
```

También puedes ejecutarlo directamente:

```bash
node index.js
```

El programa te guiará para elegir una categoría, seleccionar cuántas preguntas responder y contestar cada pregunta introduciendo el número de una opción. Si la entrada no corresponde a una opción válida, volverá a solicitarla. Antes de cada pregunta (y antes de comenzar) se puede pulsar Enter para continuar. Al finalizar se muestra el resultado y se ofrece jugar otra vez (`y` para sí).

Ejemplo del menú que presenta la aplicación:

```text
Choose a category:
  1. JavaScript Basics
  2. Node.js Fundamentals
  3. General Programming

Your choice (enter number): 1
How many questions?
  1. All questions
  2. 3 questions
  3. 5 questions
```

Las categorías incluidas contienen cinco preguntas cada una:

| Categoría | Número de preguntas |
| --- | ---: |
| JavaScript Basics | 5 |
| Node.js Fundamentals | 5 |
| General Programming | 5 |

La opción `All questions` utiliza todas las preguntas disponibles de la categoría. Las opciones de 3 y 5 preguntas aparecen si la categoría tiene suficientes preguntas.

## Estructura del proyecto

```text
.
├── README.md
└── test-app/
    └── test-app/
        ├── data/
        │   └── questions.json  # Categorías, preguntas, opciones, respuestas y explicaciones
        ├── src/
        │   ├── colors.js       # Formato ANSI para la terminal
        │   ├── input.js        # Entrada interactiva con readline
        │   └── quiz.js         # Barajado, flujo, puntuación y resultados
        ├── index.js            # Punto de entrada y carga de datos
        └── package.json        # Metadatos, scripts y requisitos de Node.js
```

## Arquitectura y funcionamiento

- `index.js` carga `data/questions.json` usando `node:fs/promises`, muestra la bienvenida y coordina el ciclo principal del juego.
- `src/input.js` implementa selección de opciones, confirmaciones y pausas mediante el módulo integrado `node:readline`.
- `src/quiz.js` contiene la clase `Quiz`: baraja preguntas con Fisher–Yates, registra respuestas y puntuación, muestra el progreso y presenta los resultados.
- `src/colors.js` proporciona funciones de formato con secuencias ANSI.
- Al terminar, el programa muestra la puntuación, un mensaje según el rendimiento y, si hubo errores, las respuestas correctas para repaso.

## Datos de preguntas

Las categorías y preguntas se mantienen en `test-app/test-app/data/questions.json`. El archivo contiene un objeto `categories`; cada categoría tiene un `name` y un arreglo `questions`. Cada pregunta usa esta estructura:

```json
{
  "question": "Texto de la pregunta",
  "options": ["Opción A", "Opción B", "Opción C"],
  "answer": 1,
  "explanation": "Explicación opcional de la respuesta."
}
```

`answer` es el índice basado en cero de la respuesta correcta dentro de `options` (en el ejemplo, la segunda opción). Para añadir preguntas, conserva esa estructura y asegúrate de que el índice corresponda a una opción existente. `explanation` es opcional.

## Scripts disponibles

Ejecuta estos comandos desde `test-app/test-app`:

| Comando | Acción |
| --- | --- |
| `npm start` | Inicia la aplicación (`node index.js`). |
| `npm test` | Ejecuta el test runner integrado de Node.js (`node --test`). |

No se encontraron archivos de pruebas en la estructura disponible; `npm test` ejecuta el runner, pero el repositorio no documenta casos propios.

## Configuración y dependencias

No se definen variables de entorno ni archivos de configuración adicionales. El proyecto utiliza módulos ES (`"type": "module"`) y módulos integrados de Node.js, incluidos `node:fs/promises`, `node:path`, `node:url` y `node:readline`. No hay dependencias npm de terceros declaradas.

## Licencia

El archivo `package.json` declara la licencia MIT.
