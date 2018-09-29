## Cómo integrar la API de Spotify en una aplicación de Expo

Veremos un paso a paso de cómo integrarnos con la API de Spotify para consumir información desde nuestra aplicación. Vamos a separar esta guia en tres partes:

1. Creación de una _aplicación de Spotify_ desde el sitio web de Desarrolladores de Spotify
2. Configuración en una aplicación de Expo para pedir al usuario autorización para usar su data de Spotify
3. Implementación de llamadas a la API de Spotify para obtener datos

### Parte uno - Crear aplicación en Spotify

#### 1) Crear una cuenta en Spotify

Para poder usar la API de Spotify, primero necesitamos tener una cuenta (ya sea _Free_ o _Premium_) en este servicio. Si ya tenés una cuenta podés avanzar al paso siguiente, si no podés hacer una gratuitamente desde el sitio de [Spotify](https://www.spotify.com).

#### 2) Crear una aplicación de Spotify

Además de una cuenta de Spotify, es necesario dar de alta una _app_ que nos permitirá comunicarnos con la API.
Para eso desde el [Dashboard](https://developer.spotify.com/dashboard/applications) podemos crear una nueva, eligiendo un nombre y descripción para la misma, marcando que NO es para uso comercial (en este caso) y finalmente aceptando los términos y condiciones.

#### 3) Obtener el Client ID

Una vez creada la _app_ vamos a poder obtener el **Client ID** de la misma, que debería ser un código hexadecimal de 18 caracteres como este `bb223824c29844c7999ac5bc0ab7fdff`. Este dato no es sensible, a diferencia del **Client Secret** que nunca deberíamos hacer público.

#### 4) Definir qué queremos obtener de la API

Consultando la documentación de todos los [_endpoints_ disponibles](https://developer.spotify.com/documentation/web-api/reference/) en la API de Spotify podemos definir qué permisos necesitamos pedirle al usuario al momento de autorizar a nuestra aplicación. Estos permisos se llaman _scopes_.

Si un endpoint necesita algún permiso en particular va a estar detallado en la sección de **Request Parameters** > **Header Fields** > **Authorization**. Por ejemplo, para obtener los [artistas que sigue un usuario](https://developer.spotify.com/documentation/web-api/reference/follow/get-followed/) necesitamos el scope `user-follow-read`.

### Parte dos - Pedir autorización al usuario

#### 1) Usar `AuthSession` de Expo

Expo nos provee de `AuthSession` para simplificar el proceso de autenticarnos via un navegador, cómo es el caso de los flujos de autenticación con OAuth. Además de ahorrarnos varios pasos del proceso, tiene una [guía detallada](https://docs.expo.io/versions/latest/sdk/auth-session) de cómo hacerlo.

#### 2) Copiar su ejemplo

Como primer paso vamos a copiar el ejemplo que ellos proponen.

```js
import React from 'react'
import { Button, StyleSheet, Text, View } from 'react-native'
import { AuthSession } from 'expo'

const FB_APP_ID = 'YOUR_APP_ID'

export default class App extends React.Component {
  state = {
    result: null,
  }

  render() {
    return (
      <View style={styles.container}>
        <Button title="Open FB Auth" onPress={this._handlePressAsync} />
        {this.state.result ? <Text>{JSON.stringify(this.state.result)}</Text> : null}
      </View>
    )
  }

  _handlePressAsync = async () => {
    let redirectUrl = AuthSession.getRedirectUrl()
    let result = await AuthSession.startAsync({
      authUrl:
        `https://www.facebook.com/v2.8/dialog/oauth?response_type=token` +
        `&client_id=${FB_APP_ID}` +
        `&redirect_uri=${encodeURIComponent(redirectUrl)}`,
    })
    this.setState({ result })
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
  },
})
```

#### 3) Adaptar el ejemplo a Spotify

El ejemplo de Expo muestra cómo autenticarse a Facebook, por lo que necesitamos hacer algunos cambios.

- En lugar de `FB_APP_ID` usaremos `SPOTIFY_CLIENT_ID` y le asignaremos el **Client ID** que obtuvimos de la web de Spotify.
- Reemplazar la `authUrl` para que use la de Spotify. En este caso como vamos a usar el [**Implicit Grant Flow**](https://developer.spotify.com/documentation/general/guides/authorization-guide/#implicit-grant-flow) lo mínimo que tenemos que hacer es: cambiar la base de la URL para que use la API de Spotify, mantener el `response_type` con `token` y cambiar el `client_id` para que use `SPOTIFY_CLIENT_ID`. (ver snippet debajo)
  ```js
  let result = await AuthSession.startAsync({
    authUrl:
      `https://accounts.spotify.com/authorize?response_type=token` +
      `&client_id=${SPOTIFY_CLIENT_ID}` +
      `&redirect_uri=${encodeURIComponent(redirectUrl)}`,
  })
  ```
- Cambiar el texto `Open FB Auth` por `Open Spotify Auth`

#### 4) Hacer una prueba desde un dispositivo

Al parecer `AuthSession` no funciona correctamente en los emuladores (al menos para iOS) por lo que deberemos probarlo en un dispositivo real.
Al intentar autorizar a nuestra app con un usuario de Spotify, veremos que Spotify nos devuelve un error que dice algo sobre `INVALID_CLIENT`.
Esto pasa porque todavía nos falta configurar la app de Spotify y definir qué valor para `redirect_url` es válido (pueden ser múltiples).

#### 5) Configurar la redirect_url en Spotify

Primero debemos saber qué `redirect_url` genera `AuthSession.getRedirectUrl()`. La misma tiene el formato `https://auth.expo.io/@your-username/your-app-slug` (reemplazando `@your-username` y `your-app-slug`, por supuesto).
Si queremos estar seguros de qué URL genera, podemos agregar un log en el método `_handlePressAsync`

```js
let redirectUrl = AuthSession.getRedirectUrl()
console.warn('Esta es la URL: ', redirectUrl)
```

Una vez obtenida esa URL, debemos ir al sitio de administración de Spotify, clickear en el botón de **Edit Settings** y agregarla a la lista de **Redirect URIs**.

#### 6) Volver a probar desde nuestra aplicación

Si volvemos a loguearnos usando Spotify esta vez deberíamos ver un JSON como resultado donde está, entre otras cosas, el `access_token` necesario para poder interactuar con la API.

### Parte tres - Implementar llamadas a la API
