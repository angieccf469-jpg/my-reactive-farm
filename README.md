Activida #3

En esta actividad hize dos mejoras para mejorar la experiencia del usuario al crear un animal.

Mejora.1
Antes, el formulario permitia intentar enviar aunque faltaran datos.
Ahora agregue una validación basica que revisa cada campo:
.Si un campo esta vacio, se marca como error
.El formulario no se envia mientras existan errores
.El foco salta directamente al primer campo con error para ayudar al usuario

¿Porque mejora la experiencia?
.Evita errores accidentales
.El usuario sabe exactamente que debe completar
.Hace el formulario mas claro y profesional

Mejora.2
Agregue dos comportamientos:
.1.Desactivar boton si faltan campos 
disabled={isFormIncomplete || submitting}
.2.Mostrar estado de carga cuando se envia
{submitting ? "sunmitting...": "create"}
Y el boton cambia de estilo para verse apagado
className={
    isFormIncomplete || submitting
    ? "bg-gray-300 cursor-not-allowed"
    : "bg-blue-500 text-white hover:bg-blue-600"
}

¿Porque mejora la experiencia?
.Evita que el usuario presione varias veces el boton
.Deja claro cuando el formulario NO se puede enviar 
.Evita envios duplicados 
.Da retroalimentación visual

El formulario ahora es:
.Seguro
.Mas claro
.Mas facil de usar
.Mas profesional 
.Evita errores y envios duplicados 

Estas mejoras ayudan a que el usuario entienda en todo momento qué está pasando y qué debe hacer para completar correctamente el formulario.
