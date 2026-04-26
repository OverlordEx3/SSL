# Trabajo Práctico #0

## Entorno
- GCC corriendo dentro de un contenedor docker, utilizando [_devcontainers_](https://code.visualstudio.com/docs/devcontainers/containers).
- OS: Ubuntu 26.04 _Resolute Racoon_

## Compilador

### Versiones
- GCC: 15.2.0
``` bash
compiler@ssl:/src $ gcc --version
gcc (Ubuntu 15.2.0-16ubuntu1) 15.2.0
Copyright (C) 2025 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

- G++: 15.2.0
``` bash
compiler@ssl:/src $ g++ --version
g++ (Ubuntu 15.2.0-16ubuntu1) 15.2.0
Copyright (C) 2025 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

- GDB: 17.1
``` bash
compiler@ssl:/src $ gdb --version
GNU gdb (Ubuntu 17.1-2ubuntu1) 17.1
Copyright (C) 2025 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
```

- make: 4.4.1-3
``` bash
compiler@ssl:/src $ make --version
GNU Make 4.4.1
Built for x86_64-pc-linux-gnu
Copyright (C) 1988-2023 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <https://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
```

### Versiones del lenguaje soportadas por GCC

> Extraído con el comando gcc -v --help 2>/dev/null | egrep "^[[:space:]]*-std=(c)(\+\+)?[1-9]+\S*"
>
> De esta forma, me trae únicamente las opciones de -std que sean de C/C++ estándar (no las extensiones de GNU)

``` bash
compiler@ssl:/src $ gcc -v --help 2>/dev/null | egrep "^[[:space:]]*-std=(c)(\+\+)?[1-9]+\S*"
  -std=c++11                  Conform to the ISO 2011 C++ standard.
  -std=c++14                  Conform to the ISO 2014 C++ standard.
  -std=c++17                  Conform to the ISO 2017 C++ standard.
  -std=c++1y                  Deprecated in favor of -std=c++14.  Same as -std=c++14.
  -std=c++1z                  Deprecated in favor of -std=c++17.  Same as -std=c++17.
  -std=c++20                  Conform to the ISO 2020 C++ standard (experimental and incomplete support).
  -std=c++23                  Conform to the ISO 2023 C++ standard (published in 2024; experimental and incomplete support).
  -std=c++26                  Conform to the ISO 2026 C++ draft standard (experimental and incomplete support).
  -std=c++2a                  Conform to the ISO 2020 C++ standard (experimental and incomplete support).  Same as -std=c++20.
  -std=c++2b                  Conform to the ISO 2023 C++ standard (published in 2024; experimental and incomplete support).  Same as -std=c++23.
  -std=c++2c                  Conform to the ISO 2026 C++ draft standard (experimental and incomplete support).  Same as -std=c++26.
  -std=c++98                  Conform to the ISO 1998 C++ standard revised by the 2003 technical corrigendum.
  -std=c11                    Conform to the ISO 2011 C standard.
  -std=c17                    Conform to the ISO 2017 C standard (published in 2018).
  -std=c18                    Conform to the ISO 2017 C standard (published in 2018).  Same as -std=c17.
  -std=c1x                    Deprecated in favor of -std=c11.  Same as -std=c11.
  -std=c23                    Conform to the ISO 2023 C standard (published in 2024).
  -std=c2x                    Deprecated in favor of -std=c23.  Same as -std=c23.
  -std=c2y                    Conform to the ISO 202Y C standard draft (experimental and incomplete support).
  -std=c89                    Conform to the ISO 1990 C standard.  Same as -std=c90.
  -std=c90                    Conform to the ISO 1990 C standard.
  -std=c99                    Conform to the ISO 1999 C standard.
  -std=c9x                    Deprecated in favor of -std=c99.  Same as -std=c99.
```

|Lenguaje|Version|Flags|
|:-:|:-:|:-:|
|C|C90|`-std=c89`, `-std=c90`|
|C|C99|`-std=c99`, `-std=c9x`|
|C|C11|`-std=c11`, `-std=c1x`|
|C|C17|`-std=c17`, `-std=c18`|
|C|C23|`-std=c23`, `-std=c2x`|
|C|C2Y|`-std=c2y`|
|C++|C++98|`-std=c++98`|
|C++|C++11|`-std=c++11`|
|C++|C++14|`-std=c++14`, `-std=c++1y`|
|C++|C++17|`-std=c++17`, `-std=c++1z`|
|C++|C++20|`-std=c++20`, `-std=c++2a`|
|C++|C++23|`-std=c++23`, `-std=c++2b`|
|C++|C++26|`-std=c++26`, `-std=c++2c`|

### Variables usadas en Dockerfile
``` dockerfile
ARG GCC_VERSION=15
ARG GPP_VERSION=15
ARG GDB_VERSION=17.1-2ubuntu1
ARG MAKE_VERSION=4.4.1-3
```