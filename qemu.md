# 🛠️ Guía Rápida de qemu-img y Gestión de QCOW2

Este documento resume las mejores prácticas para manejar imágenes de disco QEMU/KVM desde la terminal.

---

## 💾 1. Backups Eficientes (Espacio Real)
Para que un backup ocupe solo lo que tiene datos escritos, la mejor opción es la conversión.

*   **Backup Estándar (Sparse):**
    `qemu-img convert -O qcow2 origen.qcow2 destino.qcow2`
*   **Backup Comprimido:**
    `qemu-img convert -c -O qcow2 origen.qcow2 destino.qcow2`
*   **Verificar tamaño real vs virtual:**
    `qemu-img info imagen.qcow2`
    *(Fíjate en `disk size` para el espacio real y `virtual size` para el máximo).*

---

## 📸 2. Snapshots (Puntos de Control)
Los snapshots se guardan dentro del propio archivo `.qcow2`.

*   **Crear snapshot:** `qemu-img snapshot -c nombre_snap imagen.qcow2`
*   **Listar snapshots:** `qemu-img snapshot -l imagen.qcow2`
*   **Restaurar snapshot:** `qemu-img snapshot -a nombre_snap imagen.qcow2`
*   **Borrar snapshot:** `qemu-img snapshot -d nombre_snap imagen.qcow2`

---

## 🔍 3. Mantenimiento y Reparación
*   **Chequear errores:** `qemu-img check imagen.qcow2`
*   **Expandir disco:** `qemu-img resize imagen.qcow2 +10G`
    *(Luego debes expandir la partición dentro del SO invitado).*

---

## 📂 4. Montar Imágenes para Extraer Archivos
Permite acceder a los datos sin iniciar la Máquina Virtual.

1. **Activar NBD:** `sudo modprobe nbd max_part=8`
2. **Conectar:** `sudo qemu-nbd --connect=/dev/nbd0 imagen.qcow2`
3. **Montar:** `sudo mount /dev/nbd0p1 /mnt` (Cambiar p1 por la partición deseada)
4. **Desconectar:** 
   - `sudo umount /mnt`
   - `sudo qemu-nbd --disconnect /dev/nbd0`

---

## 🚀 5. Optimizando el Espacio (TRIM)
Para que los archivos no "engorden" innecesariamente tras borrar datos dentro de la VM:
1. La VM debe usar controlador **VirtIO SCSI**.
2. Habilitar la opción `discard='unmap'` en la configuración del disco.
3. Dentro de la VM (Linux), ejecutar: `sudo fstrim -av`.

