# Code Ninjas Evans GBS

### @diffs true

```template
scene.setBackgroundColor(9)

forever(function() {

})


sprites.onOverlap(SpriteKind.Player, SpriteKind.Projectile, function (sprite, otherSprite) {

})


controller.A.onEvent(ControllerButtonEvent.Pressed, function () {

})

game.onUpdateInterval(1000, function () {

})

function flap (bird: Sprite) {
  bird.vy = -50
  pause(200)
  bird.vy = 50
}

function createTrees() {
  let topTree: Sprite = null
  let bottomTree: Sprite = null
  topTree = sprites.createProjectileFromSide(sprites.duck.log7, -50, 0)
  topTree.setPosition(160, randint(0, 25))
  bottomTree = sprites.createProjectileFromSide(sprites.duck.log3, -50, 0)
  bottomTree.setPosition(160, randint(115, 140))
}
```

## Welcome to Code Ninjas Evans! 👋 @showdialog

We are so excited that you decided to come and code with us today. We are going to be building a very fun and only slightly addicting bird game. You may have played a game very similiar to it before but even if you haven't we are going to explain everything and make sure you have everything you need to be successful today.

Ok, Are you ready to get started?

## Initializing our Game

~hint What does initializing mean?

- :book: Initializing is a fancy word that simply means "Initial Set Up." We are going to set some defaults and perform setup actions to make sure our game starts the same way every time!

hint~

- :paint brush: **Add Background Color**: Set a background color by clicking on circle `|| scene: set background color ||` block that is currently inside the `||loops: on start ||` block.
- :setting: **Add Background Effects**: Let's add an effect to our background by adding a `|| scene: start screen effect ||` block.
- :heart: **Reset our Lives**: We want each player to start the game with the same amount of lives. We can set this with the `|| info: set life to  ||` block.
- :trophy: **Reset our Score**: We want each player to start the game with a score of 0. We can set this with the `|| info: set score to ||` block

```blocks
scene.setBackgroundColor(9)
effects.blizzard.startScreenEffect()
info.setLife(3)
info.setScore(0)
```

## Create Our Bird Sprite

- :plus: **Create Bird Sprite**: Create the bird sprite by adding a `|| variables(sprites):set mySprite to ||` block. Make sure to create a _New Variable_ for the **Name**, set the **Image** for the bird, and set _Player_ for the **Name**.
- :marker: **Set Bird Position**: Set a starting **Position** for the bird with `|| spirites: set mySprite position to ||`

```blocks
scene.setBackgroundColor(9)
effects.blizzard.startScreenEffect()
info.setLife(3)
info.setScore(0)
let bird: Sprite = null
bird = sprites.create(sprites.duck.duck1, SpriteKind.Player)
bird.setPosition(25, 50)
```

## Adding Gravity to the Bird

We want the bird to be continuously falling unless we tell the bird to flap. we simulate gravity by setting the velocity of our sprite.

- :move: **Move Our Bird**: We make our sprite move by adding a `|| sprites: set mySprite velocity ||` block.

~hint Critical Thinking Time 🤔

- :question: Can you guess if we will be changing the **Velocity X** or **Velocity Y** property to make the bird fall?
- :lab: Try playing with the numbers to see if you can figure out what makes the bird fall slower or faster.
- :pin: How do we keep our bird from going off the screen of our game? We will answer this one later!

hint~

```blocks
scene.setBackgroundColor(9)
effects.blizzard.startScreenEffect()
info.setLife(3)
info.setScore(0)
let bird: Sprite = null
bird = sprites.create(sprites.duck.duck1, SpriteKind.Player)
bird.setPosition(25, 50)
bird.setVelocity(0, 50)
```

## You Did It! 🔥 @showdialog

🎉 Congratulations on completing the bird! 🎉

- :check: Let your Sensei know how you're feeling! Is this easier or harder than you thought?

Let's move on to the next topic: **Events**

## Introducing Events @showhint

The next code we write will be placed inside an event block. Event blocks **listen** for certain events and run your code when it identifies the event has occurred.

~hint Wait! Where do these events come from?

- :play: Actions **trigger** events. Action can include things like sprites overlapping, colliding, and being created or destroyed. Also, users pressing buttons or even properties reaching 0 like the number of lives.

hint~

The MakeCode® Arcade platform takes care of triggering events automatically. However, our event blocks tell our game to listen for these events and run our code when they occur.

## OnEvent Events @showhint

We will use several events today but the first one is the `|| controller: on [A] button [pressed] ||` event. This event allows us to create a **EventListener** that will run our code every time the **A** button is pressed.

## Moving with the A Button

We want our bird to move when we press the **A** button. For this there is a function called **flap** that has already been created for you. We want to **call** this function inside of our `|| controller: on [A] button [pressed] ||` event block.

~hint What is a function again 😕?

- :info: A function is a group of code that is executed in a specific order to do a specific thing. Just remember that functions do things!

hint~

We call our function with the `|| function: call flap [mySprite] ||` block.

```blocks
//@collapsed
function flap (bird: Sprite) {
  bird.vy = -50
  pause(200)
  bird.vy = 50
}

controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
  let bird: Sprite = null
  flap(bird)
})
```

## Introducing Conditionals @showhint

Conditionals are super important in coding. It allows us to add some variety to our code by allowing us to choose when or if we want to do something. Conditionals allow us to do things only if a specific condition is met. Think of it like this: You probably dont wear your rain jacket every day, but only if it is going to rain 💧. In code we would use an if-then statement to do this!

## Applying a Conditional to our Game @showhint

Ok, so how do we apply conditionals the game we are building? Currently, if we press the 'A' button enough times, our bird will fly off of the screen. This allows our playing to hack our game and get infinite points without ever worrying about losing a life. We can fix this by only running the flap function if it won't send the bird off of the screen.

Let's do this in the next step!

## Bird Movement Continued

We need to add an if-then statement and place the flap code call inside there. This will make sure the bird only flaps if it won't go off the screen.

- :smile: **Add If-then**: add an `|| logic: if <true> then ||` block within the controller.A.onEvent event.
- :weight: **Check >= Condition**: We need to replace the condition which right now says true with the following logic. We need a `|| logic: O > 0 ||` block. We want to change this to **>=**.
- :marker: **Use the Bird's Y Position**: in the left circle we want to add a `|| sprites: mySprite x ||` block. Change your x to y and choose the bird as the sprite. In the right circle you want to put the number 10.
- :move: **Compare to the number 10**: Lastly we want to make sure that the flap function call is placed inside of the if-then statement. This will run the flap function only when the bird's y position is greater than or equal to 10.

~hint How does this keep the bird from moving off the screen?

- :info: The bird is continually falling and can only move upward when the A button is pressed. Placing the flap code within an if-then function makes sure that the bird can only go up when going up will keep it within the boundaries of the screen.
  hint~

```blocks
//@collapsed
function flap (bird: Sprite) {
  bird.vy = -50
  pause(200)
  bird.vy = 50
}
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
  let bird: Sprite = null
  if (bird.y >= 10) {
    flap(bird)
  }
})
```

## On Game Update Event @showhint

We will use several events today but the first one is the `||game: on game update every <Interval> ||` event. This event allows us to create a **EventListener** that will run whatever instructions we put inside at a specific interval.
In other words it waits for a specified time to elapse and then runs our instructions.

## Add some Obstacles

We will use our interval event listener to spawn tree obstacles every second.

- :play: **Create Trees**: add a `|| function: createTrees ||` block within the `|| game: on game update every <Interval> ||` block.

~hint Why does that say 1000❓

- :info: The interval is in something called milliseconds. Milliseconds are fractions of a second. 1000 milliseconds equals 1 second.
  hint~

```blocks
//@collapsed
function createTrees() {
  let topTree: Sprite = null
  let bottomTree: Sprite = null
  topTree = sprites.createProjectileFromSide(sprites.duck.log7, -50, 0)
  topTree.setPosition(160, randint(0, 25))
  bottomTree = sprites.createProjectileFromSide(sprites.duck.log3, -50, 0)
  bottomTree.setPosition(160, randint(115, 140))
}

game.onUpdateInterval(1000, function () {
  createTrees()
})
```

## Add Scoring

We want our player to get a point for every second they can last without losing all of their lives. We already have an interval timer for every second so lets just use that.

- :trophy: **Incrementing the Score**: add a `|| info: change score by ||` block and set it to whatever you want your score to increase by every second.

```blocks
//@collapsed
function createTrees() {
  let topTree: Sprite = null
  let bottomTree: Sprite = null
  topTree = sprites.createProjectileFromSide(sprites.duck.log7, -50, 0)
  topTree.setPosition(160, randint(0, 25))
  bottomTree = sprites.createProjectileFromSide(sprites.duck.log3, -50, 0)
  bottomTree.setPosition(160, randint(115, 140))
}

game.onUpdateInterval(1000, function () {
  createTrees()
  info.changeScoreBy(1)
})
```

## Awesome Job! @showdialog

The functionality of our game is almost complete. We have the bird which has 3 lives, responds to gravity, and can flap to move up when you press the **A** button. We also have trees spawning as obstacles and we get points every second that we stay alive.

## Losing Lives @showhint

The only thing left now is adding events that actually take away our lives so that the game does not go on forever. As you can see right now, you can go directly through the tree without taking any damage. We currently have two ways of losing a life.

1. Colliding with a tree
2. Falling off the screen at the bottom

Let's code this out next!

## Changing Our Life Count

- :hazard: **Collide With Tree Logic**: inside of your `|| sprites: on overlap ||` event block add a `|| sprites: destroy mySprite ||` block. Change **mySprite** to otherSprite and hit the **+** sign and select **disintegrate** as the effect. Next add the `|| info: change life by ||` block and change the number to **-1**.
- :down arrow: **Fall Off Screen Logic**: within the `|| loops: forever ||` block add an `|| logic: if <true> then ||` block. Inside you want to add the `|| logic: 0 < 0 ||` block and change it to **>**. Add the `|| sprites: mySprite x ||` block and change the **x** to **y** for the left circle and add the number 130 for the right circle. Inside this if then want to take away a life and reset the bird to it's starting position. We need to add a `|| info: change life by ||` block and set the number to **-1**. Then we need to add a `|| spirites: set mySprite position to ||` block. We should set **bird** as the sprite and give it the values of **25 & 50**.

```blocks
let bird: Sprite = null
sprites.onOverlap(SpriteKind.Player, SpriteKind.Projectile, function (sprite, otherSprite) {
  sprites.destroy(otherSprite, effects.disintegrate, 200)
  info.changeLifeBy(-1)
})

forever(function () {
  if (bird.y > 130) {
    info.changeLifeBy(-1)
    bird.setPosition(25, 50)
  }
})
```

## We are all done! @showdialog

You did it! Excellent job! 🎉. Now let's get a Sensei to help you show off your new game. We are super proud of you and hope you enjoyed making your first of many games.
