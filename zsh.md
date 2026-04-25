# Guía de Zsh (Z Shell)

Zsh es una shell potente diseñada para uso interactivo que extiende las funcionalidades de Bash, ofreciendo mejores funciones de autocompletado, personalización y manejo de errores.

## 1. Configuración Inicial

*   **Instalación**: `sudo dnf install zsh` (en Fedora/RHEL) o `sudo apt install zsh` (en Debian/Ubuntu).
*   **Cambiar shell por defecto**: `chsh -s $(which zsh)`.
*   **Archivo de configuración**: Todo se guarda en `~/.zshrc`.

## 2. Framework: Oh My Zsh

Es el framework más popular para gestionar la configuración de Zsh.
*   **Instalación**:
    ```bash
    sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
    ```

## 3. Características Clave

### Autocompletado Inteligente
*   Usa `Tab` para navegar por un menú interactivo de archivos o comandos.
*   Corrección automática de errores tipográficos menores (ej. `cd Descktop` -> `cd Desktop`).

### Navegación Rápida
*   No necesitas `cd` para entrar en carpetas (si está habilitado): simplemente escribe el nombre de la carpeta.
*   **Alias de directorio**: `..` (subir uno), `...` (subir dos), `....` (subir tres).

### Globbing Avanzado (Wildcards)
*   `ls **/*.js`: Busca todos los archivos `.js` de forma recursiva en todos los subdirectorios.
*   `ls file(.)`: Solo archivos regulares.
*   `ls folder(/)`: Solo directorios.

## 4. Plugins Recomendados

Para instalarlos en Oh My Zsh, añádelos a la línea `plugins=(...)` en tu `~/.zshrc`.

1.  **`git`**: Atajos rápidos (ej: `gst` para `git status`, `gp` para `git push`).
2.  **`zsh-autosuggestions`**: Sugiere comandos basados en tu historial mientras escribes (clonado aparte).
3.  **`zsh-syntax-highlighting`**: Colorea los comandos en tiempo real (verde si existen, rojo si no).

## 5. Temas (Personalización Visual)

El tema más usado es **Powerlevel10k** por su velocidad y capacidad de mostrar info de Git, batería, tiempo de ejecución, etc.

*   Cambia `ZSH_THEME="robbyrussell"` por `ZSH_THEME="powerlevel10k/powerlevel10k"` en el `.zshrc`.

## 6. Atajos de Teclado Útiles

*   `Ctrl + R`: Búsqueda incremental en el historial.
*   `Ctrl + A`: Ir al inicio de la línea.
*   `Ctrl + E`: Ir al final de la línea.
*   `Ctrl + U`: Borrar toda la línea.
*   `Ctrl + W`: Borrar la palabra anterior.

## 7. Ejemplo de Alias en .zshrc

```bash
alias zconf="nano ~/.zshrc"
alias reload="source ~/.zshrc"
alias ll="ls -lahF --color=auto"
alias ip="ip -c addr"
```

## 8. Historial Compartido
Zsh permite que todas las terminales abiertas compartan el mismo historial de comandos en tiempo real, lo cual es extremadamente útil para no perder comandos escritos en otras pestañas.
