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
