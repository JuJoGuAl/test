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
		- Con índice busco la celda que posea dicho índice (tr y td) y se activa la edición con setEditing.
- Metodo saveEditing: Salva la edición del selector siempre y cuando este sea del tipo td, y envia un evento a dropEditing(update=false) si valor anterior es diferente al valor actual update es True.
- Metodo dropEditing(update=false): Sale del modo de edición del selector tipo td, borrando los controles que fueron creados por setEditing, setea el nuevo valor del td y lanza un trigger updatesuccess al td, indicando un cambio de valor.
- Metodo setEditing: Convierte en editable la td, tomando como valor inicial el valor actual del td, se utiliza getValue para obtener su valor en función a la lógica del método, el nuevo objeto editable heredara todas las clases que posee el td
- Metodo getProp(prop): Obtiene la propiedad prop del Selector, si no existe retorna undefined.
- Metodo setProp(prop,val): Setea el valor (val) a la propiedad (prop) del selector si no existe retorna undefined, si existe retorna el objeto Comex Object
- Metodo initTable: Inicializa como grid una tabla, creando el objeto comexObject con las propiedades indicadas en cada th / tr.
- Metodo initColumna: Inicializa una columna de una tabla tomando las propiedades declaradas en ella y asignándolas al objeto comexObject, para luego buscar cada celda dentro de la columna e inicializarla con las mismas propiedades, las propiedades son:
	- Key: String Utilizada como la llave de la columna se usa como identificador de cada columna (debe ser único en una tabla), por defecto noSet.
	- AllowUpdate: Boolean Determina si la columna es editable o no, por defecto false.
	- Format: String Determina el formato a usar para columna (cabe destacar que ciertos Type determinan un formato).
	- ValueList: Array Arreglo de objetos que seran utilizados para llenar un DropList (select), para los casos donde Type sera DropDownList.
	- Type: String determina el tipo de dato que manejara la columna, los valores permitidos son (DropDownList, CheckBox, Text, Date, DateTime), por defecto Text, cabe destacar que ciertos Type determinan el tipo de dato de la columna:
		- CheckBox: se considera como Boolean el tipo de dato y solo se esperan datos True o False.
		- Date: se considera como Date / DateTime la columna, y espera datos dentro del formato yyyy-mm-dd o yyyy-mm-dd hh:MM:ss
		- DropDownList: Para este tipo de Columna se requiere un drop (select) en el DOM con los valores de dicha columna (ya que dicha columna solo recibirá un código y su respectivo valor debe de obtenerse de una lista de valores, dicho drop debe tener la propiedad DropDownList con el nombre de la tabla seguido del campo, por ejemplo: tabla_id.campo_key.
- Metodo initCell: Inicializa la celda td con los datos pre definidos de la columna th, siguiendo la lógica:
	- Si th Type es DropDownList toma el valor de la celda y lo busca en el drop tabla_id.columna_key, para obtener su texto y mostrarlo.
	- Si th Type es CheckBox, dibuja un checkbox utilizando el método setCheckBox, inactivo según el valor True o False.
	- Si th es Date formatea la fecha dd-mm-yyyy, quitando el fragmento de la hora si lo posee.
	- Si th es DateTime formatea la fecha dd-mm-yyyy hh:MM:ss, quitando el fragmento de los microsegundos.
- Metodo setCheckBox(checked=false,enable=true): Crea un checkbox con diseño y lo active según el valor de checked, y lo habilita según el valor de enable.
- Metodo initRow: Inicializa una row de una tabla tomando las propiedades declaradas en ella y asignándolas al objeto comexObject, las propiedades son:
	- Key: String Utilizada como la llave de la columna se usa como identificador de cada columna (debe ser único en una tabla), por defecto noSet.
- Metodo addRow: Agrega una row (tr) a una tabla inicializada previamente como grid, heredando de las columnas sus propiedades.



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

## [Proximos Cambios]
