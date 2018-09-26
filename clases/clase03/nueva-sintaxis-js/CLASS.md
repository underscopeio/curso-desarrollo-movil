### Clases

Este concepto de la programación orientada a objetos (OOP) se introdujo en la nueva sintaxis de JS.
Las clases permiten definir propiedades y métodos, y luego generar múltiples instancias de esa clase. Es una manera más ordenada de _"reusar código"_ (en JavaScript ya existía el `prototype`, pero las clases dan mayor legibilidad).
Uno de las características más importantes de las clases, es que permite definir una clase a partir de otra ya existente _heredando_ sus propiedades y métodos.

#### En código

Supongamos que tenemos el siguiente código (sin clases)

```javascript
const unPajaro = {
  patas: 2,
  contarPatas() {
    console.log(`Tengo ${this.patas} patas`)
  },
}

const unGato = {
  patas: 4,
  contarPatas() {
    console.log(`Tengo ${this.patas} patas`)
  },
}

// Si quiero otro gato, debo volver a re-escribir código que querría que fuese igual
const otroGato = {
  patas: 4,
  contarPatas() {
    console.log(`Tengo ${this.patas} patas`)
  },
}

unPajaro.contarPatas() // -> Tengo 2 patas
unGato.contarPatas() // -> Tengo 4 patas
otroGato.contarPatas() // -> Tengo 4 patas
```

Con clases podemos agrupar este comportamiento (propiedades y métodos) en una clase.

```javascript
// Definimos una clase Animal
class Animal {
  constructor(numeroDePatas) {
    this.patas = numeroDePatas
  }

  contarPatas() {
    console.log(`Tengo ${this.patas} patas`)
  }
}

// Puedo crear un nuevo Animal
const unPajaro = new Animal(2)
const unGato = new Animal(4)
const otroGato = new Animal(4)

unPajaro.contarPatas() // -> Tengo 2 patas
unGato.contarPatas() // -> Tengo 4 patas
otroGato.contarPatas() // -> Tengo 4 patas

// Luego puedo definir una nueva clase Perro que extiende de Animal
class Perro extends Animal {
  constructor() {
    super(4)
    // super() llama al constructor de la clase que se está extendiendo,
    // En este caso lo llamamos con un número de patas fijo (4) porque todos los perros tiene 4 patas
  }

  // Puedo _redefinir_ un método, e incluso llamar al método de la clase padre usando `super.elMetodo()`
  contarPatas() {
    console.log(`Guau!!`)
    super.contarPatas()
  }
}

const unPerrito = new Perro()
const otroPerrito = new Perro()
unPerrito.contarPatas() // -> Guau! Tengo 4 patas
otroPerrito.contarPatas() // -> Guau! Tengo 4 patas
```

#### ¿Y cuándo lo uso?

Cada vez que creamos un componente propio con React / React Native y extendemos de la clase `Component`, estamos usando clases.
Deberías considerar crear una clase cada vez que uses algo repetítivamente en tu código, o que descubras cosas que sigan un mismo patrón.

```javascript
class MiComponente extends React.Component {
  render() {
    return <View />
  }
}
```
