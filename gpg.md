# 📝 GPG Cheat Sheet - Ayuda Memoria

Guía rápida con los comandos esenciales de GPG para gestión de claves, cifrado y descifrado.

---

## 🔑 Gestión de Claves

### Generar par de claves
Crea tu identidad digital (clave pública y privada).
```bash
gpg --full-generate-key
```

### Listar claves instaladas
Muestra las claves disponibles en tu llavero local.
*   **Públicas:** `gpg --list-keys`
*   **Privadas:** `gpg --list-secret-keys`

### Exportar clave pública
Para compartirla con otras personas para que te envíen archivos cifrados.
```bash
gpg --armor --output mi_clave_publica.asc --export tu_correo@email.com
```

### Importar una clave ajena
Guarda la clave pública de otra persona para poder escribirle de forma segura.
```bash
gpg --import clave_amigo.asc
```

### Borrar una clave del sistema
Elimina una identidad de tu llavero local.
*   **Privada (crítico en PC prestada):** `gpg --delete-secret-keys tu_correo@email.com`
*   **Pública:** `gpg --delete-keys correo_amigo@email.com`

---

## 🌐 Servidores de Claves (Keyservers)

Permiten publicar tu clave pública en internet o buscar la de otras personas usando servidores como `://ubuntu.com` o `pgp.mit.edu`.

### Enviar tu clave pública al servidor
Publica tu clave para que cualquiera pueda encontrarte usando tu ID de clave.
```bash
gpg --keyservers hkps://://ubuntu.com --send-keys TU_KEY_ID
```
*   *Nota:* Reemplaza `TU_KEY_ID` con los últimos 8 u 16 caracteres de tu clave pública (lo ves al listarlas).

### Buscar la clave de alguien más
Busca en la base de datos pública usando el correo electrónico de la persona.
```bash
gpg --keyservers hkps://://ubuntu.com --search-keys correo_amigo@email.com
```

### Importar directamente desde el servidor
Si ya conoces el ID de clave de la otra persona, descárgala e impórtala en un solo paso.
```bash
gpg --keyservers hkps://://ubuntu.com --recv-keys ID_DE_SU_CLAVE
```

---

## 💾 Respaldo y Restauración Completa (Backup)

Utiliza estos comandos para migrar de computadora o guardar copias de seguridad de todas tus claves a la vez.

### Exportar todo el llavero (Backups)
Exporta absolutamente todas tus claves públicas y privadas en archivos únicos.
*   **Todas las públicas:** `gpg --export --output todas_las_publicas.gpg`
*   **Todas las privadas (¡Crítico/Secreto!):** `gpg --export-secret-keys --output todas_las_privadas.gpg`
*   **Clave de revocación:** `gpg --gen-revoke tu_correo@email.com > revocar.asc` *(Úsala solo si pierdes tu clave o te la roban para cancelarla en internet)*.

### Restaurar un respaldo (Restore)
Importa los archivos de respaldo en una instalación nueva de GPG.
```bash
gpg --import todas_las_publicas.gpg
gpg --import todas_las_privadas.gpg
```

---

## 🔒 Cifrado y Descifrado

### 1. Cifrado Asimétrico (Para enviar a otros)
Usa la **clave pública** del destinatario. Solo él podrá abrirlo con su clave privada.
```bash
gpg --recipient correo_amigo@email.com --encrypt documento.txt
```
*   *Resultado:* Crea `documento.txt.gpg`

### 2. Cifrado Simétrico (Para ti mismo o nube)
Usa una **contraseña manual**. Ideal para respaldar tus propios archivos en internet.
```bash
gpg --symmetric --cipher-algo AES256 archivo_a_guardar.txt
```
*   *Resultado:* Crea `archivo_a_guardar.txt.gpg`

### 3. Descifrar cualquier archivo
Aplica tanto para archivos cifrados con tu clave pública como para los simétricos con contraseña.
```bash
gpg --output archivo_original.txt --decrypt archivo_recibido.gpg
```

---

## 🖊️ Firmas Digitales

### Firmar y cifrar al mismo tiempo
Garantiza que el archivo es secreto y que realmente lo enviaste tú.
```bash
gpg --recipient correo_amigo@email.com --sign --encrypt documento.txt
```

### Verificar una firma
Comprueba que el archivo recibido no fue modificado y valida el autor.
```bash
gpg --verify archivo_recibido.sig
```
