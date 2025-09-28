# Actividad 6: Introducción a Git - Conceptos básicos y operaciones esenciales

## Configuración inicial de Git

**Comando utilizado:** `git config --global user.name "AlesxanDer1102"` y `git config --global user.email "diego.orrego.t@uni.pe"`

Se configuró Git a nivel global con el usuario AlesxanDer1102 y email diego.orrego.t@uni.pe para identificar los commits.

## Inicialización del repositorio

**Comando utilizado:** `git init`

Se inicializó un nuevo repositorio Git en el directorio diego-repo, creando la estructura .git necesaria para el control de versiones.

## Operaciones básicas add/commit

**Comandos utilizados:** `git add` y `git commit -m "mensaje"`

Se realizaron múltiples commits para demostrar el flujo básico de preparación (staging) y confirmación de cambios. Se crearon archivos como README.md, CONTRIBUTING.md y main.py.

## Exploración del historial con log

**Comando utilizado:** `git log --oneline`

Se exploró el historial de commits utilizando diferentes variantes del comando git log para visualizar los cambios realizados en el proyecto.

## Trabajo con ramas (branch/checkout/merge)

**Comandos utilizados:** `git branch`, `git checkout`, `git merge`

Se crearon y gestionaron múltiples ramas para desarrollar características de forma aislada y posteriormente fusionarlas con la rama principal, incluyendo resolución de conflictos.

## Ejercicios completados

### Ejercicio 1: Manejo avanzado de ramas y resolución de conflictos
- Creación de rama feature/advanced-feature
- Desarrollo paralelo en main y feature
- Resolución manual de conflictos durante merge
- Eliminación de rama fusionada

### Ejercicio 2: Exploración y manipulación del historial de commits
- Uso de git log -p para ver diferencias detalladas
- Filtrado de commits por autor
- Ejecución de git revert para deshacer cambios
- Rebase interactivo para limpiar historial
- Visualización gráfica con git log --graph

### Ejercicio 3: Creación y gestión de ramas desde commits específicos
- Creación de rama bugfix/rollback-feature desde commit específico (2f8e1d4)
- Desarrollo de correcciones en la nueva rama
- Merge con resolución de conflictos add/add
- Visualización del historial integrado

### Ejercicio 4: Manipulación y restauración de commits
- Uso de git reset --hard HEAD~1 para deshacer commits
- Uso de git restore para deshacer cambios no confirmados
- Demostración de diferencias entre reset y restore

## Archivos de evidencia generados

Todos los archivos de logs se encuentran en el directorio `logs/`:

- **git-version.txt**: Salida de `git --version`
- **config.txt**: Salida de `git config --list`
- **init-status.txt**: Salida de `git init` + `git status` inicial
- **add-commit.txt**: Proceso de `git add` + `git commit`
- **log-oneline.txt**: Salida de `git log --oneline`
- **branches.txt**: Salida de `git branch -vv`
- **merge-o-conflicto.txt**: Proceso de merge y resolución de conflictos
- **revert.txt**: Documentación de ejercicios con git log y revert
- **rebase.txt**: Documentación de rebase interactivo y visualización gráfica
- **cherry-pick.txt**: Documentación de gestión de ramas desde commits específicos
- **stash.txt**: Documentación de manipulación y restauración de commits

## Comandos y conceptos demostrados

- **git config**: Configuración de usuario y email
- **git init**: Inicialización de repositorio
- **git add/commit**: Preparación y confirmación de cambios
- **git log**: Exploración del historial con múltiples opciones
- **git branch/checkout**: Creación y cambio entre ramas
- **git merge**: Fusión de ramas con resolución de conflictos
- **git revert**: Reversión de commits específicos
- **git rebase**: Reescritura del historial de commits
- **git reset**: Deshacimiento de commits
- **git restore**: Restauración de archivos modificados

## Sin remoto

Esta actividad se realizó completamente en repositorio local sin configurar remote/PR externos.

## Conclusiones

La actividad demostró exitosamente el manejo completo de Git, desde operaciones básicas hasta técnicas avanzadas de manipulación del historial y resolución de conflictos. Se documentaron todas las operaciones con evidencias concretas de su funcionamiento.