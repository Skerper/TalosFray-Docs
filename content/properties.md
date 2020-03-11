---
weight: 30
title: Properties
---

# Properties

These are variables and objects that are accessible from anywhere within your bot code.

## battle

```haxe
if(battle.over){
	log("Home time!");
}
```

The [`BattleDetails`](#battledetails) object reference, containing information about this bout.

## I

```haxe
if(I.am.above(him)){
	log("Wa ha ha");
}
```

Our [`Self`](#self) object. Contains useful info about our own bot's status.

## item1

```haxe
if(item1.ready){
	item1.fire();
}
```

The [`Item`](#item) installed in Slot #1. 

## item2

```haxe
if(item2.ready){
	item2.fire();
}
```

The [`Item`](#item) installed in Slot #2. 

## item3

```haxe
if(item3.ready){
	item3.fire();
}
```

The [`Item`](#item) installed in Slot #3. 

## item4
```haxe
if(item4.ready){
	item4.fire();
}
```

The [`Item`](#item) installed in Slot #4. 

## my

```haxe
if(my.hp < 10){
	log("yabai");
}
```

Our [`Self`](#self) object. Contains useful info about our own bot's status.

## me

```haxe
var enemy = closest_bot();
if(enemy == me){
	log("Oh... guess I won!");
}
```

Our own [`Bot`](#bot) object. Not really useful for much other than comparing to other `Bot` objects.

## powerup

```haxe
if(powerup.available){
	set_destination_to(powerup);
}
```

The [`Powerup`](#powerup) object. Contains handy info about the state of powerups in the game world.