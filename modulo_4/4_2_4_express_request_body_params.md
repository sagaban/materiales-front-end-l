# Express: body params

En esta lección vamos a explicar cómo enviar datos a través de body params. Es exactamente lo mismo que enviar datos con query params, pero por otro sitio.

&#10230; &#128250; **Echa un vistazo [a este vídeo sobre body params](https://www.youtube.com/watch?v=3qyVgwQ2I58).**

> [Ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-2-express-request-body-params)

## Características de los body params

- Desde el navegador:
   - Se añaden en el cuerpo del fetch.
   - Se pueden utilizar con cualquier verbo (POST, PUT, PATCH...) excepto GET.
   - Se envían en formato JSON pero en string y con la cabecera que indica que estamos enviando datos en formato JSON, es decir, con:
      ```js
      fetch('http://localhost:3000/user', {
        method: 'POST',
        body: JSON.stringify(bodyParams),
        headers: {
          'Content-Type': 'application/json'
        },
      })
      ```
   - Como lo que estamos enviando es un objeto de JS este puede ser todo lo complejo que queramos. Puede ser un objeto que dentro tenga un array, y dentro otro objeto y dentro strings, numbers, booleans...
- En el servidor:
   - Recibimos los datos en `req.body`.
   - Tenemos que acordarnos de poner `server.use(express.json());`. Si no, el objeto `req.body` estará vacío.

## Ejercicios

### 1. Filtrar usuarias por nombre

Vamos a partir del [ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-2-express-request-body-params) y a añadir una nueva funcionalidad. Ya sabemos que cuando pulsamos en el segundo botón del ejercicio, se llama al endpoint http://localhost:3000/users y el servidor nos devuelve el listado completo de usuarias.

Pues bien, queremos añadir un filtro a la web y al servidor para que el servidor nos devuelva las usuarias filtradas por nombre. Para ello:

1. Añade un campo de filtro a la web:
   1. Edita `public/index.html` para añadir un input de texto en el segundo rectángulo.
   1. Edita `public/js/main.js` para que cuando ejecutamos `fetch('http://localhost:3000/users')` se envíe por body params un nuevo dato con el nombre `filterByName`.
   1. Comprueba desde devtools > network qué la llamada que estás haciendo tiene el formato correcto, es decir la URL concatendada con el body param. Si este formato es correcto ya puedes empezar a editar el servidor.
1. Añade el filtro al servidor:
   1. Edita `src/index.js`.
   1. En el endpoint `server.get('/users', (req, res) => {...})` debes recoger el body param `filterByName` y guardarlo en una constante.
   1. En el ejercicio del vídeo estamos devolviendo todo el array de usuarias, que lo hacemos con el código:
      ```js
      res.json({
        result: users
      });
      ```
      Cambia este código para que no devuelva todo el array sino un array con solo aquellas usuarias cuyo nombre contenga el texto escrito en el input de filtrado.

Recuerda que para que el array `users` tenga usuarias hay que añadir usuarias a través del primer formulario de la web.

### 2. Filrar usuarias por nombre e email

Partiendo del ejercicio anterior:

1. Añade un segundo campo de texto a la web para filtrar por email y envíalo también por body params al servidor.
1. Añade un segundo filtro en el servidor en la función `server.get('/users', (req, res) => {...})` para que el servidor solo devuelva aquellas usuarias cuyo nombre contenga el texto del filtro de nombre y cuyo email contenga el texto del filtro de email.

##### ¿Te ha gustado?

Por favor rellena este [formulario](https://adalab.typeform.com/to/Rc0bft9x) para darnos feedback sobre la calidad de esta mini lección.