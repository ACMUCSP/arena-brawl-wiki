---
title: Consideraciones
description: A tener en cuenta al momento de programar tu bot
tags:
 - guide
 - considerations
---

#
## Consideraciones

- Si tu implementación es muy lenta en cada iteración de bucle es más probable que un enemigo te mate o que el servidor del EVAB te expulse de la partida por considerarte inactivo y no realizar acciones.
- Los atributos de las estructuras `EvabBotPackage` y `ElementInfo` no se guardan de manera local y se actualizan en cada iteración de bucle, lo que quiere decir que no vale la pena tratar de modificarlas ya que el servidor solo actualizará la dirección y/o la autorización de moverse o de disparar que `evab::BotHandler` le envie.
- Las balas que tendrás son limitadas asi que aprovéchalas bien.
- En el día del evento se darán restricciones para el límite de memoria usado por tu bot, así que ten cuidado si en una iteración de bucle tu código puede llegar a sobrepasar ese límite de memoria permitida o sino el proceso de tu bot será detenido y tu implementación no podrá controlarlo.
