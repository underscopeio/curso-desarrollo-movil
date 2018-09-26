### Definición de objetos

En la nueva versión de JavaScript definir propiedades y funciones en objetos es mucho más fácil.

#### En código

Definir propiedades en base a una variable **manteniendo el nombre**

```javascript
const nombre = 'Lionel'

// En vez de
const persona = { nombre: nombre }
// Se puede
const persona = { nombre }
```

Definir funciones

```javascript
// En vez de
const perro = {
  ladrar: function() {
    console.log('Guau')
  },
}
// Se puede
const perro = {
  ladrar() {
    console.log('Guau')
  },
}
```

Definir nombres de propiedades _dinámicamente_ (es decir, en tiempo de ejecución)

```javascript
const clave = esPerro ? 'patas' : 'piernas'
const valor = esPerro ? 4 : 2

const tom = {
  [clave]: valor,
}
```

#### ¿Y cuándo lo uso?

En React se usa mucho para setear el estado de un componente (por ejemplo, al _handlear_ un evento).

```javascript
class MiComponente extends Component {
  handleTextChange(texto) {
    this.setState({ texto })
  }
}
```
