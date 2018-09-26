### Template Strings

Los _template strings_ hacen más simple la construcción de _strings_ en base a parámetros, entre otras cosas.
El caracter que se usa para definirlos es la tilde invertida (\`\`), a diferencia de los _strings_ tradicionales que se definen con comillas simples o dobles ('', "")

Tiene otros usos más complejos que no veremos en este documento, ya que probablemente no necesites usarlos.

#### En código

```javascript
const nombre = 'Pedro'
const edad = 30

// Lo que antes se hacía así
console.log('El señor ' + nombre + ' tiene ' + edad + ' años')
// Ahora puede hacerse más simple
console.log(`El señor ${nombre} tiene ${edad} años`)
```

#### ¿Y cuándo lo uso?

Cada vez que tengas que definir un texto en base a ciertas variables, ya sea texto que uses para _debuggear_, para mostrar en algún componente, o cualquier otro propósito.
