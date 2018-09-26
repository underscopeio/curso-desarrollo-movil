# Clase 7

## Módulos externos

Por lo general, con los **componentes y APIs** que incluyen **React Native y Expo** es más que suficiente para construir la aplicación que queremos.
Sin embargo, puede pasar que necesitemos algo que no es parte del _core_ de React Native o Expo. En esos casos podemos recurrir a **módulos externos** que satisfagan nuestra necesidad.

### Package Managers

Para poder usar estos módulos externos lo más común es usar un _package manager_ que nos ayude con la descarga, instalación y configuración de estas _dependencias_, además de mantener un repositorio de público acceso desde donde se descargan todos esos módulos.
Con la aparición de **NodeJS** surgió **npm** (acrónimo de **Node Package Manager**) y se convirtió en el estándar para manejar paquetes de JavaScript.
Más tarde Facebook creó **yarn**, una alternativa a **npm** manteniendo las mismas funcionalidades y agregando algunas extras.

Cualquiera de las dos nos sirve a nuestro propósito de poder usar módulos externos en nuestro proyecto.

### ¿Cómo uso un módulo externo?

Tanto **npm** como **yarn** proveen una **CLI** para poder instalar módulos fácilmente.
Como cada módulo tiene un nombre único (que funciona como identificador) sólo necesitamos eso para poder instalarlo.

Pongamos por caso que queremos instalar `lodash` en nuestro proyecto. Lo que tenemos que hacer es, usando la terminal y dentro de la carpeta de nuestro proyecto ejecutar

```sh
yarn add lodash
# o usando npm
npm install lodash --save
```

### ¿Donde encuentro módulos externos?

La mayoría de los módulos externos son **OSS** (Open Source Software) y se encuentran en **Github**.
Además, los nombre de los módulos que sirven exclusivamente para proyectos de **React Native** suelen comenzar con `react-native-`, por lo que es fácil reconocerlos.

### ¿Puedo usar cualquier módulo de npm/yarn en mi proyecto de React Native/Expo?

**No**, no todos los módulos van a servir en cualquier proyecto. Recordemos que originalmente **npm** se pensó para paquetes para NodeJS.
Como regla, podemos decir que:

- Si el módulo usa algo relacionado al browser (como `window`, por ejemplo) o NodeJS, entonces no puedo usarlo (existe [una manera de usar paquetes de Node](<(https://code.janeasystems.com/nodejs-mobile/getting-started-react-native)>), pero no es tan sencilla)
- Si el módulo **contiene código nativo**, entonces puedo usarlo en un **proyecto React Native, siempre y cuando no use Expo**
- Si el módulo es **puramente JavaScript**, entonces puedo usarlo en **cualquier proyecto React Native**, use o no use **Expo**

### ¿Y si no hay ningún módulo para lo que necesito?

Si ya buscaste en [Github](https://github.com/), [npm](https://www.npmjs.com/), [esta lista de componentes](https://github.com/jondot/awesome-react-native), [esta otra](https://github.com/madhavanmalolan/awesome-reactnative-ui) y todavía seguís sin encontrar lo que necesitas, entonces... **podés hacer tu propio módulo!**

Si tu módulo usa sólo JavaScript, entonces es sencillo: en un nuevo archivo podés desarrollar la funcionalidad que necesites y luego simplemente usarlo.

Si tu módulo va a contener código nativo, entonces te recomiendo que leas estas guías sobre cómo hacer módulos nativos:

- [Componentes de UI Nativa para Android](https://facebook.github.io/react-native/docs/native-components-android)
- [Componentes de UI Nativa para iOS](https://facebook.github.io/react-native/docs/native-components-android)
- [Módulos nativos para Android](https://facebook.github.io/react-native/docs/native-modules-android)
- [Módulos nativos para iOS](https://facebook.github.io/react-native/docs/native-modules-ios)

> Tené en cuenta que estos módulos nativos vas a poder usarlos sólo en proyectos de **React Native** que no usen **Expo**.
