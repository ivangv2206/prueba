# Política de Seguridad del Repositorio

## 1. Exclusión de Archivos Sensibles (.gitignore)
Para garantizar la seguridad del repositorio, se ha configurado un archivo `.gitignore` que excluye de forma automática los siguientes tipos de archivos:
*   **Archivos de entorno y credenciales (`.env`, `config.local.php`):** Contienen contraseñas de bases de datos y tokens de APIs. Si se subieran al control de versiones, cualquier persona con acceso al código podría comprometer los servidores.
*   **Dependencias y Binarios (`node_modules/`, `vendor/`, `*.exe`):** No se suben porque aumentan innecesariamente el tamaño del repositorio. Las dependencias deben instalarse en cada entorno mediante el gestor de paquetes correspondiente (npm, composer, etc.).
*   **Archivos temporales y logs (`*.log`):** Contienen datos de la ejecución local que no son útiles para el resto del equipo y podrían llegar a registrar información sensible del usuario de la máquina.

## 2. Protección de la Documentación y el Código
Para mantener la integridad del código fuente y la documentación, aplicamos las siguientes medidas:
*   **Ramas protegidas (Protected Branches):** La rama principal (`main` o `master`) está bloqueada para subidas directas (*push* directos). 
*   **Revisión de Pull Requests:** Todo cambio debe integrarse a través de un *Pull Request* (PR) y requiere al menos la revisión y aprobación de otro desarrollador antes de fusionarse.
*   **Principio de Menor Privilegio:** Los colaboradores solo reciben el nivel de acceso estrictamente necesario para su rol en el proyecto.

## 3. Plan de Recuperación ante Pérdida de Datos
En caso de errores graves (como el borrado accidental de una rama o un *commit* destructivo), el repositorio garantiza su recuperación mediante:
1.  **Uso de `git reflog`:** Permite rastrear los movimientos del puntero HEAD localmente para recuperar *commits* que aparentemente han sido borrados.
2.  **Reversión segura (`git revert`):** Si un error ya se ha subido a la rama principal, no se reescribe el historial (lo que causaría conflictos al resto del equipo), sino que se utiliza `git revert` para crear un nuevo *commit* que deshaga los cambios defectuosos.
3.  **Copias distribuidas:** Dado que Git es descentralizado, cada desarrollador tiene una copia local completa del historial. Si el repositorio remoto de GitHub sufriera un problema, cualquier miembro del equipo podría restaurarlo subiendo su versión local.
