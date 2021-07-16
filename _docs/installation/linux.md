---
title: Instalación Linux Ubuntu 20.04 LTS
description: Instalar EVAB en Linux Ubuntu 20.04 LTS
---
# Instalación en Linux

## Requisitos:

- SFML Versión 2.5.1
- Compilador C++ 17

## Instalando requisitos

- Abre una terminal y ejecutar el siguiente comando:
  ```bash
  $ sudo apt-get install libsfml-dev
  ```
- Si no tuvieras instalado el compilador MinGW(g++), abre un terminal y ejecuta el siguiente comando:
  ```bash
  $ sudo apt install g++
  ```

## Ejecución de EVAB

Ahora puedes [descargar](../../assets/EVAB/EVAB_linux_ubuntu2004lts.rar) el "Entorno de Videojuego Arena Brawl (EVAB)" y dentro de la carpeta ARENA_BRAWL_ACM_UCSP ejecuta el siguiente comando:

  ```bash
  $ ./evab jugar
  ```
EVAB te solicitará que eligas la cantidad de bots, coloca una cantidad entre 2 y 10. Ahora deberías ver varios bots combatiendo, son bots por defecto. Al final verás el cuadro de resultados. Con todo esto ya tenemos listo EVAB, ahora ve a "Guías" para que empieces a programar tu primer bot.
