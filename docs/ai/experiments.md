# Experimentos con IA en programación

En este documento comparo resolver problemas con y sin IA,
midiendo tiempo, calidad del código y comprensión del problema.

## Experimento: Consultas al proyecto con MCP en Cursor

Para este experimento usé el servidor MCP filesystem conectado
a Cursor, que permite a la IA leer directamente los archivos
del proyecto sin necesidad de copiar y pegar código.

### Consulta 1: Listar archivos JavaScript
**Prompt:** "Lista todos los archivos JavaScript del proyecto"
**Respuesta:** Cursor encontró js/app.js, js/script.js y tailwind.config.js
**Conclusión:** Sin MCP habría tenido que buscarlos manualmente.

### Consulta 2: Contar funciones en app.js
**Prompt:** "Lee el archivo app.js y dime cuántas funciones tiene"
**Respuesta:** Detectó 5 funciones principales nombradas más
una función interna guardarEdicion() y varios callbacks anónimos.
**Conclusión:** Útil para hacer un inventario rápido del código.

### Consulta 3: Archivos en docs/ai
**Prompt:** "¿Qué archivos hay dentro de la carpeta docs/ai?"
**Respuesta:** Listó los 5 archivos markdown correctamente.
**Conclusión:** MCP tiene acceso completo a la estructura del proyecto.

### Consulta 4: Elementos del formulario en index.html
**Prompt:** "Lee el index.html y dime qué elementos del formulario tiene"
**Respuesta:** Describió con detalle todos los inputs, select,
botones y sus atributos exactos.
**Conclusión:** Muy útil para auditar el HTML sin abrirlo.

### Consulta 5: Qué hace styles.css
**Prompt:** "¿Qué hace el archivo styles.css?"
**Respuesta:** Explicó variables CSS, layout, estilos de tarjetas,
modo oscuro y responsive de forma muy completa.
**Conclusión:** MCP permite a la IA analizar archivos enteros
en segundos, algo imposible sin esta conexión.

## Conclusión general sobre MCP
MCP es útil en proyectos reales porque permite a la IA tener
contexto completo del proyecto sin necesidad de copiar código
manualmente. Es especialmente útil para auditorías, revisiones
de código y documentación automática.
