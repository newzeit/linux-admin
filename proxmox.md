# 🛡️ Manual de Gestión y Rescate de Proxmox (CLI)

Este manual cubre los comandos esenciales para administrar Proxmox VE (PVE) directamente desde la terminal.

---

## 📊 1. Gestión de Máquinas Virtuales (VMs)
Proxmox utiliza el comando `qm` (Qemu Manager).

*   **Listar todas las VMs:** `qm list`
*   **Iniciar una VM:** `qm start <ID_VM>`
*   **Apagar una VM (limpio):** `qm shutdown <ID_VM>`
*   **Forzar apagado (reset):** `qm stop <ID_VM>`
*   **Ver configuración de una VM:** `qm config <ID_VM>`
*   **Cambiar RAM en caliente:** `qm set <ID_VM> -memory 4096`

---

## 📦 2. Backups y Restauración (vzdump)
Proxmox usa archivos `.vma` (a veces comprimidos como `.vma.zst`).

*   **Crear backup manual:**
    `vzdump <ID_VM> --storage <NOMBRE_STORAGE> --mode stop --compress zstd`
    *Modos: `stop` (apaga), `suspend` (pausa), `snapshot` (en caliente).*
*   **Restaurar un backup:**
    `qmrestore /ruta/al/archivo.vma.zst <NUEVO_ID_VM>`
*   **Listar backups en un storage:**
    `pvesm list <NOMBRE_STORAGE>`

---

## 🗄️ 3. Gestión de Almacenamiento (Storage)
*   **Estado de todos los storages:** `pvesm status`
*   **Escanear discos físicos:** `lsblk` o `fdisk -l`
*   **Ver uso de disco detallado:** `df -h`
*   **Ubicación por defecto (tipo Directory):** `/var/lib/vz/images/`

---

## 🛠️ 4. Comandos de Rescate y Fallos
Si la interfaz web (GUI) no responde o el nodo está bloqueado:

*   **Reiniciar el servicio web (pveproxy):**
    `systemctl restart pveproxy.service`
*   **Reiniciar el gestor de cluster (pvestatd):**
    `systemctl restart pvestatd.service`
*   **Ver logs en tiempo real (para diagnosticar fallos):**
    `journalctl -f`
*   **Desbloquear una VM (quitar el "lock" tras un fallo):**
    `qm unlock <ID_VM>`

---

## 🌐 5. Configuración de Red
Si pierdes acceso a la IP de Proxmox, debes editar el archivo de interfaces:

*   **Editar red:** `nano /etc/network/interfaces`
*   **Aplicar cambios de red:** `ifreload -a` (o reiniciar el servicio: `systemctl restart networking`)

---

## 💾 6. Manejo de Discos (qemu-img en Proxmox)
Si usas storage de tipo "Directory", puedes usar los trucos de `qemu-img` aprendidos:

*   **Ver tamaño real de un disco de VM:**
    `qemu-img info /var/lib/vz/images/<ID>/vm-<ID>-disk-0.qcow2`
*   **Reducir espacio (reclamar ceros):**
    `qemu-img convert -O qcow2 archivo_inflado.qcow2 archivo_compacto.qcow2`

---

## 💡 Tips de Oro
1. **IDs de VM:** Proxmox asigna números (100, 101...). No olvides el ID, es la llave para casi todos los comandos.
2. **Consola Serial:** Si la VM no tiene red, puedes intentar entrar por terminal: `qm terminal <ID_VM>`.
3. **Actualización segura:** Siempre usa `apt update` seguido de `apt dist-upgrade` en Proxmox para mantener la estabilidad del kernel.

