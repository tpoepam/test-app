# Quiz CLI

Aplicación interactiva de preguntas de opción múltiple para terminal, pensada para practicar conceptos de JavaScript, Node.js y programación general. El proyecto también ilustra conceptos básicos de JavaScript moderno y Node.js, como ES modules, programación asíncrona, operaciones con archivos, entrada por consola y programación orientada a objetos.

## Tabla de contenidos

- [Características](#características)
- [Requisitos](#requisitos)
- [Instalación](#instalación)
- [Uso](#uso)
- [Estructura del proyecto](#estructura-del-proyecto)
- [Cómo funciona](#cómo-funciona)
- [Preguntas y categorías](#preguntas-y-categorías)
- [Pruebas](#pruebas)
- [Tecnologías y dependencias](#tecnologías-y-dependencias)
- [Licencia](#licencia)

## Características

- Selección interactiva de categoría y cantidad de preguntas.
- Preguntas barajadas aleatoriamente mediante Fisher–Yates.
- Indicador de progreso, puntuación, explicaciones y revisión de respuestas incorrectas.
- Interfaz de terminal con colores ANSI, sin dependencias externas.
- Posibilidad de repetir el cuestionario.

## Requisitos

- Node.js **18.0.0 o superior** (requisito declarado en `package.json`).
- npm, incluido normalmente con Node.js, para ejecutar los scripts del proyecto.
- Una terminal interactiva para responder a las preguntas.

## Instalación

El paquete de la aplicación está en `test-app/test-app`. Desde la raíz de este repositorio:

```bash
cd test-app/test-app
```

No se declaran dependencias de terceros en `package.json`; la aplicación utiliza módulos integrados de Node.js. Por tanto, no es necesario instalar paquetes adicionales. Para una instalación de dependencias reproducible si se incorporan dependencias en el futuro, puede usarse `npm install`.

## Uso

Desde `test-app/test-app`, inicia el programa con:

```bash
npm start
```

El comando ejecuta `node index.js`. También se puede iniciar directamente:

```bash
node index.js
```

Sigue las indicaciones de la terminal para elegir una categoría, escoger el número de preguntas disponibles, responder introduciendo el número de una opción y decidir si quieres volver a jugar. Las respuestas válidas se numeran desde `1`; el programa vuelve a solicitar la entrada si se introduce una opción fuera de rango.

Las categorías y cantidades disponibles actualmente son:

| Categoría | Preguntas |
| --- | ---: |
| JavaScript Basics | 5 |
| Node.js Fundamentals | 5 |
| General Programming | 5 |

La aplicación presenta todas las preguntas de la categoría por defecto y ofrece opciones de 3 o 5 preguntas cuando hay suficientes. Al finalizar muestra el resultado y las respuestas incorrectas para repaso.

## Estructura del proyecto

```text
.
├── README.md
└── test-app/
    └── test-app/
        ├── data/
        │   └── questions.json  # Categorías, preguntas, opciones, respuestas y explicaciones
        ├── src/
        │   ├── colors.js       # Utilidades de formato ANSI para la terminal
        │   ├── input.js        # Interfaz readline y prompts interactivos
        │   └── quiz.js         # Lógica de cuestionario, puntuación y resultados
        ├── index.js            # Punto de entrada y flujo principal de la aplicación
        └── package.json        # Metadatos, scripts, tipo de módulo y versión mínima de Node
```

## Cómo funciona

1. `index.js` carga `data/questions.json` con `node:fs/promises` y muestra el menú de categorías.
2. `src/input.js` gestiona los prompts de consola con el módulo integrado `node:readline`.
3. `src/quiz.js` crea una instancia de `Quiz`, baraja las preguntas, valida las respuestas seleccionadas y mantiene el progreso y la puntuación.
4. La aplicación muestra el resultado final, las respuestas erróneas y sus respuestas correctas, y pregunta si se desea jugar otra vez.
5. `src/colors.js` aplica estilos mediante secuencias ANSI. No se utiliza ninguna biblioteca de color externa.

## Preguntas y categorías

El archivo `test-app/test-app/data/questions.json` contiene un objeto `categories`. Cada categoría tiene un nombre y una lista de preguntas; cada pregunta contiene `question`, `options`, `answer` y, opcionalmente, `explanation`. El campo `answer` es un índice de base cero en `options` (por ejemplo, `0` identifica la primera opción). Para ampliar el cuestionario, añade entradas siguiendo esta estructura y conserva índices de respuesta válidos.

## Pruebas

El proyecto declara este script:

```bash
npm test
```

Ejecuta `node --test` desde `test-app/test-app`. No se encontraron archivos de pruebas en la estructura disponible, así que el repositorio no documenta actualmente casos de prueba propios.

## Tecnologías y dependencias

- JavaScript con módulos ES (`"type": "module"`).
- Node.js y sus módulos integrados: `node:fs/promises`, `node:path`, `node:url` y `node:readline`.
- No hay dependencias npm de terceros declaradas.
- Scripts npm: `start` y `test`.

## Licencia

El `package.json` declara la licencia **MIT**.
