# Changelog
Cambios realizados en el Proyecto Comex.

## [0.0.1] - 2022-07-01
### Añadido
- Se crea archivo LOG (CHANGELOG.md).
- Funcion clear_validations(): Toma todos los Objetos con las class is-invalid y / o is-valid y las remueve (para borrar diseño de validaciones rotas o cumplidas).
- Metodo getLabel: Retorna un String con el label del selector, si el selector no posee label retorna la propiedad name.
- Metodo valObj: Retorna un Boolean para indicar si el selector posee un valor distinto a vacío.
- Metodo valNumber(_positive = false): Retorna un Boolean para indicar si el selector posee un numero, recibe el parámetro _positive Boolean, que por defecto es false, si es seteado a true el numero debe ser mayor a 0.
- Metodo valDateTime: Retorna un Boolean para indicar si el selector posee una fecha / fecha hora valida.
- Metodo valTable: Retorna un Boolean para indicar si el selector posee al menos una row dentro de tbody, si el selector no es tabla retorna un error.
- Metodo valList: Retorna un Boolean para indicar si el selector posee un valor seleccionado distinto a -1 (se utiliza -1 para las opciones del tipo: SELECCIONE UN VALOR / SELECCIONE), si el selector no es select retorna un error.


### Changed
- Refer to a "change log" instead of a "CHANGELOG" throughout the site to
  differentiate between the file and the purpose of the file — the logging of
  changes.

### Removed
- Remove empty sections from CHANGELOG, they occupy too much space and create
  too much noise in the file. People will have to assume that the missing
  sections were intentionally left out because they contained no notable
  changes.

## [Unreleased]