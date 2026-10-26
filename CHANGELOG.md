# Historial de Cambios (Changelog)

Todos los cambios notables de este proyecto se documentan en este archivo.
El formato se basa en [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/)
y este proyecto se adhiere a [Semantic Versioning](https://semver.org/lang/es/).

## [Unreleased]

## [v1.5.0] - 2026-10-26

### Added
- Mapeo explícito en el tokenizador plano `#ejs-js-interior` hacia los scopes nativos exactos de `JavaScript.tmLanguage.json` de VS Code:
  - Propiedades nativas DOM/JS (`.length`, `.prototype`, `.value`, `.style`, etc.) → `support.variable.property.js`.
  - Objetos receptores de acceso a propiedad (`peliculas.`, `pelicula.`) → `variable.other.object.js`.
  - Propiedades de usuario (`.Title`, `.Genre`, `.imdbRating`) → `variable.other.property.js`.
  - Métodos nativos de Array/String (`.forEach`, `.map`, `.filter`, `.includes`, `.trim`) → `support.function.js`.
  - Parámetros de callbacks arrow (`(pelicula) =>`) → `variable.parameter.js`.
  - Identificadores `const` / mayúsculas → `variable.other.constant.js`.
- Restauración de `"contentName": "source.js"` en bloques EJS válidos (`#ejs-output-escaped`, `#ejs-output-unescaped`, `#ejs-scriptlet`) para activar reglas de temas basadas en contexto (`source.js variable...`) sin invocar la gramática recursiva de bloques JS.

## [v1.4.0] - 2026-10-26

### Fixed
- Separación física entre la gramática de lenguaje base (`syntaxes/ejs.tmLanguage.json`, que incluye `text.html.basic`) y la gramática de inyección (`syntaxes/ejs-injection.tmLanguage.json`, que solo inyecta `#ejs-tag` y `#ejs-in-attribute` sin re-inyectar `text.html.basic`).
- Sustitución de `"include": "source.js"` dentro de etiquetas EJS por un tokenizador léxico plano (`#ejs-js-interior`) que nunca abre sub-bloques `meta.block.js` al encontrar `{` o `(`, impidiendo que una llave abierta en `<% if (...) { %>` secuestre el cierre `%>` y rompa el coloreado HTML posterior.

## [v1.3.1] - 2026-10-26

### Fixed
- Eliminación de la regla de cierre huérfano (`#ejs-error-orphan-close`) que, al inyectarse con prioridad `L:`, capturaba los cierres `%>` legítimos antes que la regla `end` de cada etiqueta EJS y los coloreaba erróneamente en rojo.

## [v1.3.0] - 2026-10-26

### Added
- Detección visual extendida de errores sintácticos y semánticos en todas las etiquetas EJS (resaltados en **Rojo Intenso Subrayado `#ff4757`**):
  - Doble signo de apertura por snippet mal expandido (`<<%`, `<<%=`, `<<%-`, `<<%#`).
  - Modificadores de apertura o cierre inexistentes (`<%==`, `<%--`, `<%##`, `<%=#`, `=%>`).
  - Etiquetas EJS vacías (`<% %>`, `<%= %>`, `<%- %>`).
  - Comentarios con cierre roto o anidado (`<%# ... <% ... %>`).
  - Estructuras de control (`if`, `else`, `for`, `while`, `switch`, `forEach`, `function`) dentro de etiquetas de salida `<%=` o `<%-`.
  - Uso de `<%= include(...) %>` en lugar de `<%- include(...) %>` (escaparía el HTML del partial).
  - Olvido del signo `=` al intentar imprimir una propiedad o variable (`<% pelicula.Genre %>`).
- Archivo de prueba e inspección visual `muestra-etiquetas.ejs` con catálogo de casos válidos e inválidos.

## [v1.2.0] - 2026-10-26

### Changed
- Diferenciación cromática clara entre etiquetas de salida y estructuras de control:
  - Etiquetas de **Salida** (`<%=` y `<%-`): apertura `<%` y cierre `%>` en **Verde Lima (`#a3e635`)**, con `=` en **Cian Brillante (`#00f5d4`)** y `-` en **Naranja Ámbar (`#fb923c`)**.
  - Etiquetas de **Control / Scriptlet** (`<% ... %>`): apertura `<%` y cierre `%>` en **Amarillo Eléctrico (`#ffea00`)**.
  - Símbolos de recorte de espacio (`_`, `-` en `<%_`, `_%>`, `-%>`) en **Cian Brillante (`#00f5d4`)**.
- Separación de la puntuación de apertura en dos capturas independientes (delimitador `<%` + modificador `=`/`-`/`_`) para un coloreado quirúrgico sin alterar el color de `%>`.

## [v1.1.0] - 2026-10-26

### Fixed
- Registro nativo del lenguaje `ejs` (`.ejs`) en `package.json` junto con `language-configuration.json`.
- Ampliación de `injectTo` a `["text.html.derivative", "text.html.basic"]` para garantizar compatibilidad en cualquier modo de archivo HTML/EJS.

## [v1.0.0] - 2026-10-26

### Added
- Gramática TextMate inicial para EJS con unificación de comentarios `<%# ... %>` bajo el scope estándar `comment.block.ejs` (mismo color que `<!-- HTML -->` y `// JS`).
- Resaltado de etiquetas EJS dentro de atributos HTML entrecomillados (`src="<%= pelicula.Poster %>"`).
- Colección completa de snippets EJS (`snippets/ejs.json`) para estructuras de control (`if`, `ifelse`, `foreach`, `for`, `switch`) y etiquetas de salida (`ejsout`, `ejsraw`, `ejsinc`, `ejscom`).

