Actividad #1

En esta actividad cambie el estado loading dentro del archivo Farm.jsx en la linea const [loading, setLoading] = useState(true);, originalmente estaba en true, indicando que la aplicación debia mostrar el componente loader mientras se cargaba los dato del API.

Cuando pase loading a false al inicio, no vi cambios porque el useEffect lo activaba otra vez con setloading(true).
Al desactivar esa linea temporalmente, si pude ver el efecto del cambio.

.La interfaz ya no mostraba el loader.
.La app trato de mostrar los animales inmediatamente.
.Esto demuestra como el estado controla lo que el react renderiza.