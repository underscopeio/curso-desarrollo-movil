## Challenge

Transformar código que usa la sintaxis tradicional de JS en la nueva

### Instrucciones

1. Clonar este repositorio
1. Debajo de cada _snippet_ escribir cómo sería aplicando la nueva sintaxis de JS
1. Crea un Pull Request en Github con el archivo modificado
1. Compartí el link del Pull Request con el profesor

```js
var React = require('react')
var Component = React.Component
```

```js
// El valor de PI nunca debería cambiar
var PI = 3.141592

var acumulador = 0
if (true) {
  acumulador = acumulador + 10
}
```

```js
function sumar(a, b) {
  return a + b
}
```

```js
function sumar(a, b) {
  a = a === undefined ? 1 : a
  b = b === undefined ? 2 : b
  return a + b
}
```

```js
function procrear(nombre, edad) {
  return {
    nombre: nombre,
    edad: edad,
  }
}
```

TODO: agregar la sintaxis () => ({ blabla }) con parentesis para devolver objeto

```js
var hijo = {
  nombre: 'Juan',
  edad: 30,
  padre: {
    nombre: 'Pedro',
    edad: 90,
  },
}

var nombre = hijo.nombre
var edad = hijo.padre.edad
```

```js
var nombre = 'Juan'
var apellido = 'Perez'
var edad = 40

// Notar como se mezclan el operador + de strings con el + de números cuando hacemos (50 - edad)
console.log('El señor' + nombre + ' ' + apellido + ' va a cumplir 50 dentro de ' + (50 - edad) + ' años')
```

```js
function resultadoRandom(callback) {
  if (Math.random() > 0.5) {
    callback(new Error('Mala suerte'))
  } else {
    callback(null, 'Buena suerte')
  }
}

resultadoRandom(function(error, resultado) {
  if (error) {
    console.error(error)
  } else {
    console.log('Resultado: ', resultado)
  }
})
```
