---
title: Windows
description:  Instalar EVAB en Windows
tags:
  - installation
---
# Instalación en Windows

## Requisitos:

- Compilador MinGW GCC 10.3.0 (Built by MSYS2 project)

## Instalación de C++ 10.3.0

Si no tuvieras el requisito de gcc 10.3.0 sigue los siguientes pasos, sino salta a la parte de "Ejecución de EVAB".

- Primero descargaremos MSYS desde su [página oficial](https://www.msys2.org/)
- Instala el archivo descargado (msys2-x86_64-20210725.exe).
- Ejecuta el programa "MSYS2 MSYS" (es el que acabas de instalar).
- Deberías tener algo como esta imagen:
![MSYS2 MSYS](../../assets/img/msys.jpg)
- Ahora ejecuta el siguiente comando:
  ```bash
  $ pacman -S mingw-w64-x86_64-gcc
  ```
![MSYS2 MSYS2](../../assets/img/msys2.jpg)
- Te pedirá confirmar la instalación, escribe "y" y dale enter.
- Ahora debes agregar al path del sistema "C:\msys64\mingw64\bin". En caso hayas elegido otra ubicación de instalación del "MSYS2 MSYS", entonces coloca la ubicación al bin de mingw64 en el path. ("tu_ubicación_de_instalación\mingw64\bin")
- Ahora vamos a confirmar que hemos instalado la version de c++ 10.3.0 correctamente abriendo
un "Símbolo de sistema" o "Command Prompt" (según tu idioma). Ejecuta el siguiente comando.
  ```bash
  $ c++ --version
  ```
Deberías ver algo así. En caso no, vuelve a hacer los pasos nuevamente o contáctanos para ayudarte.
![C++ version](../../assets/img/c++version.jpg)

## Ejecución de EVAB

EVAB es portable, así que no requiere un procedimiento de instalación pero sí debe tomar en cuenta que los archivos de los bots participantes
se compilan cuando ejecute EVAB. 
Para descargar EVAB usa el siguiente [enlace](../../assets/EVAB/EVAB_Win64.zip).<br>
Habrás descargado el archivo `EVAB_Win64.zip` el cual debes descomprimir. Al descomprimir verás la carpeta `EVAB`, ingresa en él. <br>
Ahora verás una carpeta con el nombre `SFML`, esta carpeta debes copiarla en esta ubicación: `C:\Program Files (x86)\`. (Seguramente te pedirá que accedas como administrador, dale aceptar, [SFML](https://www.sfml-dev.org/) es un framework que utiliza EVAB y es confiable). <br>
Ahora abre un "Símbolo de sistema" en esta ubicación y ejecuta:
  ```bash
  $ evab.exe jugar
  ```
Ahora elige un número cualquiera entre 2 y 10. Dale enter y deberías ver una batalla ejecutándose automáticamente. Quizá te pida un permiso de firewall, dale permitir.

![EVAB exec](../../assets/img/exec.jpg)

Ahora ve a "Guías" a aprender los demás comandos y empezar a programar tu bot.
