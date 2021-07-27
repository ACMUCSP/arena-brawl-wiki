---
title: macOS
description: Instalar EVAB en macOS Big Sur
tags:
  - installation
---
# Instalación en macOS

## Requisitos:

- Apple clang, versión 12.0.0 o posterior.
- Administrador de paquetes [Homebrew](https://brew.sh/).

Es recomendable instalar las herramientas de linea de comandos de macOS,
estas se instalan automáticamente junto a Xcode.

## Instalación de SFML

Abre una terminal y ejecuta el siguiente comando:
```bash
$ brew install sfml
```

## Ejecución de EVAB

Descarga [EVAB](../../assets/EVAB/EVAB_macos.zip), descomprime el archivo y abre una terminal en la carpeta, finalmente ejecuta el siguiente comando:
  ```bash
  $ ./evab
  ```
Se mostrará un mensaje de ayuda si sfml se instaló correctamente.
