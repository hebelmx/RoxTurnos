# RoxTurnos

Rol de turnos de fin de semana.

## Contenido

- `RolTurnos.xlsx` — hoja de cálculo (`Sheet1`) con el rol de turnos. Una
  cuadrícula de asignación: las columnas son los tres turnos
  (**Sábado Matutino**, **Sábado Vespertino**, **Domingo Matutino**) y las
  filas los empleados (**Empleado 1** … **Empleado 17**). El bloque
  empleados × turnos se repite varias veces hacia abajo (una repetición por
  semana / periodo). Las celdas de asignación están vacías; es la plantilla.
  Creada con LibreOffice Calc.
- `scripts/xlsx-textconv.py` — driver `textconv` de Git para ver diffs
  legibles de los `.xlsx`.

## Diff legible de los `.xlsx`

`.gitattributes` marca los `.xlsx` como binarios para el merge y declara el
driver de diff `xlsx`. Actívalo una vez por clon:

```sh
git config diff.xlsx.textconv "python3 scripts/xlsx-textconv.py"
git config diff.xlsx.binary true
```

Requiere `openpyxl` (`pip install openpyxl`). Sin él, `git diff` simplemente
omite el contenido del workbook en vez de fallar.
