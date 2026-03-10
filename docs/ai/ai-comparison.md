## Prueba 1: Explicar un closure

### Prompt usado
"Explícame qué es un closure en JavaScript con un ejemplo práctico"

### Respuesta de ChatGPT
Un closure (clausura) en JavaScript es un mecanismo del lenguaje por el cual una función “recuerda” las variables de su entorno léxico (scope) incluso después de que la función externa haya terminado de ejecutarse.

Esto ocurre porque en JavaScript las funciones son objetos de primera clase y mantienen una referencia al scope donde fueron creadas, no al lugar donde se ejecutan.

En términos técnicos:

Un closure es la combinación de una función + el entorno léxico en el que fue declarada.

Este comportamiento está definido en la especificación de JavaScript (ECMAScript) y documentado por fuentes oficiales como Mozilla Developer Network (MDN).

1. Ejemplo básico de Closure
function crearContador() {
  let contador = 0;

  return function () {
    contador++;
    return contador;
  };
}

const contar = crearContador();

console.log(contar()); // 1
console.log(contar()); // 2
console.log(contar()); // 3
Qué está pasando paso a paso

Se ejecuta crearContador().

Dentro se crea la variable contador = 0.

La función devuelve otra función interna.

Esa función interna tiene acceso a contador porque fue creada dentro de ese scope.

Aunque crearContador() ya terminó, contador sigue existiendo dentro del closure.

Resultado:

1
2
3

La variable no se reinicia porque vive dentro del closure.

### Respuesta de Claude
Un closure es una función que "recuerda" las variables del contexto donde fue creada, incluso después de que ese contexto haya terminado de ejecutarse.
Dicho de forma simple: una función que lleva consigo la mochila de variables de donde nació.

Ejemplo práctico:
jsfunction crearContador() {
    let contador = 0; // Esta variable vive dentro de crearContador

    return function() {
        contador++; // La función interna "recuerda" contador
        console.log(contador);
    };
}

const miContador = crearContador();
miContador(); // 1
miContador(); // 2
miContador(); // 3
¿Qué está pasando aquí?

crearContador se ejecuta y crea la variable contador
Devuelve una función interna que usa contador
Aunque crearContador ya terminó, la función interna sigue teniendo acceso a contador
Cada vez que llamas a miContador() la variable se actualiza

¿Para qué sirve en la vida real?
En tu proyecto TaskFlow lo usas sin darte cuenta. Cuando haces:
jsarticle.querySelector('.btn-eliminar').addEventListener('click', function() {
    tareas = tareas.filter(t => t.id !== tarea.id);
});
Esa función del click recuerda tarea gracias a un closure.

### Conclusión
Claude me da la sensación que es mas veridica la información.


## Prueba 2: Detectar un bug
### Prompt usado
Encuentra el error en este código JavaScript y explícame por qué falla
### Respuesta de ChatGPT
El código tiene un error lógico (no de sintaxis). La función se llama sumar, pero realmente está restando.

Código original
function sumar(a, b) {
    return a - b;
}
console.log(sumar(3, 2));
Resultado que produce
1

Porque JavaScript calcula:

3 - 2 = 1

Pero si la función realmente sumara, el resultado esperado sería:

3 + 2 = 5
Por qué falla

El problema está en esta línea:

return a - b;

El operador - es el operador de resta en JavaScript.

Según la especificación de ECMAScript, los operadores aritméticos funcionan así:

Operador	Operación
+	suma
-	resta
*	multiplicación
/	división

En el código se usa el operador incorrecto para la intención de la función.

Código corregido
function sumar(a, b) {
    return a + b;
}

console.log(sumar(3, 2));
Resultado correcto
5
Cómo detectar este tipo de error (muy típico)

Este tipo de bug se llama error semántico o lógico:

El código no genera error en ejecución

Funciona técnicamente

Pero no hace lo que el nombre o la lógica prometen

Para detectarlo:

Revisar que el nombre de la función coincida con la operación.

Usar tests simples:

console.assert(sumar(3,2) === 5);

Si falla, sabes que hay un problema lógico.

✅ Conclusión

El código falla porque:

La función sumar usa el operador - (resta).

Debería usar + (suma).
### Respuesta de Claude
Bug detectado
El error está en la línea 2. La función se llama sumar pero usa el operador - en vez de +:
js// ❌ Incorrecto
return a - b;

// ✅ Correcto
return a + b;
sumar(3, 2) devuelve 1 en vez de 5 porque está restando en lugar de sumar. Es un error semántico, el código funciona sin errores pero hace algo diferente a lo que su nombre indica.
### Conclusión
Claude esta mejor preparada para codigo que chat gpt y creo que el analisis es mas preciso a la hora de dar una line para modificar.
## Prueba 3: Generar Código desde descripción
### Prompt usado
Crea una función JavaScript que reciba un array de tareas y devuelva solo las que están completadas"
### Respuesta de ChatGPT
Para resolverlo correctamente, necesitamos filtrar un array y devolver solo los elementos que tengan la propiedad completada en true.
La forma más idiomática en JavaScript moderno es usar el método Array.prototype.filter(), documentado por Mozilla Developer Network.

1. Ejemplo de estructura del array de tareas

Supongamos que las tareas tienen esta forma:

const tareas = [
  { id: 1, titulo: "Estudiar JavaScript", completada: true },
  { id: 2, titulo: "Hacer ejercicio", completada: false },
  { id: 3, titulo: "Terminar proyecto DAW", completada: true }
];
2. Función para obtener solo las tareas completadas
function obtenerTareasCompletadas(tareas) {
  return tareas.filter(tarea => tarea.completada === true);
}

Uso:

const completadas = obtenerTareasCompletadas(tareas);
console.log(completadas);

Resultado:

[
  { id: 1, titulo: "Estudiar JavaScript", completada: true },
  { id: 3, titulo: "Terminar proyecto DAW", completada: true }
]
3. Qué hace exactamente filter()

filter() recorre todo el array y:

Ejecuta una función para cada elemento.

Si la función devuelve true, el elemento se mantiene.

Si devuelve false, el elemento se descarta.

Flujo conceptual:

Array original
   ↓
filter()
   ↓
solo elementos que cumplen la condición
4. Versión más corta (muy usada en producción)
const obtenerTareasCompletadas = tareas =>
  tareas.filter(tarea => tarea.completada);

Esto funciona porque en JavaScript true ya es una condición válida.

5. Versión robusta (buena práctica profesional)

Para evitar errores si llega algo que no es un array:

function obtenerTareasCompletadas(tareas) {
  if (!Array.isArray(tareas)) {
    throw new Error("El parámetro debe ser un array");
  }

  return tareas.filter(tarea => tarea.completada === true);
}
6. Ejemplo completo ejecutable
const tareas = [
  { id: 1, titulo: "Estudiar JavaScript", completada: true },
  { id: 2, titulo: "Hacer ejercicio", completada: false },
  { id: 3, titulo: "Terminar proyecto DAW", completada: true }
];

function obtenerTareasCompletadas(tareas) {
  return tareas.filter(tarea => tarea.completada);
}

console.log(obtenerTareasCompletadas(tareas));

✅ Resumen

La función:

recibe un array

usa filter()

devuelve solo los objetos donde completada === true
### Respuesta de Claude
function obtenerTareasCompletadas(tareas) {
    return tareas.filter(function(tarea) {
        return tarea.completada === true;
    });
}

// Ejemplo de uso:
const tareas = [
    { id: 1, texto: 'Comprar leche', completada: true },
    { id: 2, texto: 'Estudiar JS', completada: false },
    { id: 3, texto: 'Hacer ejercicio', completada: true }
];

console.log(obtenerTareasCompletadas(tareas));
// Devuelve: las tareas con id 1 y 3. Filter recorre el array y solo se queda con los elementos donde la condición es true, en este caso donde completada es true.
## Conclusión general

Después de comparar ChatGPT y Claude en tres pruebas distintas, ambos
asistentes son útiles pero tienen matices diferentes. ChatGPT tiende a
dar respuestas más largas y detalladas, mientras que Claude es más directo
y conciso. Para detectar bugs y explicar conceptos técnicos me ha resultado
más claro Claude, ya que va al grano sin rodeos. ChatGPT en cambio genera
más ejemplos alternativos lo cual puede ser útil cuando estás aprendiendo
algo nuevo. En general usaré Claude para tareas concretas de código y
ChatGPT cuando necesite explorar un tema desde cero.