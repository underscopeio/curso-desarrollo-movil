### Object destructuring

Esta funcionalidad es muy útil para _extraer_ fácilmente propiedades de objetos y elementos de arrays.
Además permite definir valores predeterminados en el caso de que las propiedades no existan.

#### En código

```javascript
const persona = {
  nombre: 'Juan',
  apellido: 'Perez',
  edad: 32,
}

const { nombre, apellido } = persona

const [primero, segundo] = [1, 2, 3, 4, 5]

// Funciona incluso en objetos anidados
const empresa = {
  lugar: {
    direccion: 'Céspedes 3249',
  },
}

const {
  lugar: { direccion },
} = empresa
console.log(direccion) // -> Céspedes 3249

// También se puede renombrar la variable
const {
  lugar: { direccion: direccionEmpresa },
} = empresa
console.log(direccionEmpresa) // -> Céspedes 3249

// Y dar valores predeterminados, en caso de que no existan
const {
  lugar: { direccion = 'Calle falsa 123' },
  empleados = 1,
} = empresa
console.log(direccion) // (usa el valor real) -> Céspedes 3249
console.log(empleados) // (usa el valor predeterminado) -> 1
```

#### ¿Y cuándo lo uso?

Es **muy usado** en React para extraer información de las `props` y el `state` de un componente.

```javascript
class Saludo extends Component {
  state = {
    edad: 20,
  }

  render() {
    const { nombre } = this.props
    const { edad } = this.state

    return (
      <Text>
        Saluden a {nombre}, de {edad} años
      </Text>
    )
  }
}
```

También para descomponer los parámetros de una función

```javascript
const persona = { nombre: 'Pedro', edad: 28 }

// En vez de hacer lo siguiente
function saludar(persona) {
  console.log(`Saluden a ${persona.nombre}, de ${persona.edad} años`)
}

// Podemos...
function saludar({ nombre, edad }) {
  console.log(`Saluden a ${nombre}, de ${edad} años`)
}
```
