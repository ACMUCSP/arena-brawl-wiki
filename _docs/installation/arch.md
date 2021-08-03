---
title: Arch Linux
description: Instalar EVAB en Arch Linux 
tags:
  - installation
---
# Instalación en Arch Linux

## Requisitos:

- SFML versión 2.5.1
- gcc >= 9.3.0

Si no tienes instalado los requisitos o tienes versiones diferentes continúa con la sección "Instalando requisitos", sino ve directo a la sección de "Ejecución de EVAB".

## Instalando requisitos

- Instalando SFML: Abre una terminal y ejecutar el siguiente comando:
  ```bash
  $ sudo pacman -S sfml
  ```
- Instalando gcc: Abre una terminal y ejecutar el siguiente comando:
  ```bash
  $ sudo pacman -S gcc
  ```

## Ejecución de EVAB

Ahora [descarga](../../assets/EVAB/EVAB_linux.zip) el "Entorno de Videojuego Arena Brawl (EVAB)" y dentro de la carpeta ARENA_BRAWL_ACM_UCSP ejecuta el siguiente comando:

  ```bash
  $ ./evab jugar
  ```
EVAB te solicitará que elijas la cantidad de bots, coloca una cantidad entre 2 y 10. Ahora deberías ver varios bots combatiendo, son bots por defecto. Al final verás el cuadro de resultados. Con todo esto ya tenemos listo EVAB, ahora ve a "Guías" para que empieces a programar tu primer bot.
