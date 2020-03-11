---
weight: 40
title: Types
---

# Types

There are several datatypes with their own properties and methods that are used to control your bot.

<aside class="notice">
All of the read-only data in these types are updated 60 times a second. Commands made by calling methods and so on are also only delivered to the rest of the bot's hardware 60 times a second.
</aside>

<aside class="success">
These types aren't the physical objects themselves - they are only ways to organize information our bot knows about them. Even if you try to set an enemy's HP to zero, they won't die!
</aside>

## Position (Type)

`Position` is the base object for many objects available in your bot code. Any object that extends `Position` can have its whereabouts queried in relation to other objects, and can be targeted or used as a destination. The methods and properties described in this class are available in every Type labeled 'extends Position'.

### Availibility

`Position` can never be used directly, but it is the base object for `Powerup`, `Bot`, `Bullet`, and `Self`, so all of the following methods and properties are available in all of those objects.

### Methods
Method                    |Arguments                                          |Returns    |Description
--------------------------|---------------------------------------------------|-----------|----------------------------------------------------------------------
above(obj)                |obj - a Position-based object                      |Bool       |True if the obj is above the `Bot`.
below(obj)                |(as above)                                         |Bool       |True if the obj is below the `Bot`.
close_to(obj)             |(as above)                                         |Bool       |True if the object is close enough to the `Bot` to hit with a Saw.
closer(than, to)          |than, to - both Position-based objects.			  |Bool		  |True if the object is closer to 'to' than 'than' is to 'to'.
left_of(obj)              |(as above)                                         |Bool       |True if the obj is to the left of the `Bot`.
right_of(obj)             |(as above)                                         |Bool       |True if the obj is to the right of the `Bot`.
short_range_to(obj)       |obj - a Position-based object                      |Bool       |True if the obj is within range of short-range weapons
medium_range_to(obj)      |obj - a Position-based object                      |Bool       |True if the obj is within range of medium-range weapons
medium_long_range_to(obj) |obj - a Position-based object                      |Bool       |True if the obj is within range of medium-long-range weapons
long_range_to(obj)        |obj - a Position-based object                      |Bool       |True if the obj is within range of long-range weapons
will_hit(obj)			  |obj - a Position-based object                      |Bool       |True if, at their current speeds and headings, the supplied `obj` will collide with this object at some point.


### Properties
Property       |Type        |Access    |Description
---------------|------------|----------|--------------------------------------------------
sector         |Int         |Read only |The sector that the Position object is in (1 to 9)


## BattleDetails (Type)

```haxe
if(battle.over && winner == me){
	log("yeet");
}
```

Contains information about the state of this bout.

<aside class="success">
It often pays to be cautious when there are many bots remaining, but aggressive when there are few!
</aside>

### Availability
Available anywhere in code as `battle`.

### Properties

Property       |Type        |Access    |Description
---------------|------------|----------|--------------------------------------------
entrants       |Int         |Read only |The number of bots in this bout.
over           |Bool        |Read only |True if the bout has ended; false otherwise.
survivors      |Int         |Read only |The number of bots still active.
time_remaining |Int         |Read only |Time in seconds remaining in the bout.
winner         |Bot         |Read only |Reference to the round winner. Null if the round hasn't ended yet.


## Bot (Type)

**extends [Position](#position-type).**

```haxe
var enemy = closest_bot(); //enemy now contains a `Bot`
if(enemy.hp > my.hp){
	set_destination_to(enemy);
	retreat();
}
```
>Most tactical decisions will resolve around `Bot` objects!

`Bot` objects are our main way of knowing about other bots in the arena. They can be used for targeting, and queried about their position and status.

### Availability
Returned by various methods. Our own is always available as `me`.

### Properties
Property       |Type        |Access    |Description
---------------|------------|----------|--------------------------------------------
ammo           |Int         |Read only |The remaining ammo percentage of the bot as an integer. Ranges from 0 to 100. 
alive          |Bool        |Read only |True if they are. False if they ain't.
energy         |Int         |Read only |The remaining energy percentage of the bot as an integer. Ranges from 0 to 100.
hp	           |Int         |Read only |The remaining HP percentage of the bot as an integer. Ranges from 0 to 100. 
id	           |Int         |Read only |This bot's entry number. Not very useful. 
is             |Bot|Read only |Self-referential. So you can do stuff like `if(enemy.is.above(me))`.
name           |String      |Read only |The bot's name. If you want to team up with someone, this could be useful!



## Item (Type)

>Target a new enemy if the old one is dead. Fire if we're on target! This is a common control routine for a cannon-type item.

```haxe
if(enemy.alive == false){
	enemy = closest_bot();
	item1.set_target_to(enemy);
}
if(item1.ready){
	item1.fire()
}
```

>Activate your saw if your enemy is in range!

```haxe
if(enemy.is.close_to(me)){
	item1.activate();
}
else{
	item2.deactivate(); //Saws use energy quickly, so turn them off when they're not in use!
}
```

`Item` objects are your way of communicating with weapons and devices installed on your bot. Even though all of these properties and methods are available on every `Item`, not every item will make use of or respond to them. Think of it as a generic television - not every button works on every TV.

### Availability
Your bot has 4 item slots, available in code as `item1` to `item4`. All of these are `Item` objects. Even if you don't install an item in a slot, there will be a placeholder `Item` object there. 

### Properties
Property       |Type        |Access    |Description
---------------|------------|----------|----------------------------------------------------------------------------------------------------
activated      |Bool        |Read/write|Set to true if you want to attempt to activate this item. False if you wish to deactivate it.
active         |Bool        |Read only |True if the item is currently running. (Not all items can be activated; some only can be fired.)
ready		   |Bool		|Read only |True only if the item is on-target, off-cooldown, and has enough energy or ammo to fire or activate.

### Methods
Method                    |Arguments                                          |Returns    |Description
--------------------------|---------------------------------------------------|-----------|-----------------------------------------------------------------
fire()		              |None									     		  |Void       |Attempt to fire this item. (Not all items can be fired.)
activate()                |None											      |Void       |Attempt to activate this item. Same as `item.active=true;`	
deactivate()              |None											      |Void       |Attempt to deactivate this item. Same as `item.active=false;`	
set_target_to(targetable) |targetable (object with id:Int field)              |Void       |Set this item to target `targetable`
target(targetable)        |targetable (object with id:Int field)              |Void       |Shorthand for `set_target_to`

<aside class="success">
Using the global <code>set_target_to</code> command has the same effect as calling <code>set_target_to</code> on all of your items one by one. Since it's only one call, it's faster CPU-wise to use the global comand when you don't need to target different targets with different items.
</aside>


## Powerup (Type)

**extends [Position](#position-type).**

```haxe
if(powerup.active && powerup.type == HP && my.hp < 50){
	set_destination_to(powerup);
}
```

The `Powerup` type contains information about the status of the powerup in the arena. There can only be one powerup active at a time, and it is often unavailable.

### Availability
There is only one, and it is available in the global `powerup` property.

### Properties
Property       |Type            |Access    |Description
---------------|----------------|----------|--------------------------------------------
available      |Bool            |Read only |True if the powerup has appeared. False otherwise.
is             |Powerup         |Read only |Self-referential. So you can do stuff like `if(enemy.is.above(me))`.
type           |Int             |Read only |The type (ammo, hp, energy) of this powerup. Use `HP`, `AMMO`, `ENERGY` constants to compare.


## Projectile (Type)

**extends [Position](#position-type).**

```haxe
if(closest_projectile().is.short_range_to(me)){
	log("Yikes!");
}
```

The `Projectile` type contains information about projectiles fired from weapons, such as Disruptor rounds or Cannon rounds.

### Availability
Returned by methods such as `closest_projectile()`.

### Properties
Property       |Type            |Access    |Description
---------------|----------------|----------|--------------------------------------------
exists         |Bool            |Read only |True if the projectile still exists. False if it has disappeared somehow.
is             |Powerup         |Read only |Self-referential. So you can do stuff like `if(bullet.is.above(me))`.
owner 		   |Bot 			|Read only |A reference to the bot that fired this projectile.
type           |String          |Read only |The type of weapon this projectile was fired from. Use `CANNON`, `DISRUPTOR`, etc constants to compare.

<aside class='success'>
Projectiles don't usually last for very long - maybe a few seconds at best. It's important to check that a projectile still exists before you make any major decisions about it!
</aside>


## Self (Type)

**extends [Position](#position-type).**

```haxe
if(my.hp < 10){
	set_destination_to(closest_bot()); //Run awaaaaay!
	retreat();
}
```

The `Self` type holds details about our own bot. It's a good idea to adjust your strategy based on your remaining HP, ammo, and energy.

<aside class="notice">
Sorry, you can't boost your own HP with tricks like <code>my.hp = 100;</code>. Think of <code>Self</code> as a report card. 
</aside>

### Availibility
You can always get your own `Self` with the `my` and `I` global properties.

### Properties
Property       |Type            |Access    |Description
---------------|----------------|----------|--------------------------------------------	
ammo           |Int         	|Read only |Your remaining ammo percentage as an integer. Ranges from 0 to 100. 
am             |Self            |Read only |Self-referential. So you can do stuff like `if(I.am.close_to(enemy))`.	
energy         |Int         	|Read only |Your remaining energy percentage as an integer. Ranges from 0 to 100.
hp	           |Int         	|Read only |Your remaining HP percentage as an integer. Ranges from 0 to 100.
name		   |String          |Read only |Your own name. Hopefully you don't need this.
