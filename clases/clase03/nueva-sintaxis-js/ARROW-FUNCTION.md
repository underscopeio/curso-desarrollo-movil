### Arrow Function

La _arrow function_ es quizas una de las funcionalidades más útiles. Gracias a ellas podemos definir funciones de una manera mucho más _cómoda_:

- gracias a la nueva sintaxis podemos ahorrarnos las palabras clave `function` y `return`
- al compartir el contexto de quien la define, resuelve de manera más corta y simple la mayoría de los casos

Las _arrow function_ se definen con `() =>` (de ahí el nombre de _flecha_). Veamos la nueva sintaxis en más detalle con ejemplos en código.

#### En código

Pongamos como ejemplo la función `saludar`

```javascript
function saludar() {
  console.log('Hola')
}
// Ahora se puede escribir como
const saludar = () => {
  console.log('Hola')
}
```

Se vuelve más cómodo aún para funciones que devuelven algo (es decir, que usan `return`)

```javascript
function sumar(x, y) {
  return x + y
}
// Ahora se puede escribir como
const sumar = (x, y) => x + y
```

Todavía mejor para definir funciones en la misma línea! Muy útil al hacer loops.

```javascript
const numeros = [1, 5, 2]

const dobles = numeros.map(function(n) {
  return n * 2
})
// Nos ahorramos dos líneas si usamos una _arrow function_
const dobles = numeros.map(n => n * 2)
```

Y podemos usar el contexto del padre sin problemas

```javascript
function filtrarPalabras() {
  this.palabras = ['al', 'de', 'larga', 'extensa']
  this.palabrasLargas = []

  this.palabras.forEach(function(palabra) {
    if (palabra.length > 4) {
      this.palabrasLargas.push(palabra)
    }
  })

  return this.palabrasLargas
}
```

#### ¿Y cuándo lo uso?

En todos lados: cada vez que hagas un _forEach_ o un _map_, al definir cualquier función en la misma línea y cuando quieras usar el contexto _del padre_ de la función.
En React/React Native es muy útil para definir _handlers_ de eventos, donde quiero usar el `this` del componente (para setear el _state_ por ejemplo).

```javascript
class MiComponente extends Component {
  // NO funciona
  handleClick() {
    this.setState({ hizoClick: true })
    // `this` NO hace referencia al contexto de `MiComponente` porque es una función tradicional
  }

  // Funciona
  handleClick = () => {
    this.setState({ hizoClick: true })
    // `this` es el mismo que el de `MiComponente` pues allí se definió esta _arrow function_
  }

  render() {
    return <Botón onClick={this.handleClick} />
  }
}
```
