# Actividad 5: Pipeline DevOps con Make y Bash - Parte 1
# Alumno: Orrego Torrejon Diego Alesxander
## Resumen del Entorno

- **Sistema Operativo**: Linux 6.6.87.2-microsoft-standard-WSL2
- **Shell**: Bash 5.1.16
- **Python**: Python 3.10.12
- **Make**: GNU Make 4.3
- **tar**: GNU tar (determinista con --sort, --mtime, --numeric-owner)
- **sha256sum**: GNU coreutils
- **Herramientas de lint**: shellcheck y shfmt no instalados en el entorno actual

## Parte 1 - Construir: Ejercicios y Respuestas

### Ejercicio 1: make help y .DEFAULT_GOAL

**Evidencia**: `logs/make-help.txt`

El comando `make help` muestra los targets disponibles con sus descripciones extraídas de los comentarios `##`. La directiva `.DEFAULT_GOAL := help` hace que al ejecutar `make` sin argumentos se muestre la ayuda automáticamente. `.PHONY` declara targets que no corresponden a archivos reales, evitando conflictos si existieran archivos con esos nombres y asegurando que siempre se ejecuten.

### Ejercicio 2: Generación e idempotencia de build

**Evidencias**: `logs/build-run1.txt`, `logs/build-run2.txt`, `evidencia/out-hello-run1.txt`

La primera corrida ejecuta `mkdir -p out` y `python3 src/hello.py > out/hello.txt`, generando el archivo target. La segunda corrida muestra "Nothing to be done for 'build'" porque Make compara timestamps: `out/hello.txt` es más reciente que `src/hello.py`, por lo que no necesita reconstruir. Esto demuestra la idempotencia del grafo de dependencias basado en marcas de tiempo.

### Ejercicio 3: Fallo controlado y .DELETE_ON_ERROR

**Evidencia**: `logs/fallo-python4.txt`

Al usar `PYTHON=python4` (inexistente), el shell falla con "command not found" debido a `-e` (exit on error). `.DELETE_ON_ERROR` elimina automáticamente `out/hello.txt` parcialmente creado, evitando artefactos corruptos. El modo estricto `-u` (unset variables) y `-o pipefail` aseguran detección temprana de errores y estados consistentes.

### Ejercicio 4: Dry-run y depuración detallada

**Evidencias**: `logs/dry-run-build.txt`, `logs/make-d.txt`

`make -n` muestra los comandos que se ejecutarían sin ejecutarlos realmente. `make -d` revela el razonamiento interno: Make considera cada archivo objetivo, verifica si existe, compara timestamps con dependencias, y decide si debe reconstruir. La línea "Must remake target" indica que el archivo no existe o está desactualizado respecto a sus dependencias.

### Ejercicio 5: Incrementalidad con marcas de tiempo

**Evidencias**: `logs/rebuild-after-touch-src.txt`, `logs/no-rebuild-after-touch-out.txt`

Tocar `src/hello.py` actualiza su timestamp, haciendo que sea más reciente que `out/hello.txt`, forzando reconstrucción. Tocar `out/hello.txt` lo hace más reciente que su dependencia, por lo que Make no ejecuta trabajo innecesario. Esto demuestra cómo Make optimiza builds basándose en el grafo de dependencias y timestamps del sistema de archivos.

### Ejercicio 6: Verificación de estilo manual

**Evidencias**: `logs/lint-shellcheck.txt`, `logs/format-shfmt.txt`

Las herramientas `shellcheck` y `shfmt` no están instaladas en el entorno actual. En un entorno de producción, `shellcheck` detectaría problemas de shell scripting (variables sin comillas, comandos peligrosos, portabilidad) y `shfmt` normalizaría el formato. Su ausencia no impide el funcionamiento pero reduce la calidad del código.

### Ejercicio 7: Paquete reproducible

**Evidencias**: `logs/sha256-1.txt`, `logs/sha256-2.txt`, `logs/sha256-diff.txt`

**Hash obtenido**: `a5c2d43a7f927dc0bfede333961e2552d889ce3a2fe52e72e427e09980ca57c2`

Ambos empaquetados produjeron el mismo hash SHA256, confirmando reproducibilidad 100%. Los flags `--sort=name` (orden alfabético), `--mtime=@0` (época Unix), `--owner=0 --group=0 --numeric-owner` (propietario normalizado) y `gzip -n` (sin timestamp) eliminan toda variabilidad no determinista, esencial para CI/CD y auditoría.

### Ejercicio 8: Error "missing separator"

**Evidencia**: `evidencia/missing-separator.txt`

Al reemplazar el TAB inicial por espacios en una receta, Make reporta "missing separator". Make requiere TAB (no espacios) al inicio de líneas de receta para distinguirlas de variables o targets. Este error se diagnostica viendo el número de línea en el mensaje y verificando la indentación con `cat -A` para mostrar caracteres invisibles.

## Conclusiones de la Parte 1

El Makefile implementado establece un entorno de construcción estricto y determinista mediante:
- Modo estricto del shell (`-eu -o pipefail`)
- Variables de entorno normalizadas (`LC_ALL=C`, `TZ=UTC`)
- Detección de errores (`.DELETE_ON_ERROR`, `--warn-undefined-variables`)
- Grafo de dependencias basado en timestamps para builds incrementales

El script Bash demuestra prácticas robustas: verificación de dependencias, manejo de errores con `trap`, y limpieza segura. El pipeline resultante es apto para entornos CI/CD por su determinismo y capacidad de detección temprana de problemas.

**Estado**: Parte 1 completada. Lista para commit y continuación con Parte 2.