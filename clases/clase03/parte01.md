# Clase 3 - Parte 1

## Layout y Estilos en React Native

Los estilos en React Native tienen similitudes y diferencias con los estilos definidos por CSS en la web.
Por un lado, los nombres de las propiedades de estilo son en su mayoría compartidas con las de CSS.
Por otro, tenemos varias diferencias _estructurales_:

- **no se usa CSS** sino que cada componente define su estilo, es decir, no se aplican estilos _en cascada_.
- **los estilos se definen como objetos**, usando **camelCase** en vez de guiones medios para separar entre palabras. Por ejemplo, lo que en CSS sería `border-radius` en React Native es `borderRadius`.
- **la propiedad `style` puede ser un solo estilo o un array de estilos** y permite definir estilos condicionales fácilmente.
- es recomendable usar una clase utilitaria llamda **StyleSheet** para definir varios estilos ordenadamente.

### StyleSheet

**StyleSheet** es una clase utilitaria parte de React Native que permite agrupar varios estilos en una solo grupo de estilos.
Suele definirse debajo de la definición del componente y llamarse `styles`.

```javascript
import React, { Component } from 'react'
import { View } from 'react-native'

class MiComponente extends Component {
  render() {
    return <View style={styles.cuadradoAzul} />
  }
}

const styles = StyleSheet.create({
  cuadradoAzul: {
    backgroundColor: 'blue',
    width: 30,
    height: 30,
  },
})
```

### Múltiples estilos

La propiedad `style` de los componente de React Native acepta tanto estilos únicos (ya sean objetos o parte de un `StyleSheet`) como múltiples estilos tomando un array de estilos, combinando todos los estilos que son parte de ese array.
Es importante notar que **las propiedades de estilo se pisan**, quedando vigente la última aplicada.

```javascript
import React, { Component } from 'react'
import { View, Text, StyleSheet } from 'react-native'

class MiComponente extends Component {
  render() {
    return (
      <View>
        <Text style={styles.textoAzul}>Texto azul</Text>
        <Text style={[styles.textoAzul, styles.textoGrande]}>Texto grande y rojo</Text>
        <Text style={[styles.textoGrande, styles.textoAzul]}>Texto grande y azul</Text>
      </View>
    )
  }
}

const styles = StyleSheet.create({
  textoGrande: {
    color: 'red',
    fontSize: 24,
  },
  textoAzul: {
    color: 'blue',
  },
})
```

### Estilos condicionales

Muchas veces queremos que un componente tenga un estilo u otro en base a cierta condición. Esto es fácil de lograr usando un array de estilos sumado a condiciones de la siguiente manera.

```javascript
class MiBoton extends Component {
  render() {
    const deshabilitado = true // o false
    return <Button style={[styles.boton, deshabilitado && styles.deshabilitado]} />
  }
}

const styles = StyleSheet.create({
  boton: {
    fontSize: 20,
  },
  deshabilitado: {
    color: 'gray',
  },
})
```

También puede usarse el _operador ternario_ para definir un estilo si se da una condición y otro si no.

```javascript
import React, { Component } from 'react'
import { View, Text, StyleSheet } from 'react-native'

class MiTexto extends Component {
  render() {
    const respuestaCorrecta = Math.random() > 0.5

    return (
      <Text style={[styles.respuesta, respuestaCorrecta ? styles.correcta : styles.incorrecta]}>
        La respuesta es {respuestaCorrecta ? 'CORRECTA :)' : 'INCORRECTA :('}
      </Text>
    )
  }
}

const styles = StyleSheet.create({
  respuesta: {
    fontSize: 20,
  },
  correcta: {
    color: 'green',
  },
  incorrecta: {
    color: 'red',
  },
})
```

### Flexbox

> Basado en la guía de CSS Tricks (https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

Flexbox es un _sistema de layout_ que tiene como objetivo simplificar la disposición, el alineado y la distribución del espacio entre elementos dentro de un contenedor, incluso cuando no sabemos exactamente cuál es el tamaño de ellos.

La idea detrás del _diseño flexbox_ es darle al contenedor el poder de alterar el ancho y alto de sus _elementos hijos_ para ocupar el espacio disponible de la mejor manera (sobre todo para acomodarse a las distintas resoluciones).
Un _contenedor flex_ expande sus hijos para llenar el espacio o los achica para evitar que _se caigan_.

Además, el _diseño flexbox_ permite abstraernos de la dirección de un contenedor (es decir, si es vertical u horizontal).
En otras palabras, nos permite definir cómo van a comportarse los elementos sin importar su dirección.

Flexbox es especialmente útil para el diseño de aplicaciones móbiles, donde el espacio es acotado y las resoluciones pueden ser muy distintas entre un dispositivo y otro.
Es por React Native lo adopta como su _sistema de layout_ principal y recomendado.

#### Conceptos

Usando Flexbox hay que tener en cuenta que siempre hay dos _entidades_ involucradas: el **contenedor** (o padre) y los elementos **contenidos** (o hijos).
Generalmente para obtener el resultado esperado hace falta definir propiedades a ambos.

> Es importante resaltar que un _hijo_ puede al mismo tiempo ser _padre_ de otros. En ese caso, puede que definamos algunas propiedades que lo definen como _contenedor_ y otras como elemento _contenido_.

##### Propiedades del contenedor

Las propiedades que pueden definirse en un contenedor que más se usan son:

- **Dirección**: usando `flexDirection` definimos en qué dirección se ordenan los hijos.
  Los valores que puede tomar son:

  - `row` ordena los hijos en fila
  - `column` ordena los hijos en columna
  - `row-reverse` ordena los hijos en fila, pero invierte el orden de los mismos
  - `column-reverse` ordena los hijos en columna, pero invierte el orden de los mismos

- **Justificado**: usando `justifyContent` definimos cómo van a comportarse los hijos **sobre el eje de la dirección**. Es decir, si la dirección es `row` definimos cómo se comportan los hijos **eje horizontal** y si elegimos `column` en el **eje vertical**.
  Los valores que puede tomar son:

  - `flex-start`, que junta los hijos al principio del eje
  - `flex-end`, que junta los hijos al final del eje
  - `center`, que junta los hijos al centro del eje
  - `space-between`, que separa los hijos dejando **el mismo espacio entre cada uno, sin incluir los extremos**
  - `space-evenly`, que separa los hijos dejando **el mismo espacio entre cada uno, incluyendo los extremos**
  - `space-around`, que separa los hijos dejando **el mismo espacio entre cada uno y la mitad de ese espacio en los extremos**

- **Alineado**: usando `alignItems` definimos cómo van a comportarse los hijos **sobre el eje contrario a la dirección**. Es decir, si la dirección es `row` definimos cómo se comportan los hijos **eje vertical** y si elegimos `column` en el **eje horizontal**.
  Los valores que puede tomar son:

  - `flex-start`, que alinea los hijos al principio del eje
  - `flex-end`, que alinea los hijos al final del eje
  - `center`, que alinea los hijos al centro del eje
  - `baseline`, que alinea los hijos seteando una linea base (muy útil para textos)
  - `stretch`, trata de ocupar el mayor espacio posible

- **Wrap**: usando `flexWrap` definimos cómo deben comportarse en caso de que superen el tamaño del _viewport_.
  Los valores que puede tomar son:

  - `wrap`, que pasa los elementos que no entran a la siguiente fila/columna según corresponda
  - `no-wrap`, que deja los elementos en la misma fila/columna

##### Propiedades de los elementos contenidos

- **Flex**: usando la propiedad `flex` definimos al elemento cuánto espacio debe ocupar y funciona de la siguiente manera:

  - Si `flex` es un número positivo, hace que el componente sea **flexible** y que se ajuste en base a ese valor. Así, un componente que tenga `flex: 2` va a tomar el doble de espacio que uno que tenga `flex: 1`.
  - Si `flex` es `0`, el componente es **inflexible** y toma el tamaño definido en su `width` y `height`.
  - Si `flex` es `-1`, el componente usa el tamaño definido en su `width` y `height`, pero se achica hasta su `minWidth` y `minHeight` si no hay espacio suficiente.

- **Alineado**: usando `alignSelf` definimos cómo debe alinearse **este elemento específicamente**, pisando el valor de `alignItems` del padre. Puede tomar los mismos valores que `alignItems`:

  - `flex-start`, que alinea los hijos al principio del eje
  - `flex-end`, que alinea los hijos al final del eje
  - `center`, que alinea los hijos al centro del eje
  - `baseline`, que alinea los hijos seteando una linea base (muy útil para textos)
  - `stretch`, trata de ocupar el mayor espacio posible

#### Flexbox cheatsheet

Las propiedades (más usadas) que puede tener un _padre_ son

- `flexDirection` que puede ser `row` o `column` (default: `column`)
- `justifyContent` que puede ser `flex-start`, `center`, `flex-end`, `space-around`, `space-between` o `space-evenly` (default: `flex-start`)
- `alignItems` que puede ser `flex-start`, `center`, `flex-end` o `stretch` (default: `stretch`)

Las propiedades (más usadas) que puede tener un _hijo_ son

- `flex` que debe ser un número (puede ser positivo, `0` o `-1`)
- `alignSelf` que puede ser `flex-start`, `center`, `flex-end` o `stretch`

#### Consejos

Algunos consejos a la hora de crear _layouts_

- Antes que nada, pensar que elementos tendría y como debería comportarse cada uno
- Identificar los elementos que tienen tamaño fijo y cuáles son variables. Esos variables probablemente tengan que ser `flex`.
- Durante el proceso usar colores de background para cada elemento. Esto ayuda a distinguir cuanto espacio toma cada uno.
- Primero definir los estilos _inline_ para que nuestro editor (al menos si usamos VSCode) nos autocomplete las posibles propiedades y valores que puede tomar. Una vez que lo tenemos listo, moverlo a un `StyleSheet`.
- No confundir las propiedades de Flexbox que corresponden al _padre_ con las del _hijo_.
- Tampoco olvidar que un componente puede ser **padre e hijo al mismo tiempo**, por lo que podría tener propiedades de ambos. (Por ejemplo, `flexbox: 1` como hijo y `justifyContent: 'center'` como padre).

#### Ejercicios

Es recomendable usar como referencia la guía interactiva de React Native (https://facebook.github.io/react-native/docs/flexbox) ya que es exactamente como se usa en RN.

A pesar de usar la sintaxis de CSS puede resultar muy útil hacer los ejercicios de Flexbox Froggy (https://flexboxfroggy.com/) para familiarizarse con los conceptos de `justify`, `align`, `direction`, etc. de manera entretenida.
