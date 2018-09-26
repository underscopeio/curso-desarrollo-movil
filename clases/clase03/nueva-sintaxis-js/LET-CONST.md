### Let y Const

Estas dos nuevas palabras clave sirven para declarar variables dentro de un bloque (un bloque es todo lo que está entre llaves `{}`).
Con `const` declaramos variables que **NO pueden ser reasignadas** dentro del mismo bloque, es decir, variables **constantes** (de ahí el nombre)
Con `let` declaramos variables que **SI pueden ser reasignadas**

Ninguna es un reemplazo de `var` en el sentido de que no funcionan de la misma forma. Una de las estrategias más usadas por la comunidad (y que aconsejo personalmente) es:

- dejar de usar `var`
- usar `const` siempre que se pueda
- usar `let` en los casos que quiera reasignar esa variable

#### En código

```javascript
// ERROR!
// No se puede reasignar la variable `x` declarada como `const`
function constReasignada() {
  {
    const x = 1
    x = 2
  }
}

// FUNCIONA!
// Puede reasignarse `x` ya que se declaró como `let`
function letReasignada() {
  {
    let x = 1
    x = 2
  }
}

// ERROR!
// No se puede redefinir la variable `x` dentro del mismo bloque
// (NOTA: no es lo mismo reasignar que redefinir)
function constRedeclarada() {
  {
    const x = 1
    const x = 2
  }
}

// ERROR!
// No se puede redefinir la variable `x` dentro del mismo bloque
// (NOTA: Tanto `let` como `const` pueden ser definidas solamente una vez dentro de un mismo bloque)
function letRedeclarada() {
  {
    let x = 1
    let x = 2
  }
}

// FUNCIONA!
// Al estar definidas en distintos bloques, son variables distintas
function constRedeclaradaEnOtroBloque() {
  {
    const x = 'bloque externo'
    console.log('Uno: ', x) // -> 'Uno: bloque externo'
    {
      const x = 'bloque interno'
      console.log('Dos: ', x) // -> 'Dos: bloque interno'
    }
    console.log('Tres: ', x) // -> 'Tres: bloque externo'
  }
}

// FUNCIONA!
// Al estar definidas en distintos bloques, son variables distintas
// La variable `const x` NO existe en el bloque interno
function letRedeclaradaEnOtroBloque() {
  {
    const x = 'bloque externo'
    {
      let x = 'bloque interno'
    }
  }
}

// FUNCIONA!
// Una variable definida con `const` NO puede ser reasignada pero SI alterado su contenido
function objetosYArreglosConst() {
  {
    const persona = { nombre: 'María' }
    persona.nombre = 'María Clara'
    persona.edad = 30

    const numeros = [1, 2, 3]
    numeros.push(4)
    numeros.concat([5, 6, 7])
  }
}
```

#### ¿Y cuándo lo uso?

Siempre que declares variables.
Recordá usar `const` por defecto y usar `let` solamente cuando necesites reasignar esa variable (el caso más común son los loops, `for(let i = 0, i++, i < 10)`)
