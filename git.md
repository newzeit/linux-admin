# Chuleta de Git

Guía rápida de comandos básicos de Git para el control de versiones.

## Configuración Inicial
Configura tu identidad para que Git sepa quién firma los commits.

```bash
# Configurar nombre de usuario
git config --global user.name "Tu Nombre"

# Configurar correo electrónico
git config --global user.email "tu@email.com"

# Ver configuración actual
git config --list
```

## Crear un Repositorio
Inicia un nuevo repositorio local o descarga uno existente.

```bash
# Inicializar un repositorio en la carpeta actual
git init

# Clonar un repositorio remoto
git clone <url-del-repositorio>
```

## Flujo de Trabajo Básico (Snapshots)
Añadir cambios, guardarlos y revisar el estado.

```bash
# Ver el estado de los archivos (modificados, nuevos, staged)
git status

# Añadir un archivo específico al área de preparación (stage)
git add <archivo>

# Añadir todos los cambios al área de preparación
git add .

# Guardar los cambios preparados con un mensaje descriptivo
git commit -m "Mensaje descriptivo del cambio"

# Ver el historial de commits
git log --oneline --graph --all
```

## Ramas (Branching)
Las ramas permiten trabajar en diferentes funcionalidades de forma aislada.

```bash
# Listar ramas locales
git branch

# Crear una nueva rama
git branch <nombre-de-la-rama>

# Cambiar a una rama específica
git checkout <nombre-de-la-rama>

# Crear y cambiar a una rama nueva en un solo paso
git checkout -b <nueva-rama>

# Fusionar una rama con la rama actual (ej. fusionar 'feature' en 'main')
git merge <nombre-de-la-rama>

# Borrar una rama
git branch -d <nombre-de-la-rama>
```

## Repositorios Remotos
Sincroniza tus cambios con servidores como GitHub, GitLab o Bitbucket.

```bash
# Añadir un repositorio remoto
git remote add origin <url-del-repositorio>

# Enviar cambios al repositorio remoto (rama main)
git push origin main

# Descargar y fusionar los cambios del remoto
git pull origin main

# Ver los remotos configurados
git remote -v
```

## Inspección y Comparación
Revisa qué ha cambiado exactamente.

```bash
# Ver diferencias en archivos que no han sido añadidos al stage
git diff

# Ver diferencias en archivos que ya están en el stage
git diff --staged

# Ver detalles de un commit específico
git show <hash-del-commit>
```

## Deshacer Cambios
*Cuidado: algunos de estos comandos pueden sobrescribir trabajo.*

```bash
# Descartar cambios en un archivo (volver al último commit)
git checkout -- <archivo>

# Quitar un archivo del área de preparación (unstage)
git reset HEAD <archivo>

# Corregir el último commit (añadir olvidos o cambiar mensaje)
git commit --amend -m "Nuevo mensaje"
```
