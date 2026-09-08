# RoxTurnos

Aplicación web sencilla para llevar el rol de turnos de fin de semana:
alta de empleados, asignación de turnos por fecha, registro de cambios
(intercambios de turno) y un panel con los fines de semana trabajados por
cada persona.

## Uso

App publicada en **GitHub Pages**: https://hebelmx.github.io/RoxTurnos/

- **Ver el rol:** abre el enlace e introduce la **contraseña**. Funciona en
  móvil y en computadora; los datos se sincronizan solos.
- **Editar:** además de la contraseña necesitas un **token de GitHub**
  (una sola vez por dispositivo, en *Ajustes*).

### Pestañas

| Pestaña | Para qué |
|---|---|
| **Panel** | Conteo de fines de semana y turnos por empleado, cambios cedidos/tomados, cambios pendientes. |
| **Turnos** | Agregar un fin de semana (eliges el sábado, el domingo se calcula) y marcar quién cubre cada turno. |
| **Cambios** | Registrar que alguien pasó su turno a otro compañero (con motivo y fecha). Se puede dejar pendiente para el futuro y aplicarlo después. |
| **Empleados** | Alta, edición, activar/desactivar. Los inactivos no aparecen para asignar pero conservan su historial. |
| **Ajustes** | Token de GitHub, cambio de contraseña, exportar CSV. |

## Cómo se guardan los datos

- El repositorio es **público** (requisito de GitHub Pages en el plan
  gratuito), pero los datos del rol se guardan **cifrados** (AES-GCM, clave
  derivada de la contraseña con PBKDF2) en `docs/data/roster.enc.json`.
- La **contraseña nunca** se sube al repositorio. Sin ella, el archivo es
  ilegible. Aun así, elige una contraseña larga y no obvia: quien encuentre
  el repo podría intentar adivinarla por fuerza bruta.
- El **token** solo se guarda en el navegador de cada dispositivo que
  edite. Usa un token *fine-grained* limitado a este repo con permiso
  **Contents: Read and write**.

### Crear el token de GitHub

1. GitHub → *Settings* → *Developer settings* → *Personal access tokens* →
   *Fine-grained tokens* → *Generate new token*.
2. *Repository access*: **Only select repositories** → `RoxTurnos`.
3. *Permissions* → *Repository permissions* → **Contents: Read and write**.
4. Genera, copia y pégalo en la app (*Ajustes* → *Token de GitHub*).

## Desarrollo

Todo es un solo archivo estático, `docs/index.html` (HTML + CSS + JS, sin
dependencias). Para probar en local:

```sh
python3 -m http.server -d docs 8000   # http://localhost:8000
```

Nota: la sincronización llama a la API de GitHub, así que en local también
necesitas la contraseña y, para guardar, el token.

## Otros archivos

- `RolTurnos.xlsx` — hoja de cálculo original (plantilla de la que salió
  este proyecto).
- `scripts/xlsx-textconv.py` — driver `textconv` de Git para diffs legibles
  de los `.xlsx` (ver `.gitattributes`).
