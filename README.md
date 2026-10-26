# EJS Smart Colorizer (`fsolaje-tools.ejs-smart-colorizer`)

> **Versión de Entrega:** `v1.5.0`

Extensión avanzada de coloreado de sintaxis, detección visual de errores y colección de snippets para plantillas **EJS** en Visual Studio Code / Antigravity.

## Paleta y Semántica de Etiquetas EJS (`v1.5.0`)

| Etiqueta / Caso EJS | Propósito | Coloreado Aplicado |
| :--- | :--- | :--- |
| `<%= expresión %>` | Salida escapada HTML (segura frente a XSS) | Apertura `<%` y cierre `%>` en **Verde Lima (`#a3e635`)** + signo **`=` en Cian Brillante (`#00f5d4`)**. |
| `<%- expresión %>` | Salida HTML cruda sin escapar / `include()` | Apertura `<%` y cierre `%>` en **Verde Lima (`#a3e635`)** + signo **`-` en Naranja Ámbar (`#fb923c`)**. |
| `<% código %>` | Estructuras de control JS (`if`, `else`, `forEach`, `switch`...) | Apertura `<%` y cierre `%>` en **Amarillo Eléctrico (`#ffea00`)** + interior con colores nativos del tema de VS Code. |
| `<%_ ... _%>` / `-%>` | Recorte de espacios (*Whitespace slurp*) y salto de línea (*Newline trim*) | Delimitadores `<%` / `%>` según su tipo (Salida o Control) + modificadores **`_` y `-` en Cian Brillante (`#00f5d4`)**. |
| `<%# comentario %>` | Comentario de servidor (no se envía al cliente) | **Mismo color de comentario del tema activo** (idéntico a `<!-- HTML -->` y `// JS`), incluyendo `<%#` y `%>`. |
| `<%%` y `%%>` | Etiquetas literales escapadas (imprimen `<%` o `%>` en pantalla) | **Violeta / Lavanda (`#c084fc`)**, igual que las secuencias de escape. |
| **Errores de uso** (`<% pelicula.Genre %>`, `<%= if (...) %>`, `<%= include(...) %>`, `<%= %>`, `<<%`, `<%==`, `=%>`) | Detección visual inmediata de errores sintácticos o semánticos en EJS | **Rojo Intenso en Negrita y Subrayado (`#ff4757`)**. |

## Ventajas Principales

1. **Integración Nativa con el Tema de VS Code (`source.js`):** El código JavaScript interior conserva los scopes oficiales de VS Code (`support.variable.property.js` para `.length`, `variable.other.object.js` para objetos, `support.function.js` para `.forEach`/`.map`, `variable.parameter.js` para parámetros arrow) sin que llaves abiertas `{` en bloques `<% if (...) { %>` bloqueen el cierre `%>`.
2. **Detección Visual de Errores Frecuentes:** Alerta en tiempo real si olvidas el `=` al imprimir (`<% pelicula.Genre %>`), si pones un `if`/`forEach` dentro de `<%=`, si usas `<%= include(...) %>` en vez de `<%- include(...) %>`, o si dejas una etiqueta vacía o con doble apertura `<<%`.
3. **Comentarios 100% Homogéneos con HTML y JS:** Captura `<%# ... %>` completo como `comment.block.ejs`.
4. **Configuración Automática (`configurationDefaults`):** Al instalar el `.vsix` en cualquier VS Code, aplica automáticamente los colores y la asociación de archivos sin configuración manual.

## Regenerar el paquete `.vsix`

```bash
node pack-vsix.js
```
