# GIT

## Introducción

### Primero pasos con git-core

En cualquier momento es posible obtener informacion (o manual) de cada comando y su modo de empleo:

```bash
# git help <comando>

git help init
git help commit
git help add
git help remote

# git <comando> --help

git init --help
git commit --help
git add --help
git remote --help
```

#### Configuraciones básicas

`git config`

Configuracion básica en el entorno. Está configuracion se aplica de forma global (`--global`) pero siempre existe la posibilidad de definir valores locales a cada repositorio (`--local`):

```bash
# git config [--global | --local] key_config value
# git config [--global | --local] key_config=value

git config --global user.name "Desarrollador Humano"  # definiendo nombre de usuario 
git config --global user.email "correo@example.com"   # definiendo correo


git config --global init.defaultBranch main           # define la rama por defecto
git config --global core.editor vim                   # define el editor de texto por defecto (ej. realizar commit's)
```

Listando la configuración:

```bash
git config --list
```

#### Iniciando un nuevo repositorio local

`git init`

Para comenzar un nuevo repositorio es necesario iniciar el espacio de trabajo .git:

```bash
# git init [directorio]

git init ./example-project
```

### Manejo básico de repositorios

`git status`

La herramienta principal para determinar qué archivos están en qué estado es el comando **git status**.

```bash
git status

# On branch main
# No commits yet
# 
# nothing to commit (create/copy files and use "git add" to track)
```

```bash
# git status -s

git status -s

#  M README
#  M index.html
# MM Rakefile
# A  lib/git.rb
# M  lib/simplegit.rb
# ?? LICENSE.txt
```

La forma abreviada con `-s` permite listar los cambios en el directorio de trabajo.  El estado aparece en dos columnas al inicio de cada linea: la columna de la izquierda indica el estado preparado y la columna de la derecha indica el estado sin preparar.

`git add`

Permite cambios del directorio de trabajo al area de **staging**. Esto permite preparar los cambios para ser registrados en el repositorio (mediente *git commit*)

```bash
# git add [path_archivo_o_directorio | COMODIN(*) | COMODIN(.) ]

git add index.html
```

`git rm`

Eliminar archivos desde el arbol de indicex. Esto provoca que el archivo no vuelva a ser trackeado

```bash
# git rm <path_archivo>

git rm Readme.md
```

Elimina archivos desde el area de preparación (staging)

```bash
# git rm --cache <path_archivo>

git rm --cache Readme.md

# Otra opcion : git restore --staged <path_archivo>
# revisar uso de comando "git restore"
```

`git commit`

Confirmar cambios que se encuentran listos para registrar en arbol

```bash
# git commit

git status 
# On branch main
# No commits yet
# 
# Changes to be committed:
#   (use "git rm --cached <file>..." to unstage)
#         new file:   index.html
# 
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#         Readme.md

git commit
```

El comando anterior abre el editor de texto por defecto definido en la configuracion y permite registrar el mensaje de commit de forma mas completa.

Al finalizar los cambios en el editor y guardar el *commit* se registra en el arbor de indices.

```bash
# git commit -m "mensaje_COMMIT"

git commit -m "Iniciando repositorio, agregando un archivo..."
```

Con el flag `-m` podemos enviar el mensaje "in-line" sobre el comando.

```bash
# git commit -a -m "mensaje_COMMIT"

git commit -a -m "Iniciando repositorio, agregando un archivo..."
```

Con el flag `-a` permitimos al comando agregar, en un solo paso, las modificaciones pendientes en el directorio de trabajo al area de preparacion (staging)

`git log`

Para visualizar el arbol de cambios (*log*) podemos emplear este comando, el cual proporciona una salida genérica de la información de los registros:

```bash
# git log [-n_commits]

git log

# commit 32ce63fe8c122234e6a87ea6480988b59bad6d94 (HEAD -> main)
# Author: Oscar Marquez Olvera <oscar.marq.olv@gmail.com>
# Date:   Fri Aug 18 16:19:45 2023 -0600
# 
#     Creando archivo `.gitignore`
# 
#      Changes to be committed:
#             new file:   .gitignore
# 
# commit 17fe19b4efd51be6f5e71d001407bd77a81817e1
# Author: Oscar Marquez Olvera <oscar.marq.olv@gmail.com>
# Date:   Fri Aug 18 16:17:11 2023 -0600
# 
#     Agregando todos los cambios pendientes...
# 
#      Changes to be committed:
# ...
```

```bash
# git log -p [-n_commits]

git log -p -1
```

Muestra los cambios aceptados en cada entrada del registro

```bash
# git log --stat [-n_commits]

git log --stat -2
```

```bash
# git log --graph [-n_commits]

git log --graph
```

```bash
# git log --pretty=<formato> --abbrev-commit

git log --pretty=oneline --abbrev-commit
```

| Opcion | Valor |
| ----- | ----- |
| %H | Hash de la confirmación |
| %h | Hash de la confirmación abreviado |
| %T | Hash del árbol |
| %t | Hash del árbol abreviado |
| %P | Hashes de las confirmaciones padre |
| %p | Hashes de las confirmaciones padre abreviados |
| %an | Nombre del autor |
| %ae | Dirección de correo del autor |
| %ad | Fecha de autoría (el formato respeta la opción -–date) |
| %ar | Fecha de autoría, relativa |
| %cn | Nombre del confirmador |
| %ce | Dirección de correo del confirmador |
| %cd | Fecha de confirmación |
| %cr | Fecha de confirmación, relativa |
| %s | Asunto |

```bash
# ejemplos avanzados de presentacion...

git log --graph --pretty=format:"%h %s" --all

git log --graph --pretty=oneline --abbrev-commit --all

git log --all --graph --pretty="%C(yellow) %h %C(blue) %ad %C(red) %s " --date=human
```

`git rm`

Elimina un archivo del repositorio, pero el archivo sigue existiendo

`git restore`

Elimina un archivo desde el area de preparacion y mantiene los cambios

`git reset`

Regresa un archivo a un estado anterior (pero perdiendo todos su cambios posteriores)

`git checkout`

Con archivos: me permite despreciar los ultimos cambios hasta el ultimo punto en el
