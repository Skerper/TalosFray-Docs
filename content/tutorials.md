---
weight: 12
title: Tutorials
---

# Tutorials

## Introduction

So you want to make a fighting robot? Well, you've come to the right place! This series of tutorials should get you up and running with a bot in no time.

Firstly, some technical details about bot battles.

### Your Bot

Your bot consists of a main body, a display (on which your Twitch avatar is shown), four slots for items, and a CPU. The main body is circular, and takes care of movement. If your main body is destroyed, your bot is destroyed.


### Your Program
You control your bot by writing a program for it to follow. Essentially, you're teaching your bot to fight, by giving it an AI. 

The CPU doesn't have direct knowledge of the outside world, nor does it have direct control of your bot's hardware. 60 times a second, it receives an information pack about the battlefield, and at the same time, it sends any commands you've made to the bot's hardware.

Don't worry about writing complicated targeting or manoeuvring routines using math and so on; this isn't that kind of game. Things like target leading and pathfinding are dealt with by hardware outside of the CPU, with every bot having equal footing in those regards. Your program's chief job is to determine your bots's *strategy*. Who to target, what to use, where to go, and so on.

Rather than min-maxing numbers or trying to build the best targeting algorithm, your job is to use the information at hand to make the optimal strategy against any other bot you may come up against.

### Battles
Battles take place in the arena, and can be watched on [Twitch](http://twitch.tv/talosfray). Everyone watches the same battle. 

Battles are free-for-all, and the last bot standing wins. If a battle takes too long to end, the surviving bot that has dealt the most damage will be judged the winner. In the case of a tie, all bets are cancelled and the round is not recorded.


### Items
Your bot can hold up to four items, be they for attack, defense, or manoeuvring. Items have differing weight, and the more you carry, the slower your bot will move.


### This Document
```haxe
//Over here! This is where code examples will be!
```
> And this is where advice about the code goes.

In the following tutorials and documentation, you'll be given code examples to try on your bot. Information will be in the middle column (which you're reading right now), while code examples will be in the column to your right.

Additional hints and tips will be given in the following formats;
<aside class='success'>
This green box for tips, tricks, and good-to-know information.
</aside>
<aside class='notice'>
This blue box for extra details and technical explanations.
</aside>
<aside class='warning'>
This red box for warnings, cautions, and gotchas. 
</aside>


### Who are these tutorials for?
If you have little to no programming experience, these tutorials are the right place to start. If you already have a grasp of programming concepts, you might want to skip past the tutorials and just read the API.

However, even if you are a beginner programmer, please note that this is not 'programming 101'. You should first read up on the many tutorials and resources available on concepts such as variables, control structures, and so on. The language used here is hscript, essentially haxe, but concepts learned from Java, Javascript, Actionscript, PHP, C++, and so on, will all apply.


## 1. Getting Started
Enough talk, let's get started!


### Registration
This game is integrated with [Twitch.tv](http://twitch.tv). You will need a free Twitch account to play. Once you have registered on Twitch, you can log in to your bot dashboard with your Twitch account. 

<aside class='success'>
Worried about your Twitch credentials? Don't be! As you will see when you log in, you only ever enter your username and password on Twitch.tv. We have no access to any information that you don't actively agree to give us! Not even your email address. 
</aside>


### Installation
No software is required to play this game; you can log in to [your dashboard](http://talosfray.tv/) with your Twitch account, make your bot, and watch the battles on [Twitch](http://twitch.tv/talosfray) entirely in your browser.

You can test your bot code in the emulator, which can be seen to the right of the code editor on your dashboard.


### Your First Bot
Logging in to the [dashboard](http://talosfray.tv/), you will see that some placeholder code has already been filled out for you, and that your bot has one item - a cannon - installed. 

<aside class='notice'>
You will notice that the `activate` checkbox is left unchecked. Your bot will not appear in battles unless this box is checked, and save is clicked. This is so your half-finished bot doesn't get annihilated before you can even test it! Feel free to deactivate your bot whenever you want to work on it. 
</aside>

```haxe
//Pre-battle stuffs goes here
			

while(true){
	//Sneeky taktix go here  
}
```

As you can see on the right, the placeholder code is rather empty. The lines beginning with `//` are comments, and have no bearing on the bot's operation. All that leaves is the `while(true)` loop, which those with programming experience will know is an endless loop; it will simply repeat the commands inside the curly brackets ad absurdum.

Why an endless loop? Put simply, **if your program ends or crashes, your bot will die. It must continue running for the duration of the battle.**


### Do something!!
```haxe 
//Pre-battle stuffs goes here
var enemy = random_bot(); 	//select a random bot
set_target_to(enemy); 		//point our weapons at it
set_destination_to(enemy);	//move towards it

while(true){
	item1.fire(); 			//Fire the cannon!
}
```

As it is now, your bot will simply sit in the corner until somebody puts it out of its misery. Let's make it do something. 

Have a look at the example code. This is an extremely simple control routine for your bot. All it does is pick a random bot, and move towards them while firing at them.

We stored `random_bot()` in the `enemy` variable so that we could target and move towards the same bot. If we'd written the code like the second example on the right, we may have ended up moving towards one bot while targeting another!

<aside class='notice'>
The global variable item1 contains the control interface for the item in slot 1. If you moved your cannon to, for example, slot 3, you would have to use item3 instead to control it.
</aside>

> Bad example - not storing our randomly selected bot:

```haxe
set_target_to(random_bot());		//Set target to a random bot
set_destination_to(random_bot());	//No guarantee it's the same bot!
```

<aside class='success'>
It's a pain to write out <code>set_target_to</code> and <code>set_destination_to</code> all the time. If you're sick of it, you can just use the shorthand <code>target</code> and <code>destination</code> instead.
</aside>


### Testing
You can test this bot either by activating it and entering it in a battle, or by loading up a target dummy scenario in the editor. 

<aside class='notice'>
To enter your bot in a battle, first ensure that it is activated, then say <code>!menext</code> in the Twitch chat while logged in. You will be entered in the queue to battle. Don't forget to say `!start` to start the stream if it's not currently live!
</aside>

As you will see, this bot is not terribly effective. It charges towards the enemy, wasting ammunition firing before its turret is even facing the target, and will likely be quickly slaughtered by close-quarter weapons before it can deal any significant damage.

But hey, it's a start!


## 2. Thinking Smarter
The control code we wrote in tutorial 1 works, but just barely. As far as artificial intelligence goes, it's very weak on the 'intelligence' front. It's unlikely that it will ever win a battle!


### Analysis
There are two main problems with our previous bot. 1) it's wasteful, and 2) it has no sense of self-preservation.

There are many other problems - especially regarding things it *should* do but doesn't. But these are the two big issues with what it *does* do, which is shoot at an enemy.


### Improvement

> This reads "If item1 is ready and the enemy is in medium range to me, fire item1."

```haxe
if(item1.ready && enemy.medium_range_to(me)){
	item1.fire();
}
```

Regarding wastefulness, it makes sense to only fire your cannon when there's a reasonable chance it will hit its target. Checking the [documentation for the cannon](#cannon) tells us that it 'reports ready' when it's pointing at the target, and that it has 'medium' effective range.

As such, we can best expect to hit the enemy when we're within medium range, and the cannon says it's ready. 

We can check these conditions with `if` statements, as shown on the right.

<aside class='notice'>
'<code>&&</code>' is read 'and'. This is called a 'logical operator'.
</aside>

>Which gives us our final control code: 

```haxe
var enemy = random_bot(); 	//select a random bot
set_target_to(enemy); 		//point our weapons at it
set_destination_to(enemy);	//move towards it
keep_medium_distance(); 	//maintain cannon range
while(true){	
	if(item1.ready && enemy.medium_range_to(me)){
		item1.fire();       //Fire! But only when ready.
	}
}
```

Next, the self-preservation issue. It stands to reason that you should never be closer to an enemy than you need to be! You can tell your bot to maintain a certain distance to the enemy.

Since our weapon has medium range, it makes sense to maintain medium distance. We can do this before the `while` loop, since we only need to say it once.


### Testing
Loading up this bot will show it to be markedly more competent than the previous iteration! It will still struggle to make an impact in battles though, as I'm sure you can imagine.


## 3. Switching Targets
```haxe
if( !enemy.alive ){				//If the enemy has expired
	enemy = random_bot();		//Pick another at random
	set_destination_to(enemy);	//again, move towards them
	set_target_to(enemy);		//again, target them
	keep_medium_distance();		//again, maintain cannon range
}
```

In tutorial 2, we wrote a bot that will maintain an appropriate range to its target while shooting at it. As you may have noticed, though, once its target is dead, it just continues shooting at it until it runs out of ammunition. This is not a great strategy, because there are likely to be other bots that need shooting. 

Obviously, what we need to do is to change targets once our enemy is defeated. We can do this by checking on our enemy's welfare. A simple method is to check our enemy's `alive` property. We can't be sure we were the one who killed a bot with `alive` set to `false`, but we can at least be certain that that bot is dead, and that it's time to pay our respects and move on.

> The check, implemented

```haxe
var enemy = random_bot(); 			//select a random bot
set_target_to(enemy); 				//point our weapons at it
set_destination_to(enemy);			//move towards it
keep_medium_distance(); 			//maintain cannon range
while(true){	
	if( !enemy.alive ){				//If the enemy has expired
		enemy = random_bot();		//Pick another at random
		set_target_to(enemy);		//again, target them
		set_destination_to(enemy);	//again, move towards them
		keep_medium_distance();		//again, maintain cannon range
	}
	if(item1.ready && enemy.medium_range_to(me)){
		item1.fire();      			//Fire! But only when ready.
	}
}
```

The code to the right is best placed within our `while(true)` main loop, so that we check each time cycle whether the enemy has been defeated.


### Testing
Try selecting a two- or four-target scenario in the emulator. You'll see that after the first target is killed, your bot will dutifully begin dismantling a different target.

<aside class='success'>
This is the first bot we've written that may have a chance at winning a round, as it will continue fighting against any living enemy. As long as it has ammunition, it has a chance!
</aside>

If you enter your bot in some battles and watch how it performs, you might start getting ideas as to how you can improve its strategy. By all means, try them out! There is no need to rigidly follow these tutorials line-by-line; you will learn far quicker by experimenting. 

<aside class='notice'>
If your bot keeps dying right at the start of a round, or when it still has HP, it likely has some kind of error that is causing your control program to crash. Your best bet is to run it in the emulator, and read the error message that comes out!
</aside>

### Improvement 
```haxe
function selectEnemy(){
	var new_enemy = random_bot(); 	//select a random bot
	set_target_to(new_enemy); 		//point our weapons at it
	set_destination_to(new_enemy);	//move towards it
	keep_medium_distance(); 		//maintain cannon range
	return new_enemy;				//Return the new enemy for storage
}
var enemy = selectEnemy();			//Get our first enemy
while(true){	
	if( !enemy.alive ){				//If the enemy has expired
		enemy = selectEnemy();		//Get a new enemy
	}
	if(item1.ready && enemy.medium_range_to(me)){
		item1.fire();      			//Fire! But only when ready.
	}
}
```

As you may have noticed from the comments, having to type the same commands out multiple times is a drag. If you find yourself reusing code, it might be a good idea to make functions! 

Functions are bundles of code that can be called from anywhere. You will probably recognise that in hscript, they're essentially identical to javascript.

The example on the right is not the neatest way to use a function, but it will suit our needs for now. As you can see, we've collected our enemy-selecting code into one place. Now, we can replace that code in our control program with calls to the function. 

<aside class='success'>
You have to declare functions before you can use them!
</aside>