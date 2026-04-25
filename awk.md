# Guía del Comando AWK

`awk` es un lenguaje de procesamiento de texto potente y versátil, diseñado para manipular datos basados en columnas y generar reportes.

## Sintaxis Básica

```bash
awk 'patrón { acción }' archivo
```
Si el patrón coincide, se ejecuta la acción (por defecto la acción es imprimir la línea completa).

## Variables Internas Clave

*   **`$0`**: Representa la línea completa actual.
*   **`$1, $2, $n`**: Representan el primer campo, segundo campo, etc.
*   **`FS`** (Field Separator): Define el separador de campos (por defecto es espacio o tabulador).
*   **`NR`** (Number of Record): El número de la línea actual que se está procesando.
*   **`NF`** (Number of Fields): El número total de campos en la línea actual.
*   **`OFS`** (Output Field Separator): Separador de campos para la salida (por defecto espacio).

## Ejemplos Prácticos

### 1. Imprimir columnas específicas
Imprimir el usuario y su shell desde `/etc/passwd` (usando `:` como separador).
```bash
awk -F':' '{ print $1, $7 }' /etc/passwd
```

### 2. Filtrar por coincidencias de texto
Buscar líneas que contengan "error" e imprimir la segunda columna.
```bash
awk '/error/ { print $2 }' log.txt
```

### 3. Filtrar por condiciones numéricas
Mostrar procesos que consuman más del 5% de CPU (suponiendo que la columna 3 es %CPU).
```bash
ps aux | awk '$3 > 5.0'
```

### 4. Usar variables NR y NF
Imprimir el número de línea seguido del contenido de la línea.
```bash
awk '{ print NR, $0 }' archivo.txt
```
Imprimir solo el último campo de cada línea (muy útil cuando el número de columnas varía).
```bash
awk '{ print $NF }' archivo.txt
```

### 5. Operaciones matemáticas
Sumar los valores de la primera columna e imprimir el total al final.
```bash
awk '{ sum += $1 } END { print "Total:", sum }' datos.txt
```

### 6. Filtrar por longitud de línea
Mostrar solo las líneas que tengan más de 80 caracteres.
```bash
awk 'length($0) > 80' archivo.txt
```

## Bloques Especiales

*   **`BEGIN { ... }`**: Se ejecuta **antes** de procesar cualquier línea. Útil para imprimir cabeceras o definir separadores.
*   **`END { ... }`**: Se ejecuta **después** de procesar todas las líneas. Útil para sumatorios o resúmenes.

Ejemplo completo:
```bash
awk 'BEGIN { print "Iniciando conteo..." } { count++ } END { print "Total de líneas:", count }' archivo.txt
```
