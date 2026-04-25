# Guía de Expresiones Regulares (RegExp) en Linux

Las expresiones regulares son patrones utilizados para encontrar, filtrar o manipular texto. En Linux, herramientas como `grep`, `sed` y `awk` las utilizan de forma intensiva.

## 1. Tipos de Motores
*   **BRE (Basic Regular Expressions):** Utilizadas por defecto en `grep` y `sed`. Los símbolos `(`, `)`, `{`, `}` deben escaparse con `\`.
*   **ERE (Extended Regular Expressions):** Utilizadas con `grep -E` o `egrep`. Símbolos como `+`, `?`, `|` y los paréntesis no necesitan escape.
*   **PCRE (Perl Compatible):** Utilizadas con `grep -P`. Son las más potentes.

## 2. Metacaracteres (Anclas y Posición)
*   **`^`**: Inicio de línea. (Ejemplo: `^Admin` busca líneas que empiecen con "Admin").
*   **`$`**: Fin de línea. (Ejemplo: `bash$` busca líneas que terminen en "bash").
*   **`.`**: Cualquier carácter individual (excepto nueva línea).
*   **`\b`**: Límite de palabra (inicio o fin).
*   **`\B`**: No es un límite de palabra.

## 3. Cuantificadores (Repetición)
*   **`*`**: 0 o más repeticiones del carácter anterior.
*   **`+`**: 1 o más repeticiones (ERE).
*   **`?`**: 0 o 1 repetición (ERE).
*   **`{n}`**: Exactamente `n` veces.
*   **`{n,}`**: `n` o más veces.
*   **`{n,m}`**: Entre `n` y `m` veces.

## 4. Clases de Caracteres (Conjuntos)
*   **`[abc]`**: Cualquiera de los caracteres dentro del corchete.
*   **`[^abc]`**: Cualquier carácter que **no** esté en el corchete (negación).
*   **`[a-z]`**: Cualquier letra minúscula.
*   **`[0-9]`**: Cualquier dígito.
*   **`[a-zA-Z0-9]`**: Cualquier carácter alfanumérico.

### Clases POSIX (Sintaxis `[[:clase:]]`)
*   **`[:alnum:]`**: Alfanumérico.
*   **`[:alpha:]`**: Alfabético.
*   **`[:digit:]`**: Números.
*   **`[:lower:]`**: Minúsculas.
*   **`[:upper:]`**: Mayúsculas.
*   **`[:space:]`**: Espacios en blanco, tabuladores, etc.

## 5. Agrupación y Alternancia
*   **`|`**: Operador "OR" (O lógico). Ejemplo: `cat|dog` busca "cat" o "dog".
*   **`(...)`**: Agrupa elementos para aplicar cuantificadores o para capturar grupos.
*   **`\n`**: Referencia a un grupo capturado (ej. `\1` para el primer grupo).

## 6. Caracteres de Escape
*   **`\`**: Anula el significado especial de un metacarácter.
    *   Ejemplo: `\.` busca un punto literal en lugar de "cualquier carácter".
    *   Ejemplo: `\$` busca el símbolo de dólar literal.

## 7. Ejemplos Prácticos

### Buscar una dirección IPv4 básica
```bash
grep -E "([0-9]{1,3}\.){3}[0-9]{1,3}" archivo.txt
```

### Buscar líneas que NO estén vacías
```bash
grep "." archivo.txt
# O mejor aún:
grep -v "^$" archivo.txt
```

### Buscar correos electrónicos (simplificado)
```bash
grep -E "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}"
```

### Eliminar comentarios y líneas vacías con sed
```bash
sed -E '/^#|^$/d' archivo.conf
```
