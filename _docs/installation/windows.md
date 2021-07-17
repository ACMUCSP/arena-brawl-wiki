---
title: Instalacion Windows
description: Getting started with Docsy Jekyll
tags:
  - installation
---
# Instalación en Windows

## Requisitos:

- SFML Versión 2.5.1
- CMake Versión 3.15 mínimo
- Compilador MinGW (g++)

## Instalación de SFML

- Crear una carpeta temporal para realizar la compilación de la librería SFML
- Ejecutar el siguiente comando en la carpeta creada:
  ```bash
  $ git clone https://github.com/SFML/SFML.git
  ```
- Una vez que el proceso de descarga termine, deberá construir el proyecto de la librería con cmake en una carpeta build que deberá crear;
  luego, en la misma carpeta donde se encuentra el archivo CMakeLists.txt de SFML ejecute el siguiente comando:
  ```bash
  $ cmake -G "MinGW Makefiles" -B build
  ```
- Ahora, vaya a la carpeta build y ejecute este último comando:
  ```bash
  $ mingw32-make install
  ```
  Esto instalará la librería SFML en el disco donde su sistema instala programas. 
  La librería es fácilmente removible simplemente eliminando la carpeta donde se instaló SFML. 
  Normalmente es en `C://Program-Files(x86)/SFML`

## Ejecución de EVAB

EVAB es portable, así que no requiere un procedimiento de instalación pero sí debe tomar en cuenta que los archivos de los bots participantes
se compilan cuando ejecute EVAB, lo cual hace que deba especificar las carpetas include y lib de su SFML instalado para hacerlo. 
En la raíz de EVAB encontrará un archivo llamado `CompilationSettings.conf` con dos unicos campos: `INCLUDE_PATH` y `LIB_PATH`,
en los cuales deberá colocar las rutas a las carpetas include y lib de su SFML instalado si es que se instaló en otra ruta que no sea `C://Program-Files(x86)/SFML`. 
Ambas carpetas las encontrará en la raíz de su SFML y señaladas con los nombres include y lib respectivamente.

Ahora sí puede ejecutar EVAB y probar su bot.
