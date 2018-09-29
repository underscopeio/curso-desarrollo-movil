# Clase 9

## Web APIs

Una **Web API** es una API que puede ser consumida via **HTTP**, el protocolo usado en la **Web**.
En la actualidad prácticamente toda red social y servicio web popular tiene su propia API.
Por mencionar algunos, **Facebook**, **Twitter** e **Instagram** tienen una. También servicios de pagos como **PayPal** y **Stripe**, de SMS y mensajes de voz y video como **Twilio**, o de autenticación como **Auth0**.

### Para qué sirven

El uso que podemos darle a una API depende precisamente de quien provee la misma.
En el caso de las redes sociales, probablemente nos dejen obtener cierta información de los usuarios, e incluso poder publicar cosas en su nombre (en algunos casos).
En el caso de los proveedores de pagos, podemos crear un _pedido de pago_, ejecutarlo, cancelarlo o devolverlo.

**Lo que podamos hacer o no, va a depender siempre de quien nos provee la API.**

### Cómo se usan

La manera de consumir una API va a depender de qué estándares adopten, sobre todo en cuanto a formato del contenido y tipo de autorización.

Si bien hay excepciones la mayoría de las APIs siguen los siguientes:

- Formato **JSON**: tanto el _payload del request_ como el _response_ suele ser en formato **JSON**
- Autorización via **OAuth**: en el caso de necesitar autorización para consumir la API, se suele usar este estándar. Actualmente la versión más adoptada (por cuestiones de seguridad) es **OAuth 2**

Asumiendo que se cumplen estas dos condiciones, los pasos a seguir (a grandes rasgos) son los siguientes.

#### Dar de alta una cuenta

Por lo general siempre hace falta dar de alta una cuenta para poder usar una API. La mayoría de los proveedores de APIs tienen un sitio separado para developers (Facebook, Twitter, Instagram, PayPal, Stripe, por nombrar algunos) donde podemos crear una cuenta con la que podremos interactuar con la API.

#### Obtener credenciales

Una vez creada la cuenta, vamos a necesitar obtener credenciales para que la API nos autorize cuando queramos interactuar con la misma.
Hay distintos tipos de credenciales, que varían en cuanto a su tiempo de expiración y su uso (clieant-side o server-side).

Si usamos **OAuth** las credenciales se obtienen haciendo un request a un _endpoint_ específico de la API donde se aclaran los _scopes_ requeridos (es decir, los permisos que se quieren obtener del usuario). Dependiendo del tipo de autorización la respuesta de ese _request_ puede ser un **access token** o un **authorization code**.

#### Efectuar llamados a la API

Teniendo ya un **token** (o el tipo de credencial que corresponda) podemos interactuar con la API.
Por lo general una API tiene múltiples _endpoints_ dependiendo de la data que querramos obtener o la operación que querramos hacer.
Los _requests_ que vamos a hacer a la API se hacen via HTTP, por lo que tenemos que tener en cuenta:

- **El método HTTP**: dependiendo lo que querramos hacer, puede ser un `GET`, `POST`, `PUT` o `DELETE`, entre otros
- **Los headers**: en los mismos generalmente se incluye el **token** de autorización
- **Query strings**: con ellos muchas veces se pasan _parámetros_ según cada enpoint
- **El payload**: para request que no sean `GET` muchas veces pueden enviarse parámetros dentro del payload, usados sobre todo en `POST` y `PUT`.

#### Procesar la respuesta

Al ser un request HTTP, la respuesta puede ser satisfactoria (código 2**) o erronea (código 4** o 5\*\*).
En caso de ser satisfactoria, tendremos la respuesta de la API y de allí podemos obtener la información que necesitemos.
