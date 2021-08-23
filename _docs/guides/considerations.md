---
title: FAQ
description: Preguntas frecuentes sobre EVAB
tags:
 - guide
 - considerations
 - faq
---

# Preguntas frecuentes

Consideraciones generales y preguntas frecuentes al momento de programar tu bot y usar EVAB. Es **obligatoria** la lectura de esta sección para comenzar a programar tu bot.

### ¿Cada cuánto tiempo se actualiza el paquete de datos?

EVAB envía el paquete de datos `EVAB::EvabBotPackage` cada _100 ms_ a todos los bots que hayan enviado una respuesta a EVAB en la iteración anterior.
Es decir, cada iteración del bucle `while(evab::BotHandler::onBotGameplay())` debe durar como máximo _100 ms_. 
Si el tiempo usado en los cálculos dentro del bucle `while` principal dura más de _100 ms_, tu bot no enviará su respuesta al servidor 
a tiempo para dicha ronda y la aplazará para la próxima, o hasta que terminen los operaciones realizadas de la iteración actual.

De este modo, si tu implementación es muy lenta, es más probable que un enemigo te mate ya que el servidor del EVAB te considerará inactivo al no enviar acciones a tiempo,
y además, no recibirás todos los paquetes.

Por ejemplo, supongamos que tu implementación se demora _1s_ en alguna iteración, por lo tanto, no enviará su respuesta durante 9 rondas
(ya sea `evab::BotHandler::onBotActionAttack()`, `evab::BotHandler::onBotActionMoving()` o `evab::BotHandler::onBotActionRotation()`), y no recibirás 9 paquetes.
Durante ese tiempo puede que un bot enemigo dispare una bala en tu dirección y te elimine del juego, o que tus ataques ya no sean certeros debido a que los bots
enemigos probablemente se movieron en las 9 rondas que tu bot se mantuvo inactivo.

### ¿A qué velocidad se mueven los bots y las balas?

Antes de conocer la velocidad de los objetos en EVAB, es importante conocer sus dimensiones. Las cuáles son las siguientes (_ancho x alto_ en unidades):
- Espacio: _1000 x 1000_
- Nave: _25 x 26_
- Bala: _20 x 10_

_Nota_: Las coordenadas del espacio vienen dadas por los siguientes puntos: 
- (0, 0): extremo superior izquierdo
- (1000, 1000): extremo inferior derecho.

La velocidad de los objetos en EVAB son las siguientes (_unidades x iteración_):
- Nave: _10_
- Bala: _25_

Por ejemplo, si un bot se encuentra en la posición **(x, y)**, y realiza las acciones  `evab::BotHandler::onBotActionRotation(90)` y `evab::BotHandler::onBotActionMoving(true)`.
Su posición para la próxima iteración será **(x, y + 10)**, es decir, descenderá 10 unidades.

Es muy importante conocer fundamentos trigonométricos para hallar las distancias y ángulos entre objetos para predecir sus trayectorias y realizar rotaciones.
Para ello, es totalmente válido el uso de la librería `math.h` de STL.

### ¿Puedo modificar los valores que recibo en `EVAB::EvabBotPackage`?

Los atributos de las estructuras `EVAB::EvabBotPackage` y `EVAB::ElementInfo` no se guardan de manera local y se actualizan en cada iteración de bucle,
lo que quiere decir que no vale la pena tratar de modificarlas ya que el servidor solo actualizará la dirección y/o la autorización de moverse o de disparar que `evab::BotHandler` le envié
(es decir, `evab::BotHandler::onBotActionAttack()`, `evab::BotHandler::onBotActionMoving()` o `evab::BotHandler::onBotActionRotation()`).

Lo que si es muy válido es guardar dicha información durante las rondas para tomar mejores decisiones a posterior.
```c++
package = evab::BotHandler::getGameData();
// insertar package en algún vector
package_history.push_back(package);
```
_Nota_: Revisa bien el [uso de memoria](#existen-restricciones-del-uso-de-memoria-y-cpu) si realizas este guardado de información. 


### ¿Cuántas balas tiene mi bot?

Las balas que tendrás son limitadas (120 al comenzar el juego), así que aprovéchalas bien. Estas no se recargan una vez se hayan acabado.

### ¿Puedo atacar y moverme al mismo tiempo?

No, solo puedes realizar una de dichas acciones durante una iteración. Sin embargo, siempre puedes realizar una rotación
(la cuál define la dirección de movimiento del bot, o de la bala disparada).

Por ejemplo, si quieres disparar dos balas, necesitaras hacerlo en 2 rondas diferentes:
```c++
int shot_twice = 0;
while(evab::BotHandler::onBotGameplay()){
  (...)
  if (shot_twice < 2) {
    evab::BotHandler::onBotActionAttack(true);
    show_twice++;
  }
  (...)
}
```
De la misma forma, si quieres llegar a un punto dado, deberás hacerlo en varias iteraciones, en cada una de las cuales te moverás 10 unidades en una dirección determinada.

### ¿Existen restricciones del uso de memoria y CPU?

Días antes del evento se anunciarán las restricciones detalladas del uso de recursos por cada bot. Estas serán no menos que:

| Recursos |
|--|
| CPU | 1 procesador de 3.1 Ghz |
| Memoria | 1 GB |

En el evento Arena Brawl, los bots se ejecutarán en contenedores de docker, ten cuidado si en una iteración de bucle tu código puede llegar a sobrepasar el límite de memoria permitida,
ya que es probable que el proceso de tu bot sea detenido, afectando tu participación.
