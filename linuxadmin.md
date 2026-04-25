# Comandos de Linux para Administradores

Guía rápida de comandos esenciales para la gestión de procesos, monitoreo del sistema, redes y manipulación de texto.

## 1. Gestión de Procesos

*   **`ps -ef | head`**: Muestra las primeras 10 líneas de todos los procesos en el sistema con detalles completos.
    *   `-e`: Selecciona todos los procesos.
    *   `-f`: Formato de listado completo (UID, PID, PPID, C, STIME, TTY, TIME, CMD).
*   **`ps aux`**: Muestra todos los procesos, incluyendo porcentaje de uso de CPU (`%CPU`) y memoria (`%MEM`).
*   **`top`**: Monitor de procesos dinámico en tiempo real.
    *   **Teclas interactivas**:
        *   `m`: Ordenar procesos por uso de memoria.
        *   `p`: Ordenar procesos por uso de CPU.
        *   `k`: Matar un proceso enviando el PID.
*   **`htop`**: Versión mejorada e interactiva de `top` (más visual).
*   **`pidof <programa>`**: Devuelve el ID de proceso (PID) de un programa por su nombre.
*   **`jobs`**: Lista los procesos que se están ejecutando en segundo plano (background).
*   **`kill <PID>`**: Termina un proceso por su ID.
    *   `-9`: Envía la señal SIGKILL para forzar el cierre.
    *   *Ejemplo*: `kill -9 1120 625`
*   **`killall <nombre>`**: Termina procesos buscando por el nombre del ejecutable.
*   **`nice`**: Inicia un proceso con una prioridad específica (-20 es la más alta, +19 la más baja).
    *   *Ejemplo*: `nice -n 10 nano archivo.txt &`
*   **`renice`**: Cambia la prioridad de un proceso que ya se está ejecutando.
    *   *Ejemplo*: `sudo renice -n -5 -p 1120`

## 2. Estado del Sistema

*   **`vmstat <intervalo> <conteo>`**: Reporta estadísticas de memoria virtual, procesos, CPU, etc.
    *   *Ejemplo*: `vmstat 2 5` (Muestra 5 reportes cada 2 segundos).
*   **`df -h`**: Muestra el uso de espacio en disco de los sistemas de archivos en formato legible.
*   **`free -h`**: Muestra la cantidad de memoria RAM y Swap usada y libre.
*   **`uptime`**: Indica cuánto tiempo ha estado funcionando el sistema y la carga media.

## 3. Redes

*   **`ping -c 4 google.com`**: Envía 4 paquetes a un host para verificar conectividad y latencia.
*   **`speedtest-cli`**: Herramienta para medir el ancho de banda de internet (requiere `sudo dnf install speedtest-cli`).
*   **`dig google.com`**: Utilidad para realizar consultas DNS (requiere `sudo dnf install dnsutils`).
*   **`ss`**: Investigar sockets de red (reemplazo moderno de `netstat`).
    *   `ss -tuln`: Muestra puertos en escucha (`l`), TCP (`t`), UDP (`u`) y numérico (`n`).
    *   `ss -tnp`: Muestra conexiones TCP establecidas y el proceso (`p`) asociado.
*   **`traceroute <host>`**: Muestra la ruta de saltos que sigue un paquete hasta el destino.
*   **`nslookup <host>`**: Resolución de nombres DNS básica.
*   **`tcpdump`**: Analizador de tráfico de red.
    *   `tcpdump -D`: Lista interfaces disponibles.
    *   `sudo tcpdump -i enp1s0 -n`: Captura tráfico en una interfaz sin resolver nombres.
*   **`nmap <host>`**: Escáner de seguridad y exploración de red.
*   **`iperf`**: Herramienta para medir el rendimiento máximo de red.
*   **`nc` (Netcat)**: Herramienta de lectura/escritura en red.
    *   *Servidor*: `nc -l -p 1234`
    *   *Cliente*: `nc 192.168.124.66 1234`

## 4. Manipulación de Textos

*   **Expresiones Regulares**: Patrones usados para búsqueda de texto.
*   **`grep` / `egrep`**: Busca líneas que coincidan con un patrón.
*   **Pipes (`|`)**: Redirige la salida de un comando a la entrada de otro.
*   **Redirecciones**:
    *   `>`: Redirige salida a un archivo (sobrescribe).
    *   `>>`: Redirige salida a un archivo (añade al final).
    *   `<`: Toma la entrada desde un archivo.
*   **`sed`**: Editor de flujo para filtrar y transformar texto.
*   **`awk`**: Lenguaje de procesamiento de columnas.
    *   *Ejemplo*: `awk '/linea/ {print $3}' ejemplo.txt` (Imprime la tercera columna de líneas que contengan "linea").
*   **`cut`**: Remueve secciones de cada línea de archivos.
*   **`sort`**: Ordena líneas de texto.
*   **`uniq`**: Reporta u omite líneas repetidas (requiere que el texto esté ordenado).
    *   *Ejemplo*: `sort ejemplo.txt | uniq`
*   **`tr`**: Traduce o elimina caracteres.
    *   *Ejemplo*: `echo "hola mundo" | tr 'a-z' 'A-Z'`
*   **`wc`**: Cuenta líneas, palabras y bytes.
