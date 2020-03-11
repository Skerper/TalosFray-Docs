---
weight: 50
title: Items
---

# Items

Each bot can carry four items. Items can have offensive, defensive, or aesthetic abilities. Items generally consume ammo, energy, or make your bot slower due to their weight. All items use the same interface to control them, but not all items make use of all the interface's options. This section explains how to use each item, and gives an idea of its capabilities. 

## Interface

All items, regardless of their type, have the same properties and methods. Most items do not make use of all of them at once, however.

### Availability


> It can improve readability to put your items in nicely-named variables.

```haxe
var cannon = item1;   //Assuming you put a cannon in slot 1
cannon.fire();		  //now you can use cannon just like it was item1!
```

You can access your bots' items via the properties `item1`, `item1`, `item3`, and `item4` from anywhere in your program.

### Properties

Property       |Type        |Access    |Description
---------------|------------|----------|--------------------------------------------
active         |Bool        |Read only |Whether the item is currently engaged. Not all items need to be engaged to use.
activated      |Bool        |Read/write|Whether you have requested for the item to be engaged.
ready   	   |Bool        |Read only |Whether the item is ready to use. The specific meaning of this differs between items.


### Methods
Method            |Arguments                                          |Returns    |Description
------------------|---------------------------------------------------|-----------|------------------------------------------------------------------------
fire()            |N/A  									 		  |Void       |Requests that the item fires.
activate()        |N/A                                          	  |Void       |Sets "activated" to true, requesting activation.
deactivate()      |N/A                                           	  |Void       |Sets "activated" to false, requestion deactivation. 
set_target_to(obj)|obj - a targetable object (an enemy, sector, etc)  |Void       |Targets the supplied targetable object with just this device.
target(obj)       |(as above)                                         |Void       |Shorthand for the above (identical).

<aside class="warning">
Calling the global command "set_target_to" will override any devices' individually-set targets.
</aside>

<aside class="success">
Items don't need to be activated to use them, unless their instructions specifically say they do. Many items, like the cannon, take no notice whatsoever of activation status. Similarly, there are items that cannot be fired.
</aside>

<aside class="success">
You can target any object you can move to with <code>set_destination_to</code>, including bots, the powerup, sectors, and directions.
</aside>

<aside class="notice">
All of the code snippets in this section assume that the item being demonstrated is in item slot 1 (<code>item1</code>).
</aside>

## Cannon

```haxe
item1.set_target_to(closest_bot());
```

>Target leading is automatic.

```haxe
if(item1.ready){
	item1.fire();
}
```

>Checking ready makes sure you don't waste ammo shooting off in the distance while the turret comes around.

### Description
The cannon is your basic single-shot projectile weapon. It's mounted on a swivelling turret, which rotates to face the target. All bots start the round with their cannons facing away from the center of the arena. 

Cannons only report `ready` as true when they are on-target, off-cooldown, and have sufficient ammo. You can still fire the cannon when it's off-target, but there is no guarantee it will hit anything.

### Stats
Property    |Value
------------|-----
**Consumes**|Ammo
**Cost**    |Low
**Range**   |Medium
**Accuracy**|High
**Damage**  |Low
**Weight**  |Medium
**Aim Rate**|Medium
**Recoil**  |Medium
**Cooldown**|Short

### Controls
Targetable|Activatable|Reports ready
----------|-----------|-------------
Yes       |No         |Yes


## Deflector

```haxe
var projectile = closest_projectile();
if(projectile != null && projectile.close_to(me)){
	item1.activate();
}
else{
	item1.deactivate();
}
```

>It's best not to leave the deflector on for too long - it goes through energy very fast!

### Description

The Deflector is an energy-powered defensive item that is used to repel back enemy projectiles. 

<aside class="success">
Projectiles deflected with the Deflector become 'yours' - meaning that if someone is damaged or destroyed by their ricoheting, you get credit for it!
</aside>

<aside class="warning">
The Deflector can only deflect physical ammunition (cannon rounds, sniper shells, etc). Energy weapons like the Disruptor, and melee weapons like the Saw, will go straight through.
</aside>

### Stats

Property    |Value
------------|-----
**Consumes**|Energy
**Cost**    |High
**Range**   |Melee
**Accuracy**|N/A
**Damage**  |N/A
**Weight**  |Negligible
**Aim Rate**|N/A
**Recoil**  |N/A
**Cooldown**|N/A

### Controls
Targetable|Activatable|Reports ready
----------|-----------|-------------
No        |Yes        |No

## Disruptor

```haxe
item1.set_target_to(closest_bot());
```

>Target leading is automatic.

```haxe
if(item1.ready){
	item1.fire();
}
```

>Checking ready makes sure you don't waste energy shooting off in the distance while the turret comes around.

### Description
The disruptor is a ranged energy weapon. While it doesn't deal damage, it temporarily disables the victim, slowing their movement speed, processing speed, and item use for a short time.

While its effect and specs are different, it handles the same as the cannon.

<aside class="success">
Since processing speed is slowed, enemy bots will take much more time to react to the situation in the arena. This includes changing targets, reacting to powerups, and switching on their saw or other items.
</aside>

### Stats
Property    |Value
------------|-----
**Consumes**|Energy
**Cost**    |High
**Range**   |Short
**Accuracy**|High
**Damage**  |N/A
**Weight**  |Low
**Aim Rate**|Fast
**Recoil**  |None
**Cooldown**|Long

### Controls
Targetable|Activatable|Reports ready
----------|-----------|-------------
Yes       |No         |Yes


## Grenade Launcher

```haxe
item1.set_target_to(closest_bot());
```

>Target leading is automatic.

```haxe
if(item1.ready){
	item1.fire();
}
```

>Checking ready makes sure you don't waste ammo shooting off in the distance while the turret comes around.

### Description
The Grenade Launcher fires grenades with a timed fuse. After their fuse expires, grenades explode, dealing damage to all bots within their blast radius, as well as violently pushing them away.

Grenades will bounce off walls and other bots until their fuse runs out.

Additionally, unexploded grenades deal impact damage dependent on their velocity. 

<aside class="notice">
Grenades deal more damage and knockback the closer a bot is to the center of the explosion.
</aside>

<aside class="warning">
You can damage yourself with grenades, even fatally. The damage you deal to yourself is not added to your damage dealt score.
</aside>

### Stats
Property    |Value
------------|-----
**Consumes**|Ammo
**Cost**    |High
**Range**   |N/A
**Accuracy**|High
**Damage**  |High
**Weight**  |Low
**Aim Rate**|Medium
**Recoil**  |Low
**Cooldown**|Long

### Controls
Targetable|Activatable|Reports ready
----------|-----------|-------------
Yes       |No         |Yes


## Saw

```haxe
if(closest_bot().is.close_to(me)){
	item1.activate();
}
else{
	item1.deactivate();
}
```

>It's best not to leave the saw on for too long - it goes through energy very fast!

### Description

The saw is a very powerful melee-range weapon. It uses a lot of energy in exchange for dealing a lot of damage. 

The saw deals damage all around the bot using it, to all bots within range.

Once activated, the saw will continue running until it is either disabled or energy is depleted.

<aside class="success">
If a bot is within <code>close_to</code> range, it is close enough to hit with the saw.
</aside>

<aside class="notice">
The saw rotates clock-wise, and will push bots apart from each other due to the friction of its rotation.
</aside>

### Stats

Property    |Value
------------|-----
**Consumes**|Energy
**Cost**    |High
**Range**   |Melee
**Accuracy**|N/A
**Damage**  |High
**Weight**  |Negligible
**Aim Rate**|N/A
**Recoil**  |N/A
**Cooldown**|N/A

### Controls
Targetable|Activatable|Reports ready
----------|-----------|-------------
No        |Yes        |No


## Shotgun

```haxe
item1.set_target_to(closest_bot());
```

>Target leading is automatic.

```haxe
if(item1.ready){
	item1.fire();
}
```

>Checking ready makes sure you don't waste ammo shooting off in the distance while the turret comes around.

### Description
The Shotgun is a medium-range weapon that fires a spray of projectiles. Since the projectiles spread, and each projectile does only minor damage, it is only effective at short range. If the majority of projectiles find their mark, it will deal devastating damage.

The shotgun only reports `ready` as true when it is on-target, off-cooldown, and has sufficient ammo. You can still fire when off-target, but there is no guarantee you will hit anything.

### Stats
Property    |Value
------------|-----
**Consumes**|Ammo
**Cost**    |Medium
**Range**   |Medium
**Accuracy**|Low
**Damage**  |Very low to very high
**Weight**  |Medium
**Aim Rate**|Medium
**Recoil**  |High
**Cooldown**|Medium

### Controls
Targetable|Activatable|Reports ready
----------|-----------|-------------
Yes       |No         |Yes


## Sniper

```haxe
item1.activate(); 	//The sniper must be powered on to function
item1.target(enemy);
if(item1.ready){	//Unlike the cannon, it won't fire unless ready
	item1.fire(); 
}
```

### Description
The Sniper is a long-range, high-damage, high-cost projectile weapon. Unlike most other turreted weapons, it must be activated in order to function. While the sniper is deactivated, it will not turn to its target or fire. 

While the Sniper is activated, it consumes energy. When energy is expended, you will not be able to use the Sniper even if you have sufficient ammunition.

<aside class='success'>
You can visually confirm that the Sniper is active by its laser sight.
</aside>

### Stats
Property    |Value
------------|-----
**Consumes**|Ammo
**Cost**    |Very high (Firing) Medium (Aiming)
**Range**   |Very long
**Accuracy**|Very high
**Damage**  |Very high
**Weight**  |High
**Aim Rate**|Slow
**Recoil**  |Very high
**Cooldown**|Very long

### Controls
Targetable|Activatable|Reports ready
----------|-----------|-------------
Yes       |Yes        |Yes
