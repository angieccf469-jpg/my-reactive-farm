Actividad #2

En esta actividad agregue un filtro para permitir que los usuarios filtren animales por edad.
Cree un nuevo estado en el componente Farm.jsx:
const [ageFilter, setAgeFilter] = useStates("");
Este estado guarda la edad minima que debe tener el animal para aparecer en la lista.

Agregue un control nuevo en la interfaz input numerico, el input le permite al usuario escribir una edad minima.

Modifique la logica de filtrado en filterAnimlas:
Agregue una condición nueva:
const byAge =
ageFilter === "" || Number(a.age) >= Number(ageFilter);
Y la uni al resto:
return byType && byStatus && byQuery && byAge;

Visualmente que cambio?
.Aparecio nuevo campo de filtro al lado de los controles anteriores
.Al escribir una edad, la lista automaticamente muestra solo los animales con esa edad o mas

Como afecta al renderizado?
.El estado ageFilter cambia, react vuelve a ejecutar el filtrado, react vuelve a renderizar solo los animales
que cumplen la edad minima.

