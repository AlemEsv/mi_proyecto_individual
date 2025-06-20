# Diseño y compartición de módulos IaC con patrones de software

Alumno: Cinver Alem Espinoza Valera
Código: 20220277F

Link al repositorio: <https://github.com/AldoLunaBueno/pc3-grupo4-tema3>

Fui encargado de hacer la lógica inicial de los módulos de terraform, más en concreto la lógica total de los módulos **Singleton** y **Prototype** e hice la implementación de los scripts `generate_documentation.py`, `verify_ia_docs.py` y `main.sh`.

## Instrucciones de instalación

```bash
git clone https://github.com/AlemEsv/mi_proyecto_individual.git
cd mi_proyecto_individual
python3 -m venv .venv
# en windows
source .venv/Scripts/activate
# en linux 
source .venv/bin/activate
pip install -r requirements.txt
```

## Ejecución de scripts

- **Ejecución de scripts generales**

```bash
cd scripts_generales/scripts
# 1. generar documentación
python generate_documentation.py
# 2. verificar documentación
python verify_ia_docs.py
```

- **Ejecución de módulo singleton**

```bash
cd scripts_generales/iac_patterns/singleton
# 1. generar módulo Singleton
terraform init
terraform apply -auto-approve
cd scripts
# 2. Verificar módulo
./test_module_singleton.sh
```

- **Ejecución de módulo Prototype**

```bash
cd scripts_generales/iac_patterns/prototype
# 1. generar módulo Prototype
terraform init
terraform apply -auto-approve
cd scripts
# 2. Verificar módulo
./test_module_prototype.sh
```

- **Ejecución de pruebas**

```bash
cd scripts_generales/tests

# Verificación de documentos con texto genérico
pytest test_verify_ia_docs.py

# Verificación de generador de estado de infraestructura
pytest test_verify_state.py

# Verificación de diagrama generado
# nota: no creé el script generate_diagram.py así que no lo puse,
#       por lo que dará error al ejecutar test_generate_diagram
pytest test_generate_diagram.py
```
