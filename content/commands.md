---
weight: 20
title: Commands
---

# Commands

These are functions that are available anywhere in your botcode.


## advance()
```haxe
var enemy = closest_bot(); 	//Select the nearest active bot (Could be yourself...!)
set_destination_to(enemy); 	//The enemy is our destination
advance();					//Charge!
```
`advance` sets your bot to move towards whatever is set as its destination.
<aside class="notice">
<code>advance</code> is the default behavior of the bot, so you don't need to call it unless you've previously told it to do something other than <code>advance</code>.
</aside>

<aside class='warning'>
Using <code>advance</code>, <code>retreat</code>, <code>stop_moving</code>, or changing destination with <code>set_destination_to</code> or <code>destination</code> will cancel any <code>keep distance</code> commands.
</aside>


## bot_named(name)
```haxe
var enemy = bot_named("SkerpSkerp");
if(enemy!=null){
	set_target_to(enemy);
}
```
`bot_named` allows you to select a bot by Twitch display name.

Argument|Description
--------|-------------
name    |A `String` representing the name of the bot you are searching for.

Returns     |Description
------------|-------------------------------------------------------
`Bot`		|The `Bot` with the name specified, or `null` if that bot is not alive or in the round. 

<aside class="success">
This function can be used both for team play, and for bullying people. How wonderful!
</aside>

<aside class="warning">
It's very important to check whether this function returned <code>null</code> before trying to use it. If you try to use a <code>null</code> bot, your bot will crash and you will lose the round.
</aside>


## bot_who_damaged_me()
```haxe
var enemy = bot_who_damaged_me();
if(enemy != null){
	log("I will have my revenge!");
}
```
> Be sure to check for null!

```haxe
//BAD EXAMPLE
if(bot_who_damaged_me() != null){
	target(bot_who_damaged_me());
	destination(bot_who_damaged_me());
}
```
> At some point in the above example, it is likely that bot_who_shot_me will start returning null, which will crash your bot and forfeit the round.

Returns a [`Bot`](#bot) reference to the bot who most recently dealt damage to you. Once checked, this is cleared, and will return `null` until you are damaged again.

Returns     |Description
------------|-------------------------------------------------------
`Bot`		|The `Bot` who just damaged us, or `null` if we have not been damaged, or already checked since being damaged. 

<aside class='warning'>
Using `bot_who_damaged_me` clears the record of you being damaged. As such, it is important to store the result, and use the stored result to perform any further operations.
</aside>

<aside class='notice'>
This includes bots who have dealt a non-damaging status effect to your bot, such as the EMP effect from a Distruptor round.
</aside>


## closest_bot()
```haxe
var enemy = closest_bot();	//The variable enemy now contains the nearest living bot. It could be ourselves!
```
Gets the nearest not-dead bot to your bot. 

Returns     |Description
------------|-------------------------------------------------------
`Bot`		|The `Bot` of the nearest living bot to your bot. 

<aside class="notice">
If you are the only bot left alive, this will return a <code>Bot</code> of yourself!
</aside>

## closest_projectile()
```haxe
if(closest_projectile().will_hit(me)){
	log("we're doomed");
}
```

Gets a [`Projectile`](#projectile-type) reference to the nearest projectile fired by an enemy. Returns `null` if there are no enemy projectiles in the arena.

Returns     |Description
------------|-------------------------------------------------------
`Projectile`|The `Projectile` of the nearest enemy projectile to your bot.
 

## destination(target)

Argument|Description
--------|-------------
target  |Any object with an `id:Int` field. `Bot`s, directions (`LEFT`, `UP`, etc), sectors (`SECTOR3` etc) all work.

<aside class="notice">
This is just an alias of <code>set_destination_to</code> to make typing quicker.
</aside>


## keep_long_distance()

```haxe
var enemy = random_bot();
set_destination_to(enemy);
keep_long_distance();
```

Maintains a long distance to the target.

<aside class='warning'>
Using <code>advance</code>, <code>retreat</code>, <code>stop_moving</code>, or changing destination with <code>set_destination_to</code> or <code>destination</code> will cancel any <code>keep distance</code> commands.
</aside>


## keep_medium_distance()

```haxe
var enemy = random_bot();
set_destination_to(enemy);
keep_medium_distance();
```

Maintains a medium distance to the target.

<aside class='warning'>
Using <code>advance</code>, <code>retreat</code>, <code>stop_moving</code>, or changing destination with <code>set_destination_to</code> or <code>destination</code> will cancel any <code>keep distance</code> commands.
</aside>


## keep_medium_long_distance()

```haxe
var enemy = random_bot();
set_destination_to(enemy);
keep_medium_long_distance();
```

Maintains a medium-long distance to the target.

<aside class='warning'>
Using <code>advance</code>, <code>retreat</code>, <code>stop_moving</code>, or changing destination with <code>set_destination_to</code> or <code>destination</code> will cancel any <code>keep distance</code> commands.
</aside>


## keep_short_distance()

```haxe
var enemy = random_bot();
set_destination_to(enemy);
keep_short_distance();
```

Maintains a short distance to the target.

<aside class='warning'>
Using <code>advance</code>, <code>retreat</code>, <code>stop_moving</code>, or changing destination with <code>set_destination_to</code> or <code>destination</code> will cancel any <code>keep distance</code> commands.
</aside>


## keep_very_short_distance()

```haxe
var enemy = random_bot();
set_destination_to(enemy);
keep_very_short_distance();
```

Maintains a very short distance to the target.

<aside class='warning'>
Using <code>advance</code>, <code>retreat</code>, <code>stop_moving</code>, or changing destination with <code>set_destination_to</code> or <code>destination</code> will cancel any <code>keep distance</code> commands.
</aside>


## log(anything)
```haxe
log("Hello World!");	//Logs "Hello World!" to the debug output box
```

Used for debugging your bot with the Testbed, this will output whatever you enter as an argument to the debug output box, as well as the line number that you called it from.

Argument|Description
--------|-----------
anything|You can really put just about anything here. If it's not text, the bot will attempt to turn it into text somehow.

<aside class="warning">
Even though this does not do anything during actual battles, it will still waste CPU cycles! Best to comment it out when you're not testing.
</aside>


## lowest_ammo_bot()
```haxe 
var enemy = lowest_ammo_bot();
```

Selects the bot with the lowest remaining ammo. Will only return your own bot if there are no other living bots.

Returns     |Description
------------|-------------------------------------------------------
`Bot`		|The `Bot` with the lowest ammo


## lowest_energy_bot()
```haxe 
var enemy = lowest_energy_bot();
```

Selects the bot with the lowest remaining energy. Will only return your own bot if there are no other living bots.

Returns     |Description
------------|-------------------------------------------------------
`Bot`		|The `Bot` with the lowest energy


## lowest_hp_bot()
```haxe 
var enemy = lowest_hp_bot();
```

Selects the bot with the lowest remaining hp. Will only return your own bot if there are no other living bots.

Returns     |Description
------------|-------------------------------------------------------
`Bot`		|The `Bot` with the lowest hp


## random_bot()
```haxe
var enemy = random_bot();
```

Gets a reference to a random not-dead bot. It will not return your own bot unless all other bots are dead.

Returns     |Description
------------|-------------------------------------------------------
`Bot`		|The `Bot` of a randomly-selected living bot. 


## random_int(max)
```haxe
set_destination_to(random_int(9)); //sets the destination to a random sector
```

Returns a pseudo-random integer between 0 and `max`, inclusive. 

Argument|Description
--------|-------------
max     |A positive integer.

<aside class="warning">
When <code>max</code> is negative, the behaviour is undefined.
</aside>

## retreat()
```haxe
var enemy = closest_bot(); 	//Select the nearest active bot (Could be yourself...!)
set_destination_to(enemy); 	//The enemy is our destination
retreat();					//Run away!
```
`retreat` moves your bot away from the set destination. It will not make any attempt to avoid backing into walls, etc.

<aside class='warning'>
Using <code>advance</code>, <code>retreat</code>, <code>stop_moving</code>, or changing destination with <code>set_destination_to</code> or <code>destination</code> will cancel any <code>keep distance</code> commands.
</aside>

## set_destination_to(target)
```haxe
set_destination_to(SECTOR1);	//Destination will be the top-left sector.
```
Sets the destination of the bot's movement to 'target'. 

Argument|Description
--------|-------------
target  |Any object with an `id:Int` field. `Bot`s, directions (`LEFT`, `UP`, etc), sectors (`SECTOR3` etc) all work. The integers 1-9 also work, representing the sectors 1-9.

<aside class="notice">
This doesn't necessarily mean your bot will move towards the destination - using commands like <code>strafe_left()</code> will make it move differently *relative* to the target area.
</aside>

<aside class='warning'>
Using <code>advance</code>, <code>retreat</code>, <code>stop_moving</code>, or changing destination with <code>set_destination_to</code> or <code>destination</code> will cancel any <code>keep distance</code> commands.
</aside>

## set_target_to(target)
```haxe
var enemy = closest_bot(); 	//Select the nearest active bot (Could be yourself...!)
set_target_to(enemy);		//Bring all items to bear!
```
Sets the target of all aimable items your bot is equipped with to 'target'. Target is any object with an `id:Int` field.

Argument|Description
--------|-------------
target  |Any object with an `id:Int` field. `Bot`, directions (`LEFT`, `UP`, etc), sectors (`SECTOR3` etc) all work. The integers 1-9 also work, representing the sectors 1-9.

## set_sleep_timer(seconds)
```haxe
set_sleep_timer(2.5);
sleep_until(TIMER); //sleep for 2.5 seconds
```

Sets the time to be used when you call `sleep_until` with the `TIMER` argument. 

Argument    |Description
------------|-------------
seconds     |A positive Float giving the time to sleep in seconds.

<aside class='info'>
The sleep timer setting is never cleared - if you call <code>sleep_until(TIMER)</code> twice after calling <code>set_sleep_timer(2.5)</code> once, you will sleep for 5 seconds in total.
</aside>

<aside class='warning'>
Setting the sleep timer doesn't do anything unless you also call <code>sleep_until</code> with the <code>TIMER</code> argument!
</aside>


## set_throttle(percentage)
```haxe
set_throttle(50); //move at 50% speed
```
Sets your bot to move with a different percentage of its available acceleration.

Argument    |Description
------------|-------------
percentage  |An integer between 0 and 100 representating a percentage number of power output.


## sleep_until(code)
```haxe
sleep_until(UPDATE); //Sleep until we get information from the arena
log("good morning!"); //Will only get to hear when an update has arrived
```

>Your bot only gets updates 60 times a second, so you can save energy not acting on the same data twice.

```haxe
set_sleep_timer(5); //set sleep timer for 5 seconds
sleep_until(POWERUP_APPEARS|TIMER); //sleep until either the timer runs out or a powerup appears
```

>Prevent waiting too long for an event by also setting a timer. 

`sleep until` pauses the CPU until the specified conditions are met. 

Argument    |Description
------------|-------------
code	    |A bit field. Bit values are defined in constants (TIMER, UPDATE, etc).

<aside class='info'>
You can set multiple wake conditions using bitwise or (|). For example, to wake on UPDATE or POWERUP_APPEARS, use <code>sleep_until(UPDATE|POWERUP_APPEARS)</code>.
</aside>


## stop_advancing()
```haxe
stop_advancing();
```
Stops the bot moving towards the destination. It will now sit still unless strafing.


## stop_moving()
```haxe
stop_moving();
```
Stops all movement (strafing and retreating/advancing) in one command. The bot will stop still.

<aside class='warning'>
Using <code>advance</code>, <code>retreat</code>, <code>stop_moving</code>, or changing destination with <code>set_destination_to</code> or <code>destination</code> will cancel any <code>keep distance</code> commands.
</aside>


## stop_retreating()
```haxe
stop_retreating();
```
An alias of `stop_advancing`.


## stop_strafing()
```haxe
stop_strafing();
```
Cancels any left or right strafing movement.


## strafe_left()
```haxe
var enemy = closest_bot(); 	//Select the nearest active bot (Could be yourself...!)
set_destination_to(enemy); 	//The enemy is our destination
strafe_left();				//Orbit clockwise
```
`strafe_left` moves the bot clockwise around the set destination. It makes no attempt to maintain current range.


## strafe_right()
```haxe
var enemy = closest_bot(); 	//Select the nearest active bot (Could be yourself...!)
set_destination_to(enemy); 	//The enemy is our destination
strafe_left();				//Orbit counter-clockwise
```
`strafe_right` moves the bot counter-clockwise around the set destination. It makes no attempt to maintain current range.


## target(target)

Argument|Description
--------|-------------
target  |Any object with an `id:Int` field. `Bot`s, directions (`LEFT`, `UP`, etc), sectors (`SECTOR3` etc) all work.

<aside class="notice">
This is just an alias of <code>set_destination_to</code> to make typing quicker.
</aside>


## woke_on()
```haxe
set_sleep_timer(10);					//set sleep timer for 10 seconds
sleep_until(POWERUP_APPEARS|TIMER); 	//sleep until timer or powerup
switch(woke_on()){ 						//if we woke on...
	case POWERUP_APPEARS:  				//a powerup
		log("Woo, powerup!"); 			//do this
	case TIMER:     					//a timer
		log("I'm sick of waiting..."); 	//do this
}
```

Gets the `SleepCode` that we last came out of a `sleep_until` on.

Returns     |Description
------------|-------------------------------------------------------
SleepCode	|A SleepCode, such as POWERUP_APPEARS or UPDATE

<aside class='success'>
Using <code>woke_on</code> allows you to quickly change behaviour to suit the conditions after sleeping on multiple conditions.
</aside>