---
title: Competencia
permalink: /event/
---

# Arena Brawl 2021

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
