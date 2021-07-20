---
title: Estructuras
description: Datos que usaras para construir tu bot
tags:
 - guide
 - template
 - cli
---

# Estructuras de la plantilla de tu bot

Para que tu implementación pueda interactuar con el Arena Brawl necesitarás saber usar la plantilla que provee EVAB, la cual se puede generar usando el comando `./evab plantilla`.
El uso de la plantilla generada por el programa es obligatoria ya que contiene funciones indispensables para la comunicación entre tu bot y el Arena Brawl.

- Primero necesitarás un nombre para tu bot y este puede ser brindado usando la variable global `name` y guardándolo en la clase estática `evab::BotHandler`. Esta acción solo puede realizarse antes del siguiente punto.
```cpp
  const std::string name = "EL_NOMBRE_DE_TU_BOT";
  evab::EvabBotPackage package;
  int main() {
    evab::BotHandler::setName(name);//Guarda el nombre de tu bot para toda la partida del Arena Brawl.
    (...)
```

- La segunda función llamada `evab::BotHandler::stablishConnectionWithServer()` hará que tu bot se conecte al servidor del Arena Brawl. Este proceso demora 5 segundos aporximadamente por lo que puedes aprovechar ese tiempo para realizar cualquier precálculo que necesites.
El siguiente trozo de código te muestra donde hacer ese precálculo:

```cpp
  const std::string name = "Wall-e";
  evab::EvabBotPackage package;
  int main() {
    evab::BotHandler::setName(name);
    evab::BotHandler::stablishConnectionWithServer();
    /*
      Inicia el margen de 5 segundos para precálculo
      ejemplo:
      for(auto& player : evab::BotHandler::getGameData().players){
        if(player.player_id != evab::BotHandler::getMyId()){
          //calcular el jugador mas cercano para dispararle primero
        }
      }
    */
    while(evab::BotHandler::onBotGameplay()){
    (...)
```

El método `evab::BotHandler::getGameData()` retorna una estructura de tipo `EvabBotPackage`, la cual posee los datos de respuesta por parte del servidor de Arena Brawl que usarás para realizar tus cálculos.
No necesitas instanciar un objeto `EvabBotPackage` ya que `evab::BotHandler::getGameData()` devuelve una referencia de su atributo de tipo `EvabBotPackage` y se actualiza constantemente con el método `evab::BotHandler::onBotGameplay()`.

```cpp
  struct EvabBotPackage{
    //Informacion actualizada de todos los jugadores en la partida.
    std::vector<ElementInfo> players;
    //Informacion actualizada de todas las balas existentes en el mapa.
    std::vector<ElementInfo> bullets;
    //Atributo que verifica si tu bot está vivo o muerto(no necesitas usarlo directamente).
    bool isAlive;
    //Cantidad de munición actualizada y disponible de tu bot.
    int ammo;
  };
  ///////////////////////////////////////////
  struct ElementInfo{
    //Valores de posición y ángulo de direccion (sexagesimal) de tu bot.
    float x_position, y_position, direction;
    int player_id;
    /*Identificador del jugador en la partida
    (BotHandler guarda el identificador de tu bot, la cual 
    puede ser recuperada con el método "evab::BotHandler::getMyId()")*/
  };
```
- El método `evab::BotHandler::onBotGameplay()` servirá para dar inicio al bucle de recepción y envío de datos de tu bot al servidor. Dentro de este bucle será donde harás el llamado a las funciones de tu implementación y a los métodos de interacción:
1. `void BotHandler::onBotActionRotation(const float& rotInDegrees);`
Representa la dirección a donde está apuntando tu bot en el juego.
2. `void BotHandler::onBotActionMoving(const bool& enableMoving);`
Representa que quieres que tu bot avance en la dirección a la que está apuntando.
3. `void BotHandler::onBotActionAttack(const bool& enableAttack);`
Representa que quiere que tu bot dispare en la dirección a la que está apuntando.

Los llamados de los 3 métodos a la vez no son obligatorios en una iteración de bucle, eso dependerá de lo que tu implementación requiera hacer, ya que `evab::BotHandler::onBotGameplay()` simplemente enviará los datos que tenga guardado actualmente.
El llamado del segundo método y el tercer método poseen un conflicto mutuo, lo que significa que no podrás llamarlos a ambos en la misma iteración de bucle y solo se ejecutará la acción del primer llamado de cualquiera de ambos métodos mencionados. Y es posible cancelar una de esas acciones simplemente volviendo a llamar al método pero con el parámetro de entrada en `false`.

```cpp
  (...)
  while(evab::BotHandler::onBotGameplay()){
    /*tu algoritmo*/
    evab::BotHandler::onBotActionRotation(42.f);
    evab::BotHandler::onBotActionAttack(1);//1 o true activará la acción actual
    /*necesitas cambiar tu accion!!!*/
    evab::BotHandler::onBotActionAttack(0);//0 o false desactivará la acción actual
    evab::BotHandler::onBotActionRotation(10.f);
    evab::BotHandler::onBotActionMoving(1);//Cambio de acción atacar -> moverse
  }
```

Sin embargo, el llamado del primer método de la lista si es posible realizarlo en conjunto con algunos de los 2 siguientes ya que tu bot necesitará apuntar/rotar ya sea para disparar o para moverte.

Al finalizar la iteración de bucle, los datos que se hayan actualizado como la rotación o la activación de alguna o ninguna acción (atacar o moverse) se enviarán al servidor para actualizar a tu bot en la partida.

## Consideraciones

- Si tu implementación es muy lenta en cada iteración de bucle es más probable que un enemigo te mate o que el mismo servidor te expulse por estar AFK.
- Los atributos de las estructuras `EvabBotPackage` y `ElementInfo` no se guardan de manera local y se actualizan en cada iteración de bucle, lo que quiere decir que no vale la pena tratar de modificarlas ya que el servidor solo actualizará la dirección y/o la autorización de moverse o de disparar que `evab::BotHandler` le envie.
- Las balas que tendrás son limitadas asi que aprovéchalas bien.
- En el día del evento se darán restricciones para el límite de memoria usado por tu bot, así que ten cuidado si en una iteración de bucle tu código puede llegar a sobrepasar ese límite de memoria permitida o sino el servidor te expulsará en plena partida.