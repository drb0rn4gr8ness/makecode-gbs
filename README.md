# Code Ninjas Evans GBS

### @diffs true

## Introduction @showdialog

Today we are going to be building a space blaster game! You will have to dodge and blast asteriods as you flying your rocketship through space.
The coolest part about all of this is that you will be creating everything with code.

Are you ready to get started?

## Setting Up Our Game

When users player our game we want to make sure they all get the same experience. We can make sure this happens by doing a little setup when the game starts.

1. **Set our background image**  
   drag a `|| scene: set background image to [] ||` block inside the `||loops: on start ||` block.

2. **Initialize Our Score**  
   set our score to 0 by adding a `||info: set score to (0) ||` block.

3. **Initialize Our Lives**  
   set our lives to 3 by adding a `||info: set life to (3) ||` block.

```blocks
scene.setBackgroundImage(storySprites.world)
info.setScore(0)
info.setLife(3)
```

## Creating our Rocketship

Our star of the show is our RocketShip.

1. **Creating the Sprite**  
   add a `||sprites: set [mySprite] to sprite [] of kind (Player)||` block
2. **Rename Our Sprite**  
   Click mySprite and choose `Rename variable...`. Let's rename it to `rocketShip`.
3. **Choose the Sprite Image**  
   Choose the Airplane from the Gallery. Once you see the image in the Editor tab, use the `Flip Horizontal` button to make it face to the right.
4. **Choose the Sprite Kind**  
   Leave the kind as `Player`

```blocks
let rocketShip: Sprite = null
scene.setBackgroundImage(storySprites.world)
info.setScore(0)
info.setLife(3)
rocketShip = sprites.create(img`
    ..............ffffff....
    ..fc.........fccc2ff....
    ..f4c.....fffccc2ff.....
    ..f44ccccc22222222cc....
    ..f244ccc222224442b9c...
    ..cf24222222222244999c..
    .ccf2222222222222199b2c.
    fc22cc22222222b1111b222c
    f22ccccccc2222991222222f
    ffffffc222c22222222222f.
    ....ff222244c2222222ff..
    ...cf222244fffffffff....
    ...c222244ffc2f.........
    ...c2222cfffccf.........
    ...ffffffff2cf..........
    ........fff2c...........
    `, SpriteKind.Player)
```

## Rocketship Movement...

Now we need to set the rocketship's position, make it respond to our movement buttons, and stay within the screen.

1. **Set the Position**  
   add a `||sprites: set [mySprite] position to x (0) y (0)||` block. Change mySprite to rocketShip and adjust the 'x' and 'y' to place the airplane on the left side of the screen.
2. **Enable Movement With Buttons**  
   add a `||controller: move [mySprite] with buttons||` block and change mySprite to rocketShip.
3. **Set to Stay in Screen**  
   add a `||set [mySprite] stay in screen <ON>||` block and change mySprite to rocketShip and make sure the toggle says `ON`.

```blocks
let rocketShip: Sprite = null
scene.setBackgroundImage(storySprites.world)
info.setScore(0)
info.setLife(3)
rocketShip = sprites.create(img`
    ..............ffffff....
    ..fc.........fccc2ff....
    ..f4c.....fffccc2ff.....
    ..f44ccccc22222222cc....
    ..f244ccc222224442b9c...
    ..cf24222222222244999c..
    .ccf2222222222222199b2c.
    fc22cc22222222b1111b222c
    f22ccccccc2222991222222f
    ffffffc222c22222222222f.
    ....ff222244c2222222ff..
    ...cf222244fffffffff....
    ...c222244ffc2f.........
    ...c2222cfffccf.........
    ...ffffffff2cf..........
    ........fff2c...........
    `, SpriteKind.Player)
rocketShip.setPosition(10, 65)
controller.moveSprite(rocketShip)
rocketShip.setStayInScreen(true)
```

## You Did It! @showdialog

Congratulations on completing the rocketship!

Let your Sensei know how you're feeling. Is this easier or harder than you thought?

Let's move on to the next topic: **Events**

## Introducing Events @showhint

Our next bit of code will be placed inside a type of event block. Event blocks **listen** for certain things to happen.

There are events available to run code when sprites overlap, collide, are created, or destroyed. Also, you can use events to take action when buttons are pressed or when game counts reach zero.

## On Game Update Event @showhint

We will use several events today but the first one is the `||game: on game update every <Interval> ||` event. This event allows us to create a **EventListener** that will run whatever instructions we put inside at a specific interval.
In other words it waits for a specified time to elapse and then runs our instructions.

## Configure our Asteroids

Make asteroids generate every second...

```blocks
let asteroid: Sprite = null
game.onUpdateInterval(1000, function () {
    asteroid = sprites.create(sprites.space.spaceAsteroid0, SpriteKind.Enemy)
    asteroid.setVelocity(-100, 0)
    asteroid.setPosition(160, randint(10, 100))
    asteroid.setFlag(SpriteFlag.AutoDestroy, true)
})
```

## Configure Player to Enemy Collision

Set the player to lose a life when they collide with an asteriod.

```blocks
sprites.onOverlap(SpriteKind.Player, SpriteKind.Enemy, function (sprite, otherSprite) {
    scene.cameraShake(4, 200)
    info.changeLifeBy(-1)
})
```

## Configure our Lasers

Set the rocketship to shoot lasers when you press the 'A' button.

```blocks
let projectile: Sprite = null
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    projectile = sprites.createProjectileFromSprite(sprites.projectile.explosion1, rocketShip, 100, 0)
    music.play(music.melodyPlayable(music.pewPew), music.PlaybackMode.UntilDone)
})
```

## Configure Projectile to Enemy Collision

Set the Asteroids to be destroyed when they collide with the rocketship's lasers.

```blocks
sprites.onOverlap(SpriteKind.Projectile, SpriteKind.Enemy, function (sprite, otherSprite) {
    sprites.destroy(otherSprite, effects.warmRadial, 100)
    music.play(music.melodyPlayable(music.knock), music.PlaybackMode.UntilDone)
    info.changeScoreBy(1)
})
```

## Introducing Conditionals @showhint

Describe conditionals here!

## Adding Hearts/ Powerups

Add a bit of randomness by sometimes generating an asteriod and sometimes generating a heart

```blocks
let generatedItem: Sprite = null
game.onUpdateInterval(1000, function () {
    if (randint(0, 100) <= 10) {
        generatedItem = sprites.create(sprites.skillmap.decoration7, SpriteKind.Food)
    } else {
        generatedItem = sprites.create(sprites.space.spaceAsteroid0, SpriteKind.Enemy)
    }
    generatedItem.setVelocity(-100, 0)
    generatedItem.setPosition(160, randint(10, 100))
    generatedItem.setFlag(SpriteFlag.AutoDestroy, true)
})
```

## Configure Player to Food Collision

Add a life to the player when they collide with a heart.

```blocks
sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (sprite, otherSprite) {
    info.changeLifeBy(1)
    music.play(music.melodyPlayable(music.powerUp), music.PlaybackMode.UntilDone)
})
```
