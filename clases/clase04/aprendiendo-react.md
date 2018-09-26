# Clase 4

## Aprendiendo React

### JSX

JSX es una extensión a la sintaxis de JavaScript. Sirve para definir elementos de React de manera más declarativa.
Para convencerte, la siguiente expresión usando JSX

```javascript
const saludo = <h1 className="saludo">Hola!</h1>
```

Babel lo traduce a

```javascript
const element = React.createElement('h1', { className: 'saludo' }, 'Hola!')
```

Si todavía no te convence deberías ver componentes anidados.

### Componentes

React nos permite dividir la UI de nuestra app en piezas independientes y resusables, llamadas **componentes**.
Es el concepto más fuerte de React: definir **componentes de UI** de manera encapsulada, haciendo foco sólo en lo que ese componente debería resolver.
Además, reusar componentes es muy sencillo.
Cómo su nombre lo indica, un **componente** se puede _componer_: es decir, puede _usar_ y también _ser usado_ por otros componentes.

Haciendo una analogía con el mundo real, una **Mesa** se puede pensar como una **Tabla** con **Patas**. En React tendríamos un componente para `<Mesa>` que use los componentes `<Tabla>` una vez y `<Pata>` tres o más veces, depende de la mesa.

##### Ejemplo real con la app inicial de React Native

- Ver `App` como ejemplo
- Extiende de `Component`
- Explicar _render_
  > Es lo mínimo que necesitamos definir
  > Es la representación en vistas de nuestro componente
  > Se llama muchas veces, no sólo una

#### Componentización

- Armar un componente `<Saludo>` mostrando como puede reusarse múltiples veces

#### Props

En React los componentes pueden tener `props` que luego son usadas por el componente para definir su UI y/o comportamiento.
Según la documentación oficial de React:

> Conceptually, components are like JavaScript functions. They accept arbitrary inputs (called “props”) and return React elements describing what should appear on the screen.
> Conceptualmente, los componentes son como funciones de JavaScript. Reciben parámetros arbitrarios (llamados "props") y devuelven elementos de React que describen qué debería verse en pantalla.

- Agregar una prop `nombre` al componente `<Saludo>`
- Explicar cómo embeber _expresiones_ en JSX usando `{}` para mostrar el nombre

```javascript
class Saludo extends Component {
  render() {
    return <Text style={styles.saludo}>Hola {this.props.nombre}!</Text>
  }
}
```

- En el `render` de la app usar muchos componentes `<Saludo>` con distintos nombres

```javascript
export default class App extends Component {
  render() {
    return (
      <View style={styles.container}>
        <Saludo nombre="Juan" />
        <Saludo nombre="Romina" />
        <Saludo />
      </View>
    )
  }
}
```

- Mover el componente `<Saludo>` a un nuevo archivo `/componentes/Saludo.js`
- Mostrar como hacer el `export default` y el `import` desde `App.js`
- Agregar las dependencias necesarias y el `Stylesheet`

#### State

Para ilustrar el funcionamiento del `state` del componente vamos a usar el ejemplo de un reloj que queremos que se actualice en cada segundo. Primero vamos a intentar hacerlo usando `props` y luego compararlos.

- Creamos un nuevo componente `<Reloj>` en `/components/Reloj.js` que tome la hora que debe mostrar desde una prop `hora`

```javascript
import React, { Component } from 'react'
import { StyleSheet, Text } from 'react-native'

export default class Reloj extends Component {
  render() {
    return <Text style={styles.texto}>Son las {this.props.hora}</Text>
  }
}

const styles = StyleSheet.create({
  texto: {
    fontSize: 32,
    color: 'violet',
  },
})
```

- Desde `App.js` lo importamos, lo agregamos al render y le pasamos `new Date().toLocaleTimeString()`
- Pero ¿de qué sirve tener un reloj al que le tengo que decir que hora es? Debería ser al revés!
- Agregar un `constructor` a `<Reloj>`, explicando qué es y por qué debo llamar a `super()` antes que nada
- Setear el estado inicial con la `hora` y usar ese valor en el render. Luego borrar la prop ya innecesaria en `App.js`

  > Notar que el reloj se queda en una hora fija! Necesitamos decirle que se recalcule en cada segundo

- Probar con un `setInterval` fuera del componente y ver que no podemos acceder/modificar el estado
- Explicar qué es el _lifecycle_ de los componentes de React, en particular el `componentDidMount` y `componentWillUnmount`

  > Los componentes se montan/desmontan a medida que hay cambios en la _estructura_ de componentes y hay que asegurarse de _poner la mesa antes de comer_ así cómo de _dejar todo limpio antes de irnos_.

- Implementar el `componentDidMount` para setear un intervalo (mostrando solamente un `console.warn`) y `componentWillUnmount` para limpiar ese intervalo
- Intentar mutar el `state`
  > No funciona! El estado **NO SE DEBE MUTAR**. Hay que usar `setState` para poder cambiarlo.
- Explicar `setState` mostrando cómo funciona: toma un objeto lo _mergea_ con el estado anterior (\*)

### Resumen

#### Lifecycle de un componente de React

El _ciclo de vida_ de un componente de React puede resumirse en los siguientes pasos. (\*)

> Podemos agregar `console.warn` a cada _hook_ y comprobar el orden en que se llaman

1.  Se llama a `constructor`
1.  Se llama a `render` por primera vez
1.  Se llama a `componentDidMount`
1.  Luego puede volver a llamar a `render` debido a dos razones (\*)
    - El padre del componente se _re-renderea_
    - Se llama al `setState` del componente
1.  Se llama a `componentWillUnmount` **antes** de que el componente se desmonte

- Para poder ver el `componentWillUnmount` en acción, agregar un `<Button>` en `App.js` que haga un toggle y oculte/muestre el `<Reloj>`

#### Props vs State

Es importante resaltar cómo React separa explicítamente las propiedades _internas_ (`state`) de un componente con lo que podemos modificar del mismo al usarlo (`props`).
De hecho las `props` son de sólo lectura, es decir, **NO deben modificarse desde el componente que las recibe** y asimismo el `state` **NO debe modificarse desde afuera**.
Esta restricción, que en principio parece una desventaja, es en realidad una de las cosas que hacen fuerte a React. Es el mismo componente el que decide qué cosas permite cambiar desde afuera y cuáles las maneja internamente.

Haciendo una analogía con el mundo real: en un automóvil uno puede elegir el color (que sería una de las `props`) pero nó cómo funciona mecánicamente (que sería parte del `state`).
