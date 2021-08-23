---
title: Linea de comandos
description: Comandos disponibles en EVAB
tags:
 - guide
 - terminal
 - command line
---

# Linea de comandos

La linea de comandos de EVAB te permite crear, compilar y ejecutar tus bots.

```bash
   █████╗ ██████╗ ███████╗███╗   ██╗ █████╗
  ██╔══██╗██╔══██╗██╔════╝████╗  ██║██╔══██╗
  ███████║██████╔╝█████╗  ██╔██╗ ██║███████║
  ██╔══██║██╔══██╗██╔══╝  ██║╚██╗██║██╔══██║
  ██║  ██║██║  ██║███████╗██║ ╚████║██║  ██║
  ╚═╝  ╚═╝╚═╝  ╚═╝╚══════╝╚═╝  ╚═══╝╚═╝  ╚═╝
  ██████╗ ██████╗  █████╗ ██╗    ██╗██╗
  ██╔══██╗██╔══██╗██╔══██╗██║    ██║██║
  ██████╔╝██████╔╝███████║██║ █╗ ██║██║
  ██╔══██╗██╔══██╗██╔══██║██║███╗██║██║
  ██████╔╝██║  ██║██║  ██║╚███╔███╔╝███████╗
  ╚═════╝ ╚═╝  ╚═╝╚═╝  ╚═╝ ╚══╝╚══╝ ╚══════╝
        ██╗   ██╗     ██╗        ████╗
        ██║   ██║    ███║      ██║   ██║
        ╚██╗ ██╔╝     ██║      ██║   ██║
          ╚██╔╝      ██║██╗ ██  ╚████╔═╝
           ╚═╝       ╚═╝╚═╝      ╚═══╝
  Entorno de Videojuego de Arena Brawl 2021

Uso: evab COMANDO

Opciones:
  ayuda         Muestra este mensaje
  compilar      Compila tu bot sin inicializar el juego
  jugar         Comienza el juego Arena Brawl
  plantilla     Crea una plantilla de codigo en la carpeta 'bots'
```

## Generar plantilla

Este comando permite crear la plantilla básica para programar tu bot.

```bash
$ ./evab plantilla
```

Se te pedirá ingresar el nombre de tu bot, el cual debe contener caracteres alfanuméricos,
guiones y sub-guiones. La plantilla se guardara en la carpeta `bots`.

_Nota_: No usar el nombre `computer`, pues este es el nombre de los bots por defecto. 
Si creas un archivo con dicho nombre, se sobrescribirá la próxima vez que ejecutes el juego.

## Compilar bot

Este comando permite compilar un bot sin inicializar el juego.

```bash
$ ./evab compilar
```

Se te pedirá ingresar el nombre del bot a compilar, debes escribir el nombre del archivo
sin la extensión _.cpp_. Una vez terminada la compilación se mostrara el mensaje _Listo!_

_Nota_: Este paso no es necesario para iniciar el juego. Antes de cada partida todos los bots
dentro de la carpeta `bots` son compilados y ejecutados independientemente.

## Iniciar juego

Este comando permite iniciar el juego con tus bots.

```bash
$ ./evab jugar
```

Se te pedirá ingresar la cantidad de bots por defecto (_computer bots_) para la partida,
estos bots se mueven y atacan de forma aleatoria.

A continuación se mostrará la lista de los bots considerados para el juego, si no ves a
tu bot, es probable que no se encuentre en la carpeta `bots`.

Cuando todos los bots se conecten, el juego comenzará automáticamente.

_Nota_: Si tu bot no compila para la partida, EVAB usará la última versión compilada.
