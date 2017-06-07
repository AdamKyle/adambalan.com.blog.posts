On of the things I love to do in my spare time is working with an application known as [RPG Maker MV](http://www.rpgmakerweb.com/).

The main thing I love about this is that I can write Javascript. I am not the best javascript developer in the world, but I do alright,
considering I am employed as a Node JS Developer.

I never use to like Javascript, I use to hate it. JQuery use to make me so mad. Every time I wanted to do something and I couldn't because I didn't know how
or because the language didn't work that way (retuning from callbacks and using the value out side the callback) would make me want to flip a table.

But slowly over time I became accustomed to Javascript. I would watch talks, especially the whole series by [Douglas Crockford](https://www.youtube.com/playlist?list=PL62E185BB8577B63D) and eventually came to understand the language a little more.

It wasn't until I was turned on to React that I fell in love, that and the emerging ES6, I became gitty, even arrogant - Yet I still had no real skills.

When RPG Maker MV came out, I saw the community writing, what we call, plugins. They are Javascript files you include in a plugins directory that can manipulate,
change or even alter the in game experience. You have a lot of power with these scripts. They can be combined to play off each other to bring whole systems, such as the famous [Yanfly Plugins](Yanfly.moe).

I started looking around, before this version of RPG Maker, everything was written in a version of ruby that was usually older and lacking a lot of functionality that would come with the full fledged version of ruby.

With MV, that all changed, they allowed amateurs to mess around with Javascript. Some every good, and others ... Horrible. Complete Garbage.

That is not indicative of the whole community, a vast majority, but not the whole.

With Javascript came the ability to write ES6, if you wanted to directly affect core API's by over writing them you still had to do things like:

```js
/**
 * Add a indicator and set it to visible.
 */
let LucidEventIcon_Game_System_initialize = Game_System.prototype.initialize;
Game_System.prototype.initialize = function() {
  LucidEventIcon_Game_System_initialize.call(this);
  lucidScripts.lucidEventIcon.needRefresh = true;
};
```

This would directly override the Game_System's initialize function while keeping the original functionality intact for other scriptors or to not out right break the game.

This is where scripts can get messy, you never know who's overriding who and what and this can lead to some real issues with compatibility. Not to mention all of this in global scope, so you can go into the console and access any of these classes or some variables via `$`, for example:

```js
$gameActors.actor(1).currentClass();
```

Run in a script command in the game on an event or in the console, gives you that characters class object.

What's nice about this release is that they have released the Javascript code that is the "core" foundation on [Github](https://github.com/rpgtkoolmv/corescript).

## My adventures in this land

So what does this have to do with me? Well I am making a game, and not only that some times I see specific scripts I would want but cannot use because they are so poorly written and so badly broken that I end up [writing my own](https://github.com/AdamKyle/lucid-scripts). Again, not saying I am better then them, but I think I have some experience.

With my scripts, I included the `dist/` directory for people to be able to get the scripts easily or for me to be able to easily share them on the official forums.

I managed to use Web pack to build them scripts and a couple node scripts to append a specific header to the `dist` script to allow you, in the Game Editor, to see details about the script it's self and what it does.

I am quite proud of my work, but also fearful of having this repository up on my personal Github because I could become the laughing stalk of not just the Javascript community but the employment world should I choose to leave my current position. I can hear the laughter of "Script Kiddie" now.

But I share this with you, the reader, because there is a world out there thats beyond Ember, React, Angular and other such technologies. It is niche and relatively unknown but it does exist and I thought I would share it with you, even if I do become the laughing stalk.

It is a great hobby to have, and I have even learned a few things a long the way that I did not know previously. So I guess to every story is a silver ligning.
