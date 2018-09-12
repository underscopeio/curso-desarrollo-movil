### Parámetros predeterminados

Los _default parameters_ permiten definir valores predeterminados para los parámetros de una función.

#### En código

Es útil para parámetros que son opcionales

```javascript
function saludar(quien = 'mundo') {
  console.log('Hola ' + quien)
}

saludar('Rosa') // -> Hola Rosa
saludar() // -> Hola mundo
```

Y también para evitar chequear si un parámetro es `undefined`, sobre todo para _arrays_, objetos y _strings_.
En los siguientes casos obtendríamos una `Exception` si no

```javascript
// Para arrays
function sumarTodos(numeros = []) {
  let suma = 0
  numeros.forEach(function(numero) {
    suma += numero
  })
  return suma
}

console.log(sumarTodos()) // -> 0

// Para objetos
function saludar(persona = { nombre: 'Mengano' }) {
  console.log('Hola ' + persona.nombre)
}

console.log(saludar()) // -> 'Hola Mengano'

// Para strings
function separarPorEspacios(texto = '') {
  return texto.split(' ')
}

console.log(separarPorEspacios()) // -> []
```

#### ¿Y cuándo lo uso?

Es una buena práctica definir parámetros predeterminados (siempre que tenga sentido) para evitar valores `undefined` y hacer nuestro código menos propenso a errores, como se vió en los ejemplos anteriores.
