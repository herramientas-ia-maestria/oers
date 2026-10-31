# Kaggle CLI: crear y actualizar datasets

Guía para ejecutar desde un termina/CMD, dentro de una **carpeta independiente** que contendrá los archivos del dataset. No requiere Git ni un repositorio de GitHub.

## Bloque 1. Crear un dataset nuevo

La carpeta debe contener el archivo que desea publicar, por ejemplo `ventas.csv`.

```bash
# Instalar Kaggle CLI (una sola vez, en el entorno Python que uses), dentro de un entorno virtual
python -m pip install kaggle

# Iniciar sesión en Kaggle (una sola vez, o cuando sea necesario)
kaggle auth login

# Crear el archivo dataset-metadata.json en la carpeta actual
kaggle datasets init -p .

# Agregar el dataset
Agregar el dataset en la carpeta

# Editar los metadatos
abrir el archivo dataset-metadata.json

# Publicar como dataset público
kaggle datasets create -p . --public

# Comprobar el estado (reemplaza TU_USUARIO)
kaggle datasets status TU_USUARIO/ventas-comerciales-peru
```

**Ejemplo de `dataset-metadata.json`:**

```json
{
  "title": "Ventas comerciales de Peru - Datos sinteticos",
  "id": "TU_USUARIO/ventas",
  "licenses": [
    {"name": "CC0-1.0"}
  ]
}
```

Reemplaza `TU_USUARIO` por tu usuario de Kaggle. Publica únicamente datos que tengas permiso para compartir.

## Bloque 2. Actualizar un dataset existente (crear una nueva versión)

Sustituye o modifica el CSV **en la misma carpeta**, conservando `dataset-metadata.json` y el identificador del dataset. Si quieres que el notebook siga leyendo el mismo nombre, conserva también el nombre del CSV.

```bash
# Revisar los archivos de la carpeta actual
ls -lh en Linux o Mac / dir en Windows

# Publicar una nueva versión con los archivos actualizados
kaggle datasets version -p . -m "Ampliación a 100000 registros"

# Comprobar el estado de publicación
kaggle datasets status TU_USUARIO/ventas-comerciales-peru

# Consultar información detallada, incluida la versión actual
kaggle datasets status TU_USUARIO/ventas-comerciales-peru --format json
```

**Importante:** para actualizar, usa `version`

### Referencia oficial

- [Documentación de Kaggle CLI para datasets](https://github.com/Kaggle/kaggle-cli/blob/main/docs/datasets.md)
- [Autenticación de Kaggle CLI](https://github.com/Kaggle/kaggle-cli/blob/main/skills/references/auth.md)
