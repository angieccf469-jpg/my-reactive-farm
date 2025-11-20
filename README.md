ANALISIS DE ESTE PROYECTO:

#1. Estructura del proyecto:

my-reactive-farm/
│
├─ public/
│
├─ src/
│  ├─ assets/                # Imágenes, íconos o JSON local
│  │   └─ animals.json
│  │
│  ├─ components/            # Componentes reutilizables y visuales
│  │   ├─ Alert.jsx          # Mensajes de error, éxito o información
│  │   ├─ Loader.jsx         # Indicador de carga
│  │   ├─ Layout.jsx         # Cómo están organizadas las secciones de la pantalla.
│  │   ├─ AnimalCard.jsx     # Muestra datos de un animal individual
│  │   ├─ AnimalList.jsx     # Renderiza la lista de animales
│  │   └─ AnimalForm.jsx     # Formulario controlado con validaciones
│  │
│  ├─ pages/                 # Vistas o pantallas principales
│  │   └─ Farm.jsx           # Página principal (usa useEffect + lógica)
│  │
│  ├─ services/              # Comunicación con la API (Axios o Fetch)
│  │   └─ animalsApi.js
│  │
│  ├─ hooks/                 # lógica reutilizable
│  │   └─ useFetchAnimals.js
│  │
│  ├─ App.jsx                # Enrutador principal o punto de entrada de componentes
│  ├─ main.jsx               # Renderiza la app dentro del root DOM
│  ├─ index.css              # Estilos globales (reset, tipografía, colores)
│  └─ variables.css          # Paleta, dark mode, etc.
│
├─ package.json
├─ vite.config.js            # Herramienta para crear y correr proyectos web muy rapido
└─ README.md                 # Archivo de texto 

#2. Manejo de estado (useState)

En el proyecto en la parte del Farm.jsx, se utiliza useState para controlar lo siguiente:
. Lista de animales
. Estado de carga
. Errores
. Formulario activo
. Animal seleccionado para editar 

useState permite que la interfaz se actualize automaticamente cuando cambia un dato.

#3. Los efectos (useEffect)

En este proyecto se utiliza para:
. Cargar los animales desde la API apenas inicia la pagina 
. Actualizar los datos cuando se cambia algo como por ejemplo (un ID)
. Manejar logica que ocurre por fuera del render

Ejemplo Farm.jsx:

useEffect(() => {
    loadAnimals();
}, []);

#4. El consume de API con axios y MockAPI

El proyecto usa:

. Axios --> para hacer la peticiones HTTP
. MockAPI --> como backend donde estan los animales 

La URL base viene de .env:

VITE_API_BASE=https://mockapi.../api/v1

Desde animalsApi.js se hacen operaciones como:

. GET: obtener animales 
. POST: crear uno nuevo 
. PUT: editar
. DELETE: eliminar

Farm.jsx usa esas funciones para mostrar y actualizar los datos en pantalla

#5. El manejo de formularios y validaciones 

El formulario permite:

. Agregar nuevos animales
. Editar los existentes 

Se maneja con estado useState para:

. controlar los inputs
. Validar 
. Enviar los datos ala API
. Limpiar el formulario despues de guardar

El componente animalForm es el encargado de esta logica y se conecta con Farms.jsx

#6. Uso de tailwind css 

Se usa como el sistema principal de estilos. No se escribe css manual, se usan clases utilitarias directamente
en los componentes de react.

En resumen el proyecto usa una estructura ordenada basada en componentes, maneja datos con useState, ejecuta procesos
con useEffect, consume una API real creada en mockAPI mediante Axios, y controla formularios para crear y editar 
animales desde la interfaz.

PROPOSITO GENERAL DEL PROYECTO:
Desarrollar una aplicación web interactiva que permite gestionar animales mediante una interfaz moderna, utilizando
react para el manejo dinamico de componentes, Axios y MockAPI para el consumo de datos externos, y Tailwind CSS para
un diseño responsivo, con el fin de practicar el uso de estados, efectos, formularios y consumo de APIs en un 
entorno real de desarrollo.

CUESTIONARIO DE REACT:

#1.¿Cuál es la diferencia entre un componente presentacional y un componente de página en React? Da ejemplos usando archivos del proyecto.

Presentacional: Solo muestra el UI, la interfaz del usuario, todo lo que el usuario ve.

En app.jsx , DarkModeToggle.jsx, AnimalCard.jsx, Loader.jsx 
son componentes presentacionales muestran botones, muestran datos de los animales y aplican estilos con Tailwind,
son piezas visuales.

Pagina: Maneja la logica, estado, Apis

Farm.jsx
Pantalla completa que usa muchas piezas y maneja toda la logica.

#2.¿Para qué se utiliza useState en el proyecto? Menciona dos estados distintos y su función.

Para guardar y actualizar datos que cabian en la interfaz, como la lista de animales o el estado del formulario.

ESTADO1.
const [animals, setAnimals] = useStates([]);
Función: guardar todos los animales que vienen de la API y actualizar la pantalla cuando cambian.

ESTADO2.
const [loading, setLoading] = useStates(true);
Función: mostrar un 'LOADER' mientras la API responde y ocultarlo cuando los datos ya estan listos.

#3. ¿Cómo se usa useEffect para cargar datos desde MockAPI al inicio? Explica el flujo.

useEffect se ejecuta una vez al iniciar y pide los datos a MockAPI con Axios, cuando llegan, actualiza el estado
y la pantalla. 

Se usa useEffect con un arreglo vacio[], lo que significa que se ejecuta esto solo una vez cuando la pagina cargue.

useEffect(() => {
    loadAnimals();
}, []);

FLUJO:
1.React carga el componente (Farm.jsx)
2.useEffect se activa una sola vez porque tiene un arreglo vacio []
3.Dentro del efecto se llama Axios , getAnimals()
4.Axios pide los datos a MockAPI (GET)
5.MockAPI responde con una lista de animales 
6.Se guardan los datos en el estado con setAnimals()
7.La interfaz se actualiza y muestra los animales

#4.¿Cómo maneja el proyecto los estados de loading, error y lista vacía? ¿Qué se muestra al usuario en cada caso?

1.Loading(cargando)
const [loading, setLoading] = useStates(true);
Es cuando la app esta esperando la respuesta de MockAPI
Le muestra al usuario un mnesaje que dice Cargando o un loading 

2.Error
const [error, setError] = useStates(null);
Si la peticion ala API falla, por ejemplo si no hay internet, el servidor se callo, etc
Le muestra al usuario una alerta o un mensaje tipo, ocurrio un error al cargar los datos.

3.Lista vacia
const [animals, setAnimals] = useStates([]);
Si la API responde pero no hay animales, la lista queda vacia
Le muestra al usuario un mensaje tipo, no hay animales registrados o un componente vacio para informarle al usuaio

#5.¿Qué significa que un formulario sea controlado en React? Relaciónalo con el formulario del proyecto.

Significa que react controla el valor de cada input usando useStates, no el navegador
Cada vez que el usuario escribe, el estado se actualiza
El input siempre muestra ese estado
En el formulario de animales( AnimalForm), los campos los campos como:
.Nombre
.Tipo
.Edad
.Imagen

Se manejan con estados como:

const [formData, serFormData] = useStates({
    name: "",
    type: "",
    age: "",
});

Y cada input hace esto:

<input
  value={formData.name}
  onChange={(e)} =>
  setFormData({...formData, name: e.target.value})
  />

#6.¿Por qué es buena práctica separar la lógica de datos en archivos como animalsApi.js en vez de hacer peticiones dentro de los componentes?

Separar la API en animalsApi.js hace que el codigo se vea mas limpio, reutilizable, organizado mas profesional y facil de mantener.

#7.¿Qué hace que AnimalCard sea un componente reutilizable? ¿Cómo se podría usar una tarjeta similar en otro contexto?

AnimalCard es reutilizable porque recibe datos por props y solo muestra UI.
Se puede usar la misma estructura para mostrar cualquier tipo de tarjeta, commo por ejemplo tarjeta de productos o de 
usuarios, peliculas, libros. etc.

#8.¿Qué elementos del proyecto contribuyen a la accesibilidad? Menciona tres y explica su importancia.

1.Modo oscuro (DarModeToggle)
.Permite cambiar entre modo oscuro y claro
.Ayuda a personas con sensibilidad al brillo o problemas visuales

Mejora la lectura y reduce fatiga visual.

2.Textos claros y buen contraste usando Tailwind css
El proyecto usa clases como:
.text-gray-800
.dark:text-gray-100
.bg-white dark:bg-neutral-900

.Los textos siempre tienen un constraste adecuado en ambos modos
.Personas con dificultad de la vision se les facilita leer

3.Mensajes de estado(Loader, Alert)
Cuando hay:
.Carga
.Error
.Lista vacia
El usuario recibe un mensaje visual claro

.Las personas entienden que esta pasando sin confundirse
.Ayuda a los usuarios con dificultades cognitivas o de comprensión

4.Uso de componentes simples y estructurados
Los componentes como tarjetas, formularios y botones son claros, grandes y faciles de usar.
Mejoran la navegación para personas con dificultades motoras.

#9.Antes de agregar una funcionalidad nueva, ¿qué pasos debes pensar según la filosofía de React? (ej.: qué datos, qué estado, dónde vive la lógica)

Hay que pensar en:

1.Que datos necesito?
.Una lista?,un texto?,un numero?

2.Que estado useStates debo crear?
.Hay q guardar algo q cambia?

3.En que componente pongo los datos para que se compartan correctamente?
.Debe estar en el componente mas alto que lo necesite

4.Que logica tengo q ejecutar?
.Debo llamar ala API?
.Debo validar un formulario?
.Debo modificar un arreglo?

5.Que componentes deben recibir esos datos como props?
.AnimalCard recibe props como nombre, edad, imagen

6.Debo usar un useEffect?
.Solo si necesito cargar algo al inicio o reaccionar a cambios
.Como cargar animales cuando inicia la pagina

#10.¿Qué conceptos de React aprendidos en este proyecto podrías reutilizar en otro tipo de aplicación? Da al menos cuatro ejemplos.

1.useStates (manejo de estados)
Sirve para guardar datos que cambian
.formularios.
.contadores
.listas
.Modos(oscuro/claro)
Se puede usar en cualquier app que muestre información dinamica 

2.useEffect (cargar datos o ejecutar logica al inicio)
.Cargar datos de un API
.Escuchar cambios
.Ejecutar codigo al montar el componente
Es importante en apps reales

3.Consumo de API con Axios
.Obtener datos
.Enviar datos
.Actualizar recursos
.Eliminar elementos 
Cualquier app moderna usa APIs

4.Componentes reutilizables como(AnimalCard)
Se puede crear:
.Tarjetas
.Botones
.Formularios
.Layouts
.Encabezados reutilizables  

5.Props(pasar datos entre componentes)
.Datos que un componente le pasa a otro para que los muestre o use

6.Formulario controlado
Es fundamental para:
.Login
.Registro
.Busquedas
.Formuarios de contacto
