# EJS Smart Colorizer (`fsolaje-tools.ejs-smart-colorizer`)

Extensión de coloreado de sintaxis y snippets para plantillas **EJS** en Visual Studio Code / Antigravity.

## Paleta y Semántica de Etiquetas EJS

| Etiqueta EJS | Propósito | Coloreado Aplicado |
| :--- | :--- | :--- |
| `<%# comentario %>` | Comentario de servidor (no se envía al cliente) | **Mismo color de comentario del tema** (idéntico a `<!-- HTML -->` y `// JS`), incluyendo `<%#` y `%>`. |
| `<% código %>` | Scriptlet de control JS (`if`, `forEach`, `switch`...) | **`<%` y `%>` en Verde Lima (`#a3e635`)** + código interior con colores nativos de JavaScript. |
| `<%= expresión %>` | Salida escapada HTML (segura frente a XSS) | **`<%` y `%>` en Verde Lima (`#a3e635`)** + signo **`=` en Cian Brillante (`#00f5d4`)**. |
| `<%- expresión %>` | Salida HTML cruda sin escapar / `include()` | **`<%` y `%>` en Verde Lima (`#a3e635`)** + signo **`-` en Naranja Ámbar (`#fb923c`)**. |
| `<%_ código _%>` | Scriptlet con recorte de espacios en blanco (*Whitespace slurp*) | **`<%` y `%>` en Verde Lima (`#a3e635`)** + signo **`_` en Amarillo (`#fde047`)**. |
| `<% código -%>` | Cierre con recorte de salto de línea (*Newline trim*) | **`-%>` con `-` en Amarillo (`#fde047`)** y `%>` en Verde Lima (`#a3e635`). |
| `<%%` y `%%>` | Etiquetas literales escapadas (imprimen `<%` o `%>` en pantalla) | **Violeta / Lavanda (`#c084fc`)**, igual que las secuencias de escape. |

## Ventajas frente a otras extensiones EJS
1. **Comentarios 100% homogéneos con HTML y JS:** A diferencia de *EJS Language Support* (que colorea `<%` como operador incluso dentro de `<%#`), esta gramática captura `<%# ... %>` completo como `comment.block.ejs`.
2. **Coloreado dentro de atributos HTML:** Resalta `<%= pelicula.Poster %>` incluso cuando va dentro de comillas de atributos HTML (`src="<%= pelicula.Poster %>"`).
3. **Configuración automática (`configurationDefaults`):** Al instalar el `.vsix` en cualquier VS Code, aplica automáticamente los colores y la asociación de archivos sin tener que copiar nada manualmente al `settings.json`.

