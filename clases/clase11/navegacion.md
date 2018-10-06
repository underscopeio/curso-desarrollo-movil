# Clase 11

## Navegación

La navegación es una de las partes más importantes de una aplicación. Es fundamental definir una buena navegación, caso contrario la aplicación puede volverse difícil de usar, y hacernos perder muchos usuarios (o al menos, hacerlos menos felices).

En especial en las aplicaciones móviles, tener una navegación fácil de entender y de usar es clave, sobre todo teniendo en cuenta que al contar con una pantalla más pequeña es muy probable que tengamos múltiples pantallas, al menos más que en cualquier aplicación web.

### Navegación en React Native

Al desarrollar en nativo la navegación suele ya estar resuelta (al menos en gran parte) por la misma plataforma: tanto Android como iOS proveen a los desarrolladores soluciones _nativas_.
La cosa no está tan fácil para React Native, que al querer unificar el desarrollo para ambas plataformas, se encuentra con nuevos problemas. Por un lado, unificar ambas plataformas se vuelve muy difícil siendo que muchas veces tienen funcionalidades muy distintas. Además, se suman complejidades técnicas dado que React Native es quien maneja las vistas.

Por esta razón es que React Native no incluye una solución dentro de su core. Esto da lugar a _libraries_ que buscan resolver este problema, enfrentando desafíos de alta complejidad.
Hoy en día las dos opciones más importantes dentro de la comunidad son `react-navigation` y `react-native-navigation`.

### Comparación entre `react-navigation` y `react-native-navigation`

Ambas buscan resolver el problema de navegación _cross-platform_, es decir, compartiendo una misma interfaz, al menos en gran parte. Sin embargo, el enfoque que tienen es distinto: `react-navigation` es una solución que usa sólo JavaScript, recreando los patrones y transiciones nativas en JS aunque basándose en _primitivas_ nativas, mientras que `react-native-navigation` se un _wrapper_ de la navegación nativa exponiendo una API en JS de fácil uso.

#### Usabilidad

Si bien tienen diferencias, ambas tienen una manera de usarse similar, y si bien hay argumentos a favor y en contra para cada una, suelen ser muy subjetivos. Podemos decir que no hay un _ganador_ ni _perdedor_ en este punto, sino que es una cuestión de _gustos y costumbres_ más que de razones objetivas.

#### Performance

Ambas logran una excelente performance en cuanto a transiciones, ya que las animaciones para ambos casos se ejecutan en el thread de UI logrando los 60 FPS necesarios para que una animación sea fluida. Sin embargo, `react-navigation` puede sufrir el clásico problema de _bloqueo del thread de JS_ a diferencia de `react-native-navigation`.

#### Look and feel nativo

Este es el punto donde `react-native-navigation` es claramente superior. Al ser un _wrapper_ sobre la navegación nativa, los componentes de UI y transiciones son exáctamente igual a los nativos (porque justamente usa los mismos).
En contraposición, `react-navigation` crea réplicas de las transiciones nativas y como resultado podemos notar algunas muy sutiles diferencias.

#### Adopción

Quizás la mayor ventaja de `react-navigation` es que, al ser puramente JS, hace que su integración sea más simple ya que no hace falta integrar nada desde el lado nativo. Esta es la razón por la que Expo la recomienda como opción, otro punto que hace que su adopción sea mayor que `react-native-navigation`.

## Navegación en Expo

Como dijimos antes, Expo recomienda `react-navigation` como opción, no sólo por ser la de mayor adopción, sino también porque **no es posible** usar `react-native-navigation`, ya que es un módulo que contiene código nativo.
La única opción sería que Expo la incluya dentro de su _core_, cosa que seguramente no pase ya que ellos fueron los principales promoveedores y contribuidores de `react-navigation` desde un principio.

### Integrando React Navigation

Siendo que **React Navigation** es la mejor opción que tenemos veamos cómo integrarla en un proyecto de Expo.

> Podés encontrar una guía detallada en su [documentación](https://reactnavigation.org/docs/en/getting-started.html)

#### Instalación

Lo primero que necesitamos es instalar la dependencia

```bash
yarn add react-navigation
```

#### Creando un Stack de navegación

Para poder navegar entre pantallas primero hace falta tener... **pantallas!!** 😁
Por eso es que vamos a crear dos archivos `Screen1.js` y `Screen2.js`, cada uno con un contenido parecido a lo siguiente

```js
import React from 'react'
import { View, Text } from 'react-native'

class Screen1 extends React.Component {
  render() {
    return (
      <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
        <Text>Screen 1</Text>
      </View>
    )
  }
}

export default Screen1
```

Luego vamos a reemplazar dentro de `App.js` la clase **App** para que ahora devuelva un Stack de navegación.
Para eso debemos:

1. Importar `createStackNavigator` de `react-navigation`
1. Importar las dos _Screens_ que creamos (`Screen1.js` y `Screen2.js`)
1. Crear un nuevo _Stack_ usando `createStackNavigator` y nuestras dos _Screens_
1. Hacer que nuestra app devuelva ese _Stack_ en el `render`.

```js
import React from 'react'
import { createStackNavigator } from 'react-navigation'
import Screen1 from './Screen1'
import Screen2 from './Screen2'

const RootStack = createStackNavigator({
  Screen1: {
    screen: Screen1,
  },
  Screen2: {
    screen: Screen2,
  },
})

export default class App extends React.Component {
  render() {
    return <RootStack />
  }
}
```

#### Agregando navegación entre pantallas

Por ahora solamente podemos quedarnos en el `Screen1` pero no podemos movernos a ningún otro. Para poder hacerlo, vamos a agregar un botón en `Screen1.js` que nos permita navegar a `Screen2`.
Simplemente importando `Button` de `react-native` y agregando un botón dentro del render

```js
import React from 'react'
import { Button, View, Text } from 'react-native'
import { createStackNavigator } from 'react-navigation'

class HomeScreen extends React.Component {
  render() {
    return (
      <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
        <Text>Screen 1</Text>
        <Button title="Ir a Screen2" onPress={() => this.props.navigation.navigate('Screen2')} />
      </View>
    )
  }
}
```
