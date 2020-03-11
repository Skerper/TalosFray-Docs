---
weight: 60
title: Constants
---

# Constants

All-caps properties like the following are just handy pre-defined variables for use with various functions.

## HP (Powerup type)

```haxe
if(powerup.type == HP){
	log("I need that!");
}
```

A possible value of `powerup.type`.

## ENERGY (Powerup type)

```haxe
if(powerup.type == ENERGY){
	log("I need that!");
}
```

A possible value of `powerup.type`.

## AMMO (Powerup type)

```haxe
if(powerup.type == AMMO){
	log("I need that!");
}
```

A possible value of `Powerup.type`.

## CANNON (Projectile type)

```haxe
if(closest_projectile().type == CANNON){
	log("it is a cannonball");
}
```

A possible value of Projectile.type.

## DISRUPTOR (Projectile type)

```haxe
if(closest_projectile().type == DISRUPTOR){
	log("it is an emp burst");
}
```

A possible value of Projectile.type.

## SHOTGUN (Projectile type)

```haxe
if(closest_projectile().type == SHOTGUN){
	log("it is a shotgun pellet");
}
```

A possible value of Projectile.type.

## SNIPER (Projectile type)

```haxe
if(closest_projectile().type == SNIPER){
	log("it is a sniper slug");
}
```

A possible value of Projectile.type.

## UPDATE (SleepCode)
```haxe
while(true){
	if(!enemy.alive){
		enemy = random_bot();
		target(enemy);
	}
	if(item1.ready){
		item1.fire();
	}
	sleep_until(UPDATE);
}
```
>Neither enemy.alive nor item1.ready will change until we get new data from the arena, so it is a waste of cycles (and hence energy, if our CPU is overclocked) to keep checking them until that happens.

An argument for [`sleep_until`](#sleep-until-code), and a return code from [`woke_on`](#woke-on). Used for sleeping until new data comes from your bot's external hardware.

## TIMER (SleepCode)
```haxe
set_sleep_timer(5);
sleep_until(TIMER);
```

An argument for [`sleep_until`](#sleep-until-code), and a return code from [`woke_on`](#woke-on). Used for sleeping for the amount of time specified with `set_sleep_timer`.

## POWERUP_APPEARS (SleepCode)
```haxe
sleep_until(POWERUP_APPEARS);
```

An argument for [`sleep_until`](#sleep-until-code), and a return code from [`woke_on`](#woke-on). Used for sleeping until a powerup appears in the arena.

## UP_LEFT

```haxe
set_destination_to(UP_LEFT);
```
A direction to travel. Can also be targeted with `set_target_to`.

## UP

```haxe
set_destination_to(UP);
```
A direction to travel. Can also be targeted with `set_target_to`.

## UP_RIGHT

```haxe
set_destination_to(UP_RIGHT);
```
A direction to travel. Can also be targeted with `set_target_to`.

## LEFT

```haxe
set_destination_to(LEFT);
```
A direction to travel. Can also be targeted with `set_target_to`.

## RIGHT

```haxe
set_destination_to(RIGHT);
```
A direction to travel. Can also be targeted with `set_target_to`.

## DOWN_LEFT

```haxe
set_destination_to(DOWN_LEFT);
```
A direction to travel. Can also be targeted with `set_target_to`.

## DOWN

```haxe
set_destination_to(DOWN);
```
A direction to travel. Can also be targeted with `set_target_to`.

## DOWN_RIGHT

```haxe
set_destination_to(UP_LEFT);
```
A direction to travel. Can also be targeted with `set_target_to`.

## SECTOR1

```haxe
set_destination_to(SECTOR1);
```
Represents the top-left sector of the arena if you divide it into a 9-square grid.

## SECTOR2

```haxe
set_destination_to(SECTOR2);
```
Represents the top-middle sector of the arena if you divide it into a 9-square grid.

## SECTOR3

```haxe
set_destination_to(SECTOR3);
```
Represents the top-right sector of the arena if you divide it into a 9-square grid.

## SECTOR4

```haxe
set_destination_to(SECTOR4);
```
Represents the middle-left sector of the arena if you divide it into a 9-square grid.

## SECTOR5

```haxe
set_destination_to(SECTOR5);
```
Represents the middle sector of the arena if you divide it into a 9-square grid.

## SECTOR6

```haxe
set_destination_to(SECTOR6);
```
Represents the middle-right sector of the arena if you divide it into a 9-square grid.

## SECTOR7

```haxe
set_destination_to(SECTOR7);
```
Represents the bottom-left sector of the arena if you divide it into a 9-square grid.

## SECTOR8

```haxe
set_destination_to(SECTOR8);
```
Represents the bottom-middle sector of the arena if you divide it into a 9-square grid.

## SECTOR9

```haxe
set_destination_to(SECTOR9);
```
Represents the bottom-right sector of the arena if you divide it into a 9-square grid.
