### Importar y exportar módulos

Lo que antes resolvían los _module loaders_ (como AMD y CommonJS) ahora lo hace JavaScript incorporando el soporte para módulos.
Siguiendo la linea de JavaScript, los módulos se cargan asincrónicamente una vez que son requeridos (es decir, importados).

#### En código

Supongamos que definimos un módulo para _hacer cuentitas_ dentro de una carpeta `lib` llamado `math.js`

```javascript
// Este sería el contenido del archivo `lib/math.js`
export function sumar(x, y) {
  return x + y
}

export const PI = 3.141593
```

Luego puedo desde otro archivo (supongamos `app.js`) importar todo lo que exporte el módulo de la siguiente manera

```javascript
import * as math from './lib/math'

console.log('2π = ' + math.sum(math.PI, math.PI))
```

También puedo importar sólo lo que vaya a usar de la siguiente forma

```javascript
import { sumar } from './lib/math'

console.log('2 + 2 = ' + math.sum(2, 2))
```

Adicionalmente, se puede usar `export default` que luego puede ser importado sin declarar qué en particular.
Supongamos que creamos un módulo que solo sirve para sumar.

```javascript
// Este sería el contenido del archivo `lib/sumar.js`
export default function sumar(x, y) {
  return x + y
}
```

Luego para importarlo

```javascript
import sumar from './lib/sumar'

console.log('dos más dos es ' + sumar(2, 2))
```

#### ¿Y cuándo lo uso?

Vas a usarlo todo el tiempo: cada vez que importes React para crear un componente, al usar cualquier módulo (externo o interno).

Por ejemplo, si querés crear un componente propio (supongamos `boton.js`)

```javascript
import React, { Component } from 'react'

export default class Boton extends Component {
  render() {
    //
  }
}
```

Luego desde tu app

```javascript
import React, { Component } from 'react'
import Boton from './boton'

class App extends Component {
  render() {
    return (
      <View>
        <Boton />
      </View>
    )
  }
}
```
