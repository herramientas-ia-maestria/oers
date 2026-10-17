# Guía práctica: GitHub, Git Bash y entorno virtual para Pandas

**Módulo:** Herramientas para Inteligencia Artificial  
**Sistema operativo:** Windows 10 u 11  
**Python:** 3.14 instalado y funcionando correctamente  
**Herramientas:** navegador, Git Bash y **CMD o PowerShell**  
**Repositorio original:** https://github.com/herramientas-ia-maestria/1.2.1_1Pandas  
**Nombre del entorno virtual:** `env_pandas`

## Objetivo

Al finalizar estos pasos, usted deberá haber realizado un **fork** del repositorio de la práctica en GitHub, haberlo clonado en su computador, creado un entorno virtual **fuera del repositorio**, instalado las bibliotecas de Python y abierto el material en JupyterLab.

> **Antes de empezar:** confirme que dispone de una cuenta de GitHub, Git Bash y Python 3.14. Se asume que funcionan correctamente. El repositorio original es **https://github.com/herramientas-ia-maestria/1.2.1_1Pandas**.

## 1. Comprender la organización de carpetas

En esta práctica, el repositorio y el entorno son **carpetas hermanas**. No coloque `env_pandas` dentro de `1.2.1_1Pandas`.

```text
Documentos/
└── clases-python/
    ├── 1.2.1_1Pandas/       ← repositorio clonado desde GitHub
    │   ├── ...              ← notebooks y archivos del repositorio
    │   └── ...
    └── env_pandas/          ← entorno virtual; NO subir a GitHub
```

**¿Por qué separarlos?** El repositorio contiene los archivos de trabajo; el entorno contiene un intérprete y las bibliotecas necesarias. El entorno puede recrearse y no debe versionarse en Git.

## 2. Hacer un fork en GitHub

El **fork** crea una copia del repositorio en su propia cuenta de GitHub.

1. Abra el repositorio original: **[herramientas-ia-maestria/1.2.1_1Pandas](https://github.com/herramientas-ia-maestria/1.2.1_1Pandas)**.
2. Inicie sesión en GitHub.
3. Pulse **Fork**, en la parte superior de la página.
4. Elija su cuenta como propietario (*Owner*); conserve el nombre `1.2.1_1Pandas`.
5. Pulse **Create fork** y espere a que termine.
6. Compruebe que ahora está viendo el repositorio bajo **su usuario**, por ejemplo: `https://github.com/SU_USUARIO/1.2.1_1Pandas`.

> **Atención:** hacer *fork* no descarga los archivos a su computador. Ese es el siguiente paso.

## 3. Clonar el fork con Git Bash

1. En **su fork** de GitHub, pulse **Code** → **HTTPS** → **Copy URL**.
2. Abra **Git Bash**.
3. Prepare una carpeta para los materiales y acceda a ella:

```bash
cd ~/Documents
mkdir -p clases-python
cd clases-python
```

> Si Documentos se encuentra dentro de OneDrive o en otra ubicación, utilice la ruta que realmente corresponda en su equipo. También puede abrir esa carpeta con el Explorador de archivos y elegir **Open Git Bash here**, si la opción está disponible.

4. Escriba `git clone`, agregue un espacio y **pegue la URL HTTPS de su propio fork**. Por ejemplo:

```bash
git clone https://github.com/SU_USUARIO/1.2.1_1Pandas.git
```

**Sustituya `SU_USUARIO` por su usuario real.** No copie literalmente el ejemplo si su URL es diferente.

5. Ingrese a la carpeta descargada, **MUY IMPORTANTE**:

```bash
cd 1.2.1_1Pandas
```

6. Verifique que Git reconoce el repositorio:

```bash
git status
git remote -v
```

La dirección `origin` debe apuntar a **su fork**, no al repositorio original del docente. En el Explorador de archivos debe aparecer la carpeta `1.2.1_1Pandas`.

## 4. Crear el entorno `env_pandas` fuera del repositorio

**A partir de aquí utilice CMD o PowerShell; no necesita seguir en Git Bash.** Abra una de estas consolas y seleccione **una sola alternativa**.

### Opción A. CMD (Símbolo del sistema)

Entre en la carpeta **padre** `clases-python`:

```bat
cd /d "%USERPROFILE%\Documents\clases-python"
```

Cree el entorno, como carpeta hermana de `1.2.1_1Pandas`:

```bat
py -3.14 -m venv env_pandas
```

Si `py` no está disponible, pero `python --version` muestra Python 3.14, utilice:

```bat
python -m venv env_pandas
```

### Opción B. PowerShell

Entre en la carpeta **padre** `clases-python`:

```powershell
Set-Location "$HOME\Documents\clases-python"
```

Cree el entorno:

```powershell
py -3.14 -m venv env_pandas
```

Alternativa, si `py` no está disponible y `python` corresponde a 3.14:

```powershell
python -m venv env_pandas
```

**Importante:** el entorno se crea **una sola vez**. Cuando vuelva a trabajar otro día, deberá activarlo, no crearlo nuevamente.

## 5. Activar el entorno

Desde `clases-python`, utilice el comando que corresponda a su consola.

### CMD

```bat
env_pandas\Scripts\activate.bat
```

### PowerShell

```powershell
.\env_pandas\Scripts\Activate.ps1
```

Si PowerShell bloquea la activación, puede habilitar la ejecución **solo en la consola actual** y volver a intentar:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\env_pandas\Scripts\Activate.ps1
```

Debe aparecer un prefijo similar a:

```text
(env_pandas) C:\Users\Estudiante\Documents\clases-python>
```

Ese prefijo indica que **el entorno está activado**.

## 6. Entrar al repositorio e instalar las bibliotecas

Con el entorno activado, ingrese a la carpeta clonada.

**En CMD:**

```bat
cd 1.2.1_1Pandas
```

**En PowerShell:**

```powershell
Set-Location .\1.2.1_1Pandas
```

Primero, compruebe que está utilizando Python 3.14 y el entorno esperado:

```bat
python --version
python -m pip --version
```

Después, actualice `pip`:

```bat
python -m pip install --upgrade pip
```

**Si el repositorio contiene `requirements.txt`**, instale las dependencias indicadas en él:

```bat
python -m pip install -r requirements.txt
```

**Si el repositorio NO incluye `requirements.txt`**, instale al menos las herramientas necesarias para la práctica de Pandas y JupyterLab:

```bat
python -m pip install pandas matplotlib jupyterlab ipykernel
```

> El archivo `requirements.txt` depende del contenido real del repositorio. No se presupone que exista. Si alguna biblioteca falla al instalarse, revise su compatibilidad específica con Python 3.14 y el mensaje de error; no es necesariamente un fallo del entorno virtual.

Para comprobar la instalación:

```bat
python -m pip list
```

## 7. Iniciar JupyterLab

Mantenga **el entorno `env_pandas` activado** y asegúrese de encontrarse **dentro del repositorio `1.2.1_1Pandas`**.

En **CMD o PowerShell**:

```bat
python -m jupyterlab
```

Se abrirá JupyterLab en el navegador o aparecerá una dirección local para acceder. Abra el notebook de la práctica y ejecute sus celdas.

Puede comprobar que el kernel utiliza el intérprete esperado con una celda de Python:

```python
import sys
print(sys.executable)
```

La ruta mostrada debe corresponder a `env_pandas`.

> Para detener JupyterLab, vuelva a la consola donde quedó ejecutándose y presione **Ctrl + C**. Cerrar solo la pestaña del navegador no necesariamente detiene el servidor.

## 8. Desactivar el entorno

Después de cerrar JupyterLab, ejecute en CMD o PowerShell:

```bat
deactivate
```

Esto **no borra** el entorno ni las bibliotecas instaladas.

## 9. Volver a trabajar otro día

No repita `git clone` ni cree de nuevo el entorno. Solo actívelo, ingrese al repositorio y levante JupyterLab.

### CMD

```bat
cd /d "%USERPROFILE%\Documents\clases-python"
env_pandas\Scripts\activate.bat
cd 1.2.1_1Pandas
python -m jupyterlab
```

### PowerShell

```powershell
Set-Location "$HOME\Documents\clases-python"
.\env_pandas\Scripts\Activate.ps1
Set-Location .\1.2.1_1Pandas
python -m jupyterlab
```

## 10. Si realiza cambios en el repositorio (opcional)

Para enviar sus archivos a **su fork**, cierre primero JupyterLab si ya terminó de trabajar. Desde **Git Bash**, dentro de `1.2.1_1Pandas`, puede utilizar:

```bash
git status
git add .
git commit -a -m "Desarrollo de practica Pandas"
git push origin main
```

> No agregue al repositorio información confidencial, conjuntos de datos sensibles ni archivos temporales innecesarios. **`env_pandas` permanece fuera del repositorio**, por lo que no debería aparecer en los cambios de Git.

## 11. Problemas frecuentes

| Situación | Qué revisar |
|---|---|
| `git` no se reconoce | Abra **Git Bash** y compruebe `git --version`. |
| Clonó el repositorio original y no su fork | Verifique `git remote -v`; la URL `origin` debe corresponder a su cuenta. |
| Ya existe `1.2.1_1Pandas` | No repita `git clone` en la misma ubicación; ingrese en la carpeta existente. |
| `py` no está disponible | Compruebe `python --version`; si muestra 3.14, utilice `python -m venv env_pandas`. |
| El entorno apareció dentro del repositorio | Elimínelo únicamente si no contiene trabajo propio y recréelo desde la carpeta **padre** `clases-python`. |
| PowerShell no permite activar | Utilice la configuración temporal de la sección 5 o active con CMD. |
| `requirements.txt` no se encuentra | Compruebe si existe realmente y si está situado dentro de `1.2.1_1Pandas`. |
| `ModuleNotFoundError` | Active `env_pandas`, instale la biblioteca en ese entorno y compruebe el kernel de Jupyter. |
| Jupyter abre archivos de otra carpeta | Deténgalo e inícielo desde `1.2.1_1Pandas`. |
| Una biblioteca no se instala | Revise la compatibilidad de la versión del paquete con Python 3.14. |

## 12. Resumen rápido

| Acción | Herramienta | Comando o procedimiento |
|---|---|---|
| Crear copia en GitHub | Navegador | **Fork** → **Create fork** |
| Descargar su copia | Git Bash | `git clone URL_DE_SU_FORK` |
| Crear entorno | CMD/PowerShell desde `clases-python` | `py -3.14 -m venv env_pandas` |
| Activar | CMD | `env_pandas\Scripts\activate.bat` |
| Activar | PowerShell | `.\env_pandas\Scripts\Activate.ps1` |
| Entrar al proyecto | CMD/PowerShell | `cd 1.2.1_1Pandas` |
| Instalar paquetes | CMD/PowerShell | `python -m pip install -r requirements.txt` (si existe) |
| Iniciar JupyterLab | CMD/PowerShell | `python -m jupyterlab` |
| Detener JupyterLab | CMD/PowerShell | `Ctrl + C` |
| Desactivar entorno | CMD/PowerShell | `deactivate` |
