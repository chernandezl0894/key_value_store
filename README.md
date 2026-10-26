# key_value_store
A key-value store app using C.

## Estructura

```
inc/    cabeceras públicas (kv.h)
src/    implementación (kv.c) y punto de entrada (main.c)
```

## Configuración de Clang

En la raíz del repositorio hay tres archivos de configuración:

| Archivo         | Propósito                                                                 |
| --------------- | ------------------------------------------------------------------------- |
| `.clang`        | Flags de compilación por defecto (C11, warnings estrictos, `-Iinc`).       |
| `.clang-format` | Estilo de formateo (LLVM, indentación de 2 espacios, línea de 80).         |
| `.clang-tidy`   | Chequeos estáticos (bugprone, clang-analyzer, modernize, readability...). |

### Uso

```bash
# Formatear el código
clang-format -i src/*.c inc/*.h

# Comprobar el formato (sin escribir)
clang-format --dry-run -Werror src/*.c inc/*.h

# Compilar usando los flags del archivo .clang
clang src/main.c src/kv.c -o bin/kv @.clang

# Análisis estático (requiere un compile_commands.json)
clang-tidy -p build/ src/*.c
```

Notas:

- `.clang` no admite comentarios (es una lista de flags); es compatible con `clang @.clang`.
- `clang-tidy` necesita `compile_commands.json`. Se puede generar con
  `bear -- make` o con `cmake -DCMAKE_EXPORT_COMPILE_COMMANDS=ON`.
- `HeaderFilterRegex` cubre `inc/` y `src/`, así que también se analizan las cabeceras.
