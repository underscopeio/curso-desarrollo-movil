# Clase 6

## Componentes de UI de React Native

Como ya sabemos, **React Native** es un framework para desarrollar aplicaciones móviles y como tal posee una serie de componentes de UI ya incluidos que hacen simple la construcción de interfaces de usuario no tan simples.

Si bien no existe una forma estándar de caracterizarlos, podríamos dividirlos en grupos en base a la función que cumplen:

- **Componentes Base**, también llamados _Building Blocks_
- **Inputs**, que sirven para que el usuario pueda ingresar información
- **Touchables**, que permiten detectar _touches_ en cualquier componente
- **Scrollables**, que son contenedores que permiten deslizar el contenido
- **Otros de React Native**, que no corresponden a las categorías anteriores
- **Extras de Expo**, que son componentes no incluídos en React Native pero si en Expo

### Componentes Base

- **View** es el componente base por excelencia de React Native
- **Text** es necesario siempre que querramos mostrar un texto
- **Image** para mostrar imágenes (tanto internas como externas)

### Inputs

- **TextInput** deja al usuario ingresar un texto usando el teclado
- **Picker** muestra una lista de opciones al usuario para que seleccione una
- **Slider** deja al usuario elegir un valor numérico entre dos límites
- **Switch** usado para definir valores booleanos (verdadero/falso)
- **Button** presionable por el usuario

### Scrollables

- **ScrollView** hace scrollable el contenido que sobrepasa la pantalla
- **ListView** renderiza contenido de a partes, a diferencia del **ScrollView**
- **FlatList** es una versión más nueva y sencilla del **ListView**
- **SectionList** permite crear listas que pueden separarse en secciones

### Otros incluídos de React Native

Además de los ya mencionados, React Native posee componentes adicionales muy útiles, entre los que podemos destacar:

- **Modal**
- **ActivityIndicator**
- **RefreshControl**
- **WebView**
- Algunos propios de iOS, como **DatePickerIOS** y **TabBarIOS**
- Algunos propios de Android, como **ProgressBarAndroid** y **ViewPagerAndroid**

Dentro de la [documantación de React Native](https://facebook.github.io/react-native/docs/getting-started), en la sección **Componentes** del menu izquierdo se pueden encontrar todos los disponibles.

### Componentes Extras incluídos en Expo

Expo incluye componentes adicionales a todos los ya incluídos por React Native. Si bien son muchos, podemos mencionar algunos:

- **MapView** tomado de `react-native-maps`
- **Video** para reproducir videos
- **Svg** para mostrar SVGs
- **Lottie** para ejecutar animaciones hechas en **After Effects**
- **GLView**
- **BlurView**

La lista completa puede encontrarse en su [documentación](https://docs.expo.io/versions/latest/sdk)
