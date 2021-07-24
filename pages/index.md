---
layout: page
title: Docsy Jekyll Theme
permalink: /
---

# ARENA BRAWL
###### *edición 2021 naves espaciales*

10 naves, ningún humano controlándolos y 60 segundos en cuenta regresiva determinarán la supremacía del bot vencedor en la arena intergaláctica. ¿Quién será el humano causante de dicha victoria?

![assets/img/docsy-jekyll.png](assets/img/main_page_video.gif)

## ¿Qué es Arena Brawl?

Arena Brawl es una competición de programación de bots. Cada equipo debe programar su bot para que se desenvuelva autónomamente durante
las batallas de Arena Brawl. Para esto, debes poner en práctica todos tus conocimientos sobre programación y proponer excelente estrategias. Los equipos son libres de decidir como programar 
sus bots siempre que sigan las reglas del concurso. 
El objetivo es destrozar las naves enemigas para ser el último en pantalla. Y si hay más de un bot en pantalla, tus vidas restantes, uso
eficiente de las 120 balas otorgadas y haber hecho el primer destrozo te avalarán para pasar a la siguiente fase.

## ¿Qué es EVAB?

EVAB significa "Entorno de Videojuego Arena Brawl", es el software desarrollado por el equipo de ACM-UCSP para ejecutar las batallas de Arena Brawl.

## Reglas de elegibilidad de participantes

Lee bien estas condiciones ya que si faltas a alguna, serás descalificado.

- El concurso será restringido a los estudiantes de tiempo completo de pregrado de la carrera de Ciencia de la Computación de la Universidad Catolica San Pablo (UCSP). (esperamos que apartir de la segunda edición sea abierto para cualquier persona.)
- Tamaño del equipo: 1-2 personas.
- Todo equipo y/o participante deberá completar su inscripción hasta la fecha que indique cada edición, caso contrario no será considerado para el evento.

## Reglas del concurso

- El único lenguaje de programación permitido es c++ (11, 14 ó 17). 
- La única librería permitida es STL (Standard Template Library). No es obligatorio que la uses, pero si usas otra serás descalificado.
- Cada bot tendrá 03 vidas y 120 balas.
- Cada batalla tendrá una duración de 60 segundos.

## Formato del torneo

El torneo se divide en 2 etapas que corresponde a 02 fechas, semifinales y finales. 

#### Etapa semifinales

Esta primera fecha de semifinales tiene por objetivo ubicarte en las llaves mayores o menores de la etapa final. Todos los equipos
pasan a la etapa final pero según tu resultado irás a diferente llave.
Para las batallas de semifinales agruparemos de forma aleatoria a todos los equipos en grupos.
Estos grupos estarán conformados de mínimo 02 equipos y máximo de 10. La cantidad de grupos viene determinada de la siguiente forma:

```cpp
// Fórmula para determinar la cantidad de grupos.
// n = cantidad de equipos.

if | 1 <= n <= 10;   grupos = 2
   | n > 10;         grupos = techo(n/10)

```

La etapa de semifinales tiene la siguiente agenda:

|                                       Agenda de semifinales                                                      |
|:-----------------------------------:|:--------------------------------------------------------------------------:|
| I.   Ronda de test                  |         mínimo 01 batalla por participante y máximo 02.                    |
| II.  Ajustes de bots                |         15 minutos.                                                        |
| III. Primera ronda                  |         mínimo 01 batalla por participante y máximo 10 batallas.           |
| IV.  Ajustes de bots                |         15 minutos.                                                        |
| V.   Segunda ronda                  |         mínimo 01 batalla por participante y máximo 10 batallas.           |

Es nuestro objetivo que mínimamente tengas una batalla por ronda, pero es posible que te enfrentes a más. Si se da el caso, la suma de todos
tus resultados (de primera y segunda ronda) determinarán tu llave en la etapa final. También debes saber que todas las batallas de semifinales
se formarán de forma aleatoria.

Sabemos que es posible que te enfrentes por primera vez con otros bots, por eso
proponemos una "Ronda de test", esta solo servirá para que te des cuenta que todo anda bien con tu bot. ¿Y si no?,
tendrás un tiempo de 15 minutos, de "Ajuste de bots", para que soluciones tu problema. El segundo momento de "Ajuste de bots" úsalo 
estratégicamente.

¿Cuáles equipos pasarán a las llaves mayores y menores?

```cpp
// n = cantidad de equipos.

Llaves mayores  <--  Los techo(n/2) equipos con mayor puntaje acumulado de todas sus batallas de semifinales (primera y segunda ronda).
Llaves menores  <--  Los piso(n/2) equipos con menor puntaje acumulado de todas sus batallas de semifinales (primera y segunda ronda).
```

#### Etapa finales

En esta segunda fecha de finales se determinará al ganador del Arena Brawl. 
Según si estás ubicado en las llaves mayores o menores, cada batalla se determinará al mejor de 3 en caso de llaves mayores, al mejor de 1 en
caso de llaves menores.

Para determinar cuántos grupos en las llaves habrá se utilizará la siguiente fórmula:

```cpp
// n = cantidad de equipos.
// Determinar grupos en llaves mayores.

if | 1 <= n <= 10;   grupos = 2
   | n > 10;         grupos = techo(n/10)

// Determinar grupos en llaves menores.

if | 1 <= n <= 10;   grupos = 1
   | n > 10;         grupos = techo(n/10)

```

Los ganadores de cada batalla se determinará de la siguiente forma:

```cpp
// n = cantidad de equipos.

Ganadores   <--  Los techo(n/2) equipos con mayor puntaje por batalla (la batalla puede ser MD3 o MD1).
Perdedores  <--  Los piso(n/2) equipos con menor puntaje por batalla (la batalla puede ser MD3 o MD1).
```

Esta fecha de finales se divide en fases y en cada fase tendremos:

 - *Llaves mayores*, ganadores pasan a la siguiente fase y perdedores pasan a llaves menores.
 - *Llaves menores*, ganadores pasan a la siguiente fase de llaves menores y perdedores son eliminados.

La cantidad de fases dependerá de los grupos y la eliminación sucesiva para finalmente dar paso a la batalla final que será 1 vs 1.

## Puntaje obtenido por batalla

Estos puntajes te serán otorgados una vez acabe la batalla y determinará tu posición, asegúrate de entenderlos bien.

|                    Suceso                    | Bonificación en puntos |
|:--------------------------------------------:|:----------------------:|
| Mantenerte vivo hasta el final de la batalla.|        1,000,000       |
| Por cada naves destrozadas.                  |         100,000        |
| Por cada vidas restante.                     |         10,000         |
| Por cada munición restante.                  |           10           |
| Por destrozar primero a una nave.            |            1           |

## Patrocinadores

 - Departamento Ciencia de la Computación, Universidad Católica San Pablo Arequipa - Perú

## Equipo desarrollador de Arena Brawl 2021

 - *Proyect manager*   -  Joaquin Palma "The Real Yi" (Computer Science student).
 - *Graphic developer* -  Italo Mamani "FROZONUS" (Computer Science student).
 - *Logic developer*   -  Miguel N "EYE" (Computer Science student).
