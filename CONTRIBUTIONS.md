# Contribuciones de Cinver Espinoza Valera

## Sprint 1

- **2025-06-07**: Creé el directorio `iac/` con los modulos `singleton`, `factory`, `composite`, `prototype` y `builder` cada uno con una estructura básica en terraform: `main.tf`, `variables.tf` y `output.tf` simples.  
  - Commit: `feat(terraform): Creación de módulos iniciales para los patrones de diseño`  
  - Pull request: [#10](https://github.com/AldoLunaBueno/pc3-grupo4-tema3/pull/10)

- **2025-06-08**: Escribí `scripts/documentar_modulos.py` para generar documentación general para cada módulo. Este script escribe un archivo markdown con un titulo, descripción breve y el listado de variables que haya en la carpeta `iac/`
  - Commit: `feat(scripts): Agregar script que genera documentacion simple por patron`  
  - Pull request: [#13](https://github.com/AldoLunaBueno/pc3-grupo4-tema3/pull/13)

## Sprint 2

- **2025-06-11**: Cambio en el módulo **Singleton** por mal lectura de variables
  - Commit: `fix(terraform): Cambio en nombres de variables para los modulos`
  - Pull request: [#28](https://github.com/AldoLunaBueno/pc3-grupo4-tema3/pull/28)

- **2025-06-12**: Implementé la lógica para el módulo **Singleton**, mediante un script Bash que crea un lockfile para garantizar una única instancia global.

  - Commit: `feat(module): Modificar modulo singleton para añadir instancia unica`
  - Pull request: [#31](https://github.com/AldoLunaBueno/pc3-grupo4-tema3/pull/31)

- **2025-06-13**: Implementé la lógica para el modulo **Prototype**, genera un archivo `example.tf` a partir de una plantilla dentro de `templates/` y creé el script `clone_prototype.py` para crear más clones con diferencias mínimas.
  - Commit: `feat(module): Crear modulo prototype para tener clones a base de un tmpl`
  - Pull request: [#33](https://github.com/AldoLunaBueno/pc3-grupo4-tema3/pull/33)

- **2025-06-15**: Agregué una mejora en la lógica del script `generate_documentation.py` para que lea la descripción dentro de `./<module>/README`, implementación de ejemplo de invocación y outputs.
  - Commit: `feat(scripts): Script generador de documentos por patron con ejemplo`
  - Pull request: [#36](https://github.com/AldoLunaBueno/pc3-grupo4-tema3/pull/36)

- **2025-06-15**: Documenté en `README.md` las herramientas usadas en el proyecto y una descripción breve de **Singleton**
  - Commit: `docs(readme): Documentación de herramientas y uso de singleton`
  - Pull request: [#40](https://github.com/AldoLunaBueno/pc3-grupo4-tema3/pull/40)

- **2025-06-16**: Implementación de la lógica de `main.sh` para que invoque todos los módulos.
  - Commit: `feat(script): Mejora al script principal para que invoque cada modulo`
  - Pull request: [#42](https://github.com/AldoLunaBueno/pc3-grupo4-tema3/pull/42)

## Sprint 3

- **2025-06-16**: Escribí el script  `verificar_ia_docs.py` para revisar texto genérico en la documentación generada.
  - Commit: `feat(scripts): Script verificador de texto genérico en documentación.`  
  - Pull request: [#55](https://github.com/AldoLunaBueno/pc3-grupo4-tema3/pull/55)

- **2025-06-18**: Refiné el módulo **Singleton** agregando una variable de gestión de ciclo de vida(`instancia habilitada/deshabilitada`). Además, agregué el script `test_module_singleton.sh` para validar la creación y destrucción de la infraestructura.

  - Commit 1: `docs(readme): Instrucciones de ejecución y testeo de singleton`
  - Commit 2: `fix(module): Error al probar la creación del lock_file`  
  - Commit 3: `feat(module): Pruebas para la creación de instancia única en singleton`  
  - Pull request: [#57](https://github.com/AldoLunaBueno/pc3-grupo4-tema3/pull/57)
  
- **2025-06-19**: Refiné el módulo **Prototype** agregandole una nueva variable `random-pet`, modifiqué el template asociado para mejorar la lógica del módulo.
  - Commit 1: `feat(module): refinamiento de prototype, correccion de errores con apply`
  - Commit 2: `feat(test): Pruebas de creación de prototipo y validar outputs`
  - Pull request: [#47](https://github.com/AldoLunaBueno/pc3-grupo4-tema3/pull/59)