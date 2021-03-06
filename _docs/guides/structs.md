---
title: Estructuras y funciones
description: Datos y funciones que usarás para construir tu bot
tags:
 - guide
 - template
 - cli
---

# Estructuras y funciones para programar tu bot

Para que tu implementación pueda interactuar con el EVAB necesitarás saber usar la plantilla que provee, la cual se puede generar usando el comando `./evab plantilla`.
El uso de la plantilla generada por el programa es obligatoria ya que contiene funciones indispensables para la comunicación entre tu bot y el EVAB.

- Primero necesitarás un nombre para tu bot y este puede ser brindado usando la variable global `name` y guardándola en la clase estática `evab::BotHandler`. Esta acción solo puede realizarse antes de llamar a la función `evab::BotHandler::stablishConnectionWithServer()`.
```cpp
  const std::string name = "EL_NOMBRE_DE_TU_BOT";
  evab::EvabBotPackage package;
  int main() {
    evab::BotHandler::setName(name);//Guarda el nombre de tu bot para toda la partida.
    (...)
```

- La segunda función llamada `evab::BotHandler::stablishConnectionWithServer()` hará que tu bot se conecte al servidor del EVAB. Este proceso demora 5 segundos aproximadamente por lo que puedes aprovechar ese tiempo para realizar cualquier precálculo que necesites.
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
          //calcular el jugador más cercano para dispararle primero
        }
      }
    */
    while(evab::BotHandler::onBotGameplay()){
    (...)
```

El método `evab::BotHandler::getGameData()` retorna una estructura de tipo `EvabBotPackage`, la cual posee los datos de respuesta por parte del servidor del EVAB que usarás para realizar tus cálculos. Todos los atributos de `EvabBotPackage` y `ElementInfo` son públicos.
No necesitas instanciar un objeto `EvabBotPackage` ya que `evab::BotHandler::getGameData()` devuelve una referencia de su atributo de tipo `EvabBotPackage` y se actualiza constantemente con el método `evab::BotHandler::onBotGameplay()`.

```cpp
  struct EvabBotPackage{
    //Información actualizada de todos los jugadores en la partida.
    std::vector<ElementInfo> players;
    //Información actualizada de todas las balas existentes en el mapa.
    std::vector<ElementInfo> bullets;
    //Atributo que verifica si tu bot está vivo o muerto(no necesitas usarlo directamente).
    bool isAlive;
    //Cantidad de munición actualizada y disponible de tu bot.
    int ammo;
  };
  ///////////////////////////////////////////
  struct ElementInfo{
    // Valores de posición y ángulo de dirección (sexagesimal) de tu bot.
    // Las posiciones x e y representan el extremo superior izquierdo del objeto.
    float x_position, y_position, direction;
    int player_id;
    /*Identificador del jugador en la partida
    (BotHandler guarda el identificador de tu bot, la cual 
    puede ser recuperada con el método "evab::BotHandler::getMyId()")*/
  };
```
- El método `evab::BotHandler::onBotGameplay()` servirá para dar inicio al bucle de recepción y envío de datos de tu bot al servidor. Dentro de este bucle será donde harás el llamado a las funciones de tu implementación y a los métodos de interacción:

	1. `void BotHandler::onBotActionRotation(const float& angInDegrees);`
	Representa la dirección a la que quieres que tu bot apunte en el juego. Se utiliza el sistema de ángulos horario (0 = derecha), (90 = abajo), (180 = izquierda), (270 = arriba).
	2. `void BotHandler::onBotActionMoving(const bool& enableMoving);`
	Representa que quieres que tu bot avance en la dirección a la que está apuntando.
	3. `void BotHandler::onBotActionAttack(const bool& enableAttack);`
	Representa que quiere que tu bot dispare en la dirección a la que está apuntando.

_Nota_: Revisa la [velocidad de los objetos](considerations#a-qué-velocidad-se-mueven-los-bots-y-las-balas) de EVAB para un mejor entendimiento de la acción de movimiento.

Los llamados de los 3 métodos a la vez no son obligatorios en una iteración de bucle, eso dependerá de lo que tu implementación requiera hacer, ya que `evab::BotHandler::onBotGameplay()` simplemente enviará los datos que tenga guardado actualmente.
El llamado del segundo método y el tercer método poseen un conflicto mutuo, lo que significa que no podrás llamarlos a ambos en la misma iteración de bucle y solo se ejecutará la acción del primer llamado de cualquiera de ambos métodos mencionados. Es posible cancelar una de esas acciones simplemente volviendo a llamar al método pero con el parámetro de entrada en `false`.

```cpp
  (...)
  while(evab::BotHandler::onBotGameplay()){
    /*tu algoritmo*/
    evab::BotHandler::onBotActionRotation(42.f);
    evab::BotHandler::onBotActionAttack(1);//1 o true activará la acción actual
    /*necesitas cambiar tu acción!!!*/
    evab::BotHandler::onBotActionAttack(0);//0 o false desactivará la acción actual
    evab::BotHandler::onBotActionRotation(10.f);
    evab::BotHandler::onBotActionMoving(1);//Cambio de acción atacar -> moverse
  }
```

Sin embargo, el llamado del primer método de la lista si es posible realizarlo en conjunto con algunos de los 2 siguientes ya que tu bot necesitará apuntar/rotar ya sea para disparar o para moverte.

Al finalizar la iteración de bucle, los datos que se hayan actualizado como la rotación o la activación de alguna o ninguna acción (atacar o moverse) se enviarán al servidor para actualizar a tu bot en la partida.
