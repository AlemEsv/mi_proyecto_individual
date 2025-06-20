## Instalación

```bash
git clone --recurse-submodules https://github.com/AldoLunaBueno/pc3-grupo4-tema3.git
```

## Sprint 1

[Link Video del Sprint_1-Grupo3](https://drive.google.com/file/d/1ZWNHv99Dbc8p1jF8iGqgm0_ftpk_M3Xp/view?usp=sharing)

## Archivo `main.sh`

Archivo que automatiza la ejecución de todo el proyecto, dentro de sus funciones está lo siguiente:

* Si es ejecutado por primera vez:

  * Crea y activa el entorno virtual `.venv`.
  * Instala las dependencias.
  * Activa los hooks dentro de `git-hooks/`.

* Desde la segunda ejecución:

  * Acciona el patrón puesto.
  * limpia el estado.

```bash
cd scripts
source ./main.sh --pattern <nombre-patrón>
```

## Herramientas usadas

### 1. flake8, bandit

* **flake8**: Verifica código en Python por incorrecta sintáxis y malas prácticas.
* **bandit**: Analisa código en Python por posibles errores de seguridad.

```bash
flake8 -r scripts/
bandit -r scripts/
```

### 2. Pytest

Framework de pruebas para python, usado para asegurar buenas pruebas en los scripts `verify_state.py`, `generate_documentation.py`, `generate_diagram.py`, `etc`.

## Sprint 2

## Scripts generales

### 1. `generate_diagram.py`

Genera diagramas para cada módulo.

### 2. `generate_documentation.py`

Genera la documentación de cada patrón de diseño **(singleton, composite, builder, prototype y factory)**.

* Está dividido de la siguiente forma:

```bash
  <Titulo>
  <Índice>
  <Descripción-breve>
  <Variables>
  <Outputs>
  <Ejecución-ejemplo>
```

### 3. `verify_ia_docs.py`

Script que usa una lista de frases genéricas para verificar el porcentaje de texto copiado de páginas web, articulos, etc.

### 4. `verify_state.py`

Script que genera un archivo **.json** para mostrar el estado de cada módulo.

> Más información de los
> scripts en los comentarios de cada código: [Ver carpeta scripts](./scripts/)

## Sprint 3

## Patrones de diseño

### Singleton

Este módulo se encarga de la creación de una instancia única de un recurso, esta puede ser llamada desde diferentes módulos (**globalizada**) y solo puede instanciarse una vez durante el ciclo de vida de la infraestructura.

#### Ejecución

```bash
cd scripts # en carpeta raiz
# Llamado al módulo singleton
./main.sh --pattern singleton
```

#### Pruebas de integración

```bash
cd iac_patterns/singleton/scripts
./test_module_singleton.sh
```

#### 1. `variables.tf`

Define las variables de entrada para la generación del recurso.

* `instance_name`: nombre de la instancia.

* `instance_type`: tipo de instancia.

* `instance_enabled`: variable booleana que revisa si la instancia está o no habilitada.

#### 2. `main.tf`

Ejecuta un script para controlar la creación de la instancia.

* Crea un recurso nulo que **representará** la creación de una **instancia**.
* Acciona triggers:
  * por cada variable (`instance_name` e `instance_type`) revisa cambios para accionar el trigger.
  * Crea un `tag` para asegurar la existencia del lock cada que se accione el script `test_module_singleton.sh`
* Ejecuta el script `singleton.sh` dentro de un provisioner generando un `instance.lock`.

#### 3. `outputs.tf`

* `create_instance` muestra si la instancia está **habilitada** o **deshabilitada**.

* `singleton_status` muestra el el estado de creación del módulo.

#### Scripts

#### 1. `singleton.sh`

Script en bash que crea un archivo lock para asegurar una única instancia creada.

* `LOCK_FILE` evita la creación de múltiples instancias simultaneas.
* `PID_FILE` guarda el PID del proceso actual.
  * Si este `PID` ya existe, ejecuta un mensaje de instancia existente.
  * Si no existe el `lock`, lo crea y muestra su creación.
* Limpia el `PID` al finalizar la ejecución del script.

#### 2. Pruebas de integración: `test_module_singleton.sh`

* Verifica la creación de `singleton.lock`.

* Verifica que el `output` se ejecute correctamente.

### Prototype

Este módulo genera archivos de infraestructura a base de una plantilla modificable (`example.tf`), y ejecuta el script `clone_prototype (count = n)` para crear **N** clones a base de dicha plantilla con pequeñas modificaciones en su estructura.

#### Ejecución

```bash
cd scripts # en carpeta raiz
# Llamado al módulo prototype
./main.sh --pattern prototype
```

#### Pruebas de integración

```bash
cd iac_patterns/prototype/scripts
./test_module_prototype.sh
```

#### 1. `variables.tf`

Define las variables de entrada para la generación del archivo principal de la creación del prototypo.

* `name`: nombre del recurso creador del prototipo

* env`: variable de ejemplo para denotar un entorno dentro del recurso.

#### 2. `main.tf`

* `create_prototype`: mensaje de creación del clón a base de la plantilla dada.

* Se configura los **providers** necesarios para trabajar con archivos locales, plantillas, archivos nulos y aleatorios.

* Con un local_file procesa la plantilla y la guarda en un archivo `example.tf`.

* Cambia el contenido de la plantilla (`env` y `name`) para generar archivos .

#### 3. `outputs.tf`

* `create_prototype`: mensaje de creación del clón a base de la plantilla dada.

#### Scripts

##### 1. `clone_prototype.py`

Script hecho para crear **N** clones a base de la plantilla `prototype.hcl.tpl`, como ejemplo se tiene la creación de solo 3 clones.

##### 2. `test_module_prototype.sh`

* Valida la correcta creación de la infraestructura.

* Revisa que los outputs sean los correctos.

* pasa las pruebas de sintaxis para terraform(`tflint`)