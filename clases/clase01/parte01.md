# Clase 1 - Parte 1

## Historia

### Nativo

El desarrollo móvil surgió hace ya varios años y trajo consigo nuevos problemas y desafíos que no existían en otros tipos de desarrollo (web, por ejemplo).
Empezando por el tamaño de pantalla mucho menor a lo acostumbrado, pasando por temas de conectividad (WIFI/3G/etc), memoria y muchos mas.
Sobre todo, el hecho de que existan distintas plataformas, con iOS y Android en la cabeza, y que estas plataformas tengan grandes diferencias tanto en hardware como software, hace que el desarrollo de aplicaciones móviles sea muy complejo.

Originalmente la única manera de desarrollar las mismas era hacerlo por separado para cada una de las plataformas en las que quisiésemos que nuestra aplicación esté disponible. Es decir, desarrollar una aplicación para **Android** (en Java) y otra para **iOS** (en Objective-C).
Esto significaba equipos separados de desarrollo, y en consecuencia más tiempo y más dinero necesario para el desarrollo en múltiples plataformas.

### Híbrido basado en WebView

Con el tiempo nuevas alternativas surgieron haciendo posible el desarrollo de aplicaciones. Como estas plataformas incluían un `WebView` (es decir, un componente donde pueden verse páginas web) dentro de su _core_ no tardaron en aparecer herramientas que permitían crear una aplicación que internamente muestre una web. El resultado: una aplicación que podía instalarse desde los stores pero que internamente mostraba una web, es decir que el código era principalmente `html`, `css` y `js`. Estas alternativas, con **Phonegap** y luego **Ionic** a la cabeza, se volvieron muy populares justamente por ser **multiplataforma** y porque los skills necesarios eran prácticamente los mismos que los de la web, haciendo que muchos desarrolladores web puedan incursionar en el desarrollo móvil.

Sin embargo, este tipo de aplicaciones tenían (y siguen teniendo) una gran desventaja: al correr en un `WebView` presentan muchas limitaciones, sobre todo en términos de performance. Es notable la diferencia de _fluidez_ de animaciones y el uso de componentes que no son nativos, sino recreados en `html`, `css` y `js`.

### Híbrido basado en componentes nativos

Por suerte para nosotros, en estos últimos años vieron la luz otro tipo de aplicaciones donde podemos escribir código que es compartido entre múltiples plataformas pero que usa componentes nativos. Es decir, podemos obtener **aplicaciones nativas** reusando el código entre plataformas.

Una de las alternativas más importante (si no la más) dentro de este grupo es **React Native**.

## React Native

React Native es un framework para construir aplicaciones nativas usando **JavaScript** y **React**.  
Es desarrollado y mantenido por **Facebook**, al igual que **React**.

### ¿Por qué elegimos React Native?

- **Comunidad:** la mayor comunidad para tecnologías mobile de este tipo. En parte a que es OSS y tiene licencia MIT.
- **Soporte:** el desarrollo está liderado por Facebook
- **React:** al usar React, los mismos skills para desarrollar en mobile nos sirven para la web

## Expo

Expo es un conjunto de herramientas para desarrollar aplicaciones en React Native, simplificando mucho el proceso, sobre todo al dar los primeros pasos.
Gracias a **Snack** (una de sus herramientas) podemos crear, editar y probar una aplicación en tiempo real, sin necesidad de configurar nada en nuestra computadora.

### ¿Por qué conviene usar Expo para empezar?

- **Setup:** no hace falta _perder_ tiempo en hacer el setup necesario para buildear para Android y/o iOS
- **Target:** Expo está especialmente pensado para aquellos que están empezando con React Native
- **Features:** las funcionalidades y paquetes que incluye por defecto son muy útiles y suficientes para muchas apps
