# Changelog
Cambios realizados en el Proyecto Comex.

## [0.0.1] - 2022-07-01
### Añadido
- Se crea archivo LOG (CHANGELOG.md).
- Funcion clear_validations(): Toma todos los objetos con las class is-invalid y / o is-valid y las remueve (para borrar diseño de validaciones rotas o cumplidas).
- Metodo getLabel: Retorna un String con el label del selector, si el selector no posee label retorna la propiedad name.
- Metodo valObj: Retorna un Boolean para indicar si el selector posee un valor distinto a vacío.
- Metodo valNumber(_positive = false): Retorna un Boolean para indicar si el selector posee un numero, recibe el parámetro _positive Boolean, que por defecto es false, si es seteado a true el numero debe ser mayor a 0.
- Metodo valDateTime: Retorna un Boolean para indicar si el selector posee una fecha / fecha hora valida.
- Metodo valTable: Retorna un Boolean para indicar si el selector posee al menos una row dentro de tbody, si el selector no es tabla retorna un error.
- Metodo valList: Retorna un Boolean para indicar si el selector posee un valor seleccionado distinto a -1 (se utiliza -1 para las opciones del tipo: SELECCIONE UN VALOR / SELECCIONE), si el selector no es select retorna un error.
- Metodo valForm: Retorna un Boolean para indicar si todos los objetos dentro del selector con la class validar son validos, para ello sigue las siguientes reglas:
	- numeric: aplica la validación valNumber.
	- numeric positive: aplica la validación valNumber(true).
	- dates / datetimes: aplica la validación valDateTime.
	- table: aplica la validación valTable.
	- list: aplica la validación valList.
- Metodo setType: (Interno) Setea una class de ok o error, según el tipo de validación pasada.
- Metodo isPasswordValid: Retorna un Boolean para indicar si las contraseñas son validas y cumplen los parámetros minimos.
- Metodos getValue: Retorna un String con el valor del selector, siguiendo las siguientes instrucciones:
	- Si el selector es un input o select toma su valor, de lo contrario toma su texto
	- Si el selector posee la propiedad ComexValue, la captura.
	- Si el selector es un checkbox lee la propiedad checked (retorna true / false).
	- Si el selector es un td y dentro posee un checkbox se sigue la regla anterior.
- Metodo getKeyPressed(e): Determina la accion a seguir para la tecla presionada del selector, el selector debe ser del tipo td y recibe como parámetro evento (e), siguiendo la siguiente lógica:
	- Si tecla es ESC escapa de la edición.
	- Si tecla es ENTER o TAB, guarda la edición y pasa a la siguiente acción
	- Se detiene la propagación (disparada por ENTER para enviar el FORM)
	- Si Tecla es TAB se sigue con la siguiente lógica:
		- Si Tecla utilizo SHIFT busco el td anterior que sea editable y no sea un checkbox, para capturar su índice.
		- Si Tecla no utilizo SHIFT busco el td siguiente siguiendo la lógica anterior.
		- Si Indice es negativo busco la siguiente tr, o la anterior si tecla utilizo SHIFT.
		- Con índice busco la celda que posea dicho índice (tr y td) y se activa la edición con .setEditing.





### Changed
- Refer to a "change log" instead of a "CHANGELOG" throughout the site to
  differentiate between the file and the purpose of the file — the logging of
  changes.

### Removed
- Remove empty sections from CHANGELOG, they occupy too much space and create
  too much noise in the file. People will have to assume that the missing
  sections were intentionally left out because they contained no notable
  changes.

### Obsoleto
- Funcion convert(convert): (Interno) Retorna un String a partir de convert eliminando la etiqueta span.
- Funcion mensajeMVC(): (Sin Usar) Invoca la función dialog() pasando cada mensaje obtenido de validation_sumary.
- Funcion dialog(msj,class): (Sin Usar) Invoca toast pasando el msj y class para lanzar una alerta.

## [Unreleased]
