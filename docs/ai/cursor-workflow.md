# Flujo de trabajo con Cursor

En este documento documento mi experiencia usando Cursor como IDE
asistido por IA, atajos de teclado y ejemplos de mejoras al código.

## Atajos de teclado más usados

- `Ctrl + K` — Edición inline: modificar o añadir código seleccionado
- `Ctrl + L` — Abrir chat contextual
- `Ctrl + Shift + I` — Composer para cambios en varios archivos

## Ejemplo 1: Añadir JSDoc con Ctrl+K

### Qué hice
Seleccioné la función renderizarTodas en app.js y usé Ctrl+K
para pedir que Cursor añadiera comentarios JSDoc.

### Resultado
Cursor generó automáticamente un bloque JSDoc completo con
descripción de la función y el parámetro @param listaDeTareas
indicando que es un Array de objetos con sus propiedades.

### Conclusión
El resultado fue muy útil, Cursor entendió perfectamente qué
hacía la función y generó documentación profesional en segundos.

## Ejemplo 2: Explicar código con el chat Ctrl+L

### Qué hice
Usé el chat de Cursor con Ctrl+L para pedir que explicara
qué hace la función crearElementoTarea.

### Resultado
Cursor analizó automáticamente los archivos del proyecto y
explicó paso a paso toda la función: la traducción de prioridad,
la creación del article, el HTML interno, los eventos de editar,
completar y eliminar.

### Conclusión
El chat contextual de Cursor es muy útil para entender código
que no has escrito tú o que llevas tiempo sin revisar.
Es como tener un compañero que conoce todo tu proyecto.