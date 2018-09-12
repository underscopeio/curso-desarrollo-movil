### Promises

Las _Promises_ simplifican la programación asincrónica.
En JavaScript existía (existe) un concepto llamado _callback hell_, donde llamadas asincrónicas anidadas generan un código muy difícil de entender. Con las _Promises_ este problema puede resolverse de una manera más _elegante_.

Una `Promise` representa un valor que va a estar disponible en el futuro. Además, considera el caso en que _algo falle_ y nos permite manejar el error apropiadamente.

Debajo podemos ver ejemplos de cómo usarlo.

#### En código

Tradicionalmente cuando una función tardaba un tiempo indeterminado se resolvía pasándo un último parámetro llamado `callback` (_llamada de retorno_): una función que sería llamada en cuanto el resultado estuviese disponible.
Por convención, esa función espera como primer parámetro un `error`, que si es `null` indica que la función fue

Veamos un ejemplo

```javascript
function esperarDosSegundos(callback) {
  // Supongamos que esta función puede fallar de manera aleatoria
  if (Math.random() > 0.9) {
    callback(new Error('Mala suerte'))
    return
  }

  setTimeout(function() {
    // Llamo a callback con null, para indicar que NO hay error
    callback(null)
  }, 2000)
}

function esperarSeisSegundos(callback) {
  esperarDosSegundos(function(error) {
    if (error) {
      return callback(new Error('Fallo en la primera'))
    }

    esperarDosSegundos(function(error) {
      if (error) {
        return callback(new Error('Fallo en la segunda'))
      }

      esperarDosSegundos(function(error) {
        if (error) {
          return callback(new Error('Fallo en la tercera'))
        }

        callback(null, 'Llegó!!')
      })
    })
  })
}

esperarSeisSegundos(function(error, resultado) {
  if (error) {
    console.log('Error', error)
  } else {
    console.log('Éxito', resultado)
  }
})
```

Con _Promises_ esto puede hacerse de manera más _prolija y ordenada_, manejando por separado el caso de error del caso exitoso.
Además permite _agrupar_ el manejo de errores en un sólo lugar, en caso de que eso querramos.

```javascript
// No hace falta que reciba un `callback` ya que devolverá una `Promise`
function esperarDosSegundos() {
  // Al crear una `Promise` vamos a tener que indicar cuándo la misma fue:
  // - exitosa, en ese caso debemos llamar a `resolve` con el resultado
  // - fallida, en cuyo caso debemos llamar a `reject` con el error
  return new Promise(function(resolve, reject) {
    if (Math.random() > 0.9) {
      return reject(new Error('Mala suerte'))
    }

    setTimeout(function() {
      resolve()
    }, 2000)
  })
}

function esperarSeisSegundos() {
  // Al llamar a una función que devuelve una `Promise`, podremos manejar:
  // - el caso exitoso (usando `.then`)
  // - el caso fallido (usando `.catch`)
  esperarDosSegundos()
    .then(function() {
      return esperarDosSegundos()
    })
    .then(function() {
      return esperarDosSegundos()
    })
    .then(function() {
      return esperarDosSegundos()
    })
}

esperarSeisSegundos()
  .then(function(resultado) {
    console.log('Éxito', resultado)
  })
  .catch(function(error) {
    console.log('Error', error)
  })
```

En combinación con _arrow functions_ el código puede reducirse notablemente

```javascript
function esperarDosSegundos() {
  return new Promise(function(resolve, reject) {
    if (Math.random() > 0.9) {
      return reject(new Error('Mala suerte'))
    }

    setTimeout(resolve, 2000)
  })
}

function esperarSeisSegundos() {
  esperarDosSegundos()
    .then(() => esperarDosSegundos())
    .then(() => esperarDosSegundos())
}

esperarSeisSegundos()
  .then(resultado => console.log('Éxito', resultado))
  .catch(error => console.log('Error', error))
```

#### ¿Y cuándo lo uso?

Javascript es un lenguaje asincrónico, por lo que las llamadas asincrónicas son muy comunes y vas a usarlas todo el tiempo.
Por ejemplo, para obtener un JSON de _la web_ puedo usar `fetch` que devuelve una promise, luego parsear el JSON a Javascript Object y por último quedarme con un campo en particular. Este es un ejemplo que veremos con más detalle durante el curso.

```javascript
fetch('https://jsonplaceholder.typicode.com/posts/1')
  .then(respuesta => respuesta.json())
  .then(articulo => articulo.title)
  .then(titulo => console.log('El artículo se titula: ' + titulo))
  .catch(error => console.log('Algo falló', error))
```
