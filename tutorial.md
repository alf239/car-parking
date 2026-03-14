# Park Like a Pro: Building a Car Parking Game in Scratch

**A game physics adventure for curious minds**

---

You know what's really hard? Parking a car. Grown-ups do it every day and sometimes they *still* get it wrong. But here's the secret: parking is just physics — and physics is just a set of rules about how things move.

In this tutorial, we're going to learn those rules one at a time. And we're going to use them to build a real game in Scratch — a top-down car parking game where you drive a racing car into a tight parking spot.

By the end, you'll have a game you can show your friends. And you'll understand *why* parking is tricky — which is more than most grown-ups can say.

**What you'll need:**
- A computer with a web browser
- A Scratch account (free at scratch.mit.edu)
- A grown-up to read this with (they might learn something too)

**What we're building:**

A top-down racing game where you steer a cigar-shaped race car around a course, avoid the walls, and park it perfectly in a parking spot. There's a timer, a crash counter, and a happy sound when you nail it.

Let's go.

---

## Session 1: Where Is My Car?

*Position and Direction*

### What We Already Know

You've done coordinates before in maths — like finding a square on a grid by going along and then up. "3 across, 2 up" — that kind of thing.

You also know about turns. A quarter turn is a right angle (90 degrees). A half turn is 180 degrees. A full turn is 360 degrees — you end up facing the same way you started.

That's actually most of what you need to know to place a car on a screen and point it in a direction.

### The New Idea: Position and Direction

Everything in a game has two basic facts about it:

1. **Position** — *where* it is
2. **Direction** — *which way* it's facing

Position is just two numbers: how far across (left-right) and how far up-down. In Scratch, these are called **x** and **y**.

- **x** goes from -240 (far left) to 240 (far right)
- **y** goes from -180 (bottom) to 180 (top)
- The middle of the stage is x: 0, y: 0

Direction is an angle — a number of degrees. In Scratch:
- **0** means pointing up
- **90** means pointing right
- **180** means pointing down
- **-90** (or 270) means pointing left

So if your car is at x: 100, y: 50 and its direction is 90, it's sitting in the right half of the screen, pointing to the right.

> **For grown-ups:** Scratch's direction system is like a compass — 0 is north (up). This matches what children learn about compass directions in Year 3 geography. The x/y system maps directly to the coordinate grids they've used in maths, though Scratch extends into negative numbers. If your child hasn't met negatives yet, just say "minus means the other way" — left instead of right, or down instead of up.

### Let's Build It

**Step 1: Create a new project**

Open Scratch and click "Create". You'll see the cat sprite on the stage. We don't need the cat.

**Step 2: Delete the cat**

Right-click on the cat sprite (in the sprite area below the stage) and choose "delete".

**Step 3: Draw your car**

Click the paintbrush icon ("Paint") to create a new sprite. We're going to draw a top-down racing car — a long, thin oval shape like an old-fashioned cigar-shaped race car.

1. Select the **oval tool**
2. Pick a bright colour — red is classic for a racing car
3. Draw a long, narrow oval. Make it about 60 pixels tall and 20 pixels wide (roughly 3 times taller than it is wide)
4. Now add the **nose**: use a small triangle or arrow shape at the top of the oval. This is important — the pointy end shows which way the car is facing
5. Add two small rectangles on the sides near the bottom — these are the rear wheels
6. Add two small rectangles near the top — these are the front wheels

Make sure the car is drawn **pointing up** (towards the top of the canvas), because Scratch's default direction is 0 (up).

> **For grown-ups:** The car's "costume centre" (the crosshair in the costume editor) should be in the middle of the car. This is the point it rotates around. If it's off-centre, the car will wobble when it turns. You can drag the costume to adjust this.

**Step 4: Add movement code**

Click on your car sprite, then go to the **Code** tab. We're going to make it move with the arrow keys.

Build this script:

```
when green flag clicked
go to x: (0) y: (0)
point in direction (0)
forever
  if <key [up arrow] pressed?> then
    move (3) steps
  end
  if <key [down arrow] pressed?> then
    move (-3) steps
  end
  if <key [left arrow] pressed?> then
    turn left (3) degrees
  end
  if <key [right arrow] pressed?> then
    turn right (3) degrees
  end
end
```

**Where to find these blocks:**
- `when green flag clicked` — **Events** (yellow)
- `go to x: y:` and `point in direction` — **Motion** (blue)
- `forever`, `if then` — **Control** (orange)
- `key pressed?` — **Sensing** (light blue)
- `move steps` and `turn degrees` — **Motion** (blue)

**Step 5: Try it!**

Click the green flag. Use the arrow keys to drive your car around the stage.

Notice:
- **Up** moves the car forward (whichever way it's pointing)
- **Down** moves it backward
- **Left** and **Right** spin it

You've just built the most basic driving game possible. The car knows where it is (position) and which way it's facing (direction), and you can change both.

### Try It!

- Drive to each corner of the stage
- Try to drive in a straight line from left to right. (Hint: you'll need to point the car to the right first — direction 90)
- Park on the exact centre (x: 0, y: 0). How close can you get? Check by looking at the x and y values shown below the stage

### Want More?

Draw a road on the **backdrop**. Click the stage, then the "Backdrops" tab, and use the rectangle tool to draw grey roads on a green background. Now your car has somewhere to drive!

---

## Session 2: Fast and Slow

*Speed, acceleration, and braking*

### What We Already Know

You know about measuring distances — centimetres, metres, kilometres. You know that some things are fast (a cheetah) and some things are slow (a snail). You probably know that cars have a speedometer that shows how fast they're going.

You also know from maths that bigger numbers mean more. If you walk 10 steps, you go further than if you walk 3 steps. Simple.

### The New Idea: Speed

In Session 1, our car moved 3 steps every time we pressed the up arrow. That's fine, but it's not how real cars work. Real cars:

- **Speed up gradually** when you press the accelerator (gas pedal)
- **Slow down gradually** when you take your foot off
- **Brake** when you press the brake pedal
- **Don't stop instantly** — they slide a little bit first

Speed is just a number that says "how far does the car move each moment?" If speed is 0, the car is still. If speed is 5, it moves 5 steps each tick. If speed is -2, it moves backward.

**Acceleration** is what changes the speed. Press the accelerator, and the speed number gets bigger. Brake, and it gets smaller.

**Friction** is what slows you down even when you're not braking. In real life, the road surface and air resistance slow the car. In our game, we'll shrink the speed a tiny bit each moment so the car naturally coasts to a stop.

> **For grown-ups:** We're keeping this intuitive — speed as "steps per frame," acceleration as "speed change per frame." We're not introducing units or the formal v = d/t equation. Friction here is simplified to a multiplier (speed × 0.95 each frame), which mimics drag reasonably well for a game. The actual physics of friction (static vs kinetic, normal force) would be inappropriate for this age — the key insight is just "things slow down on their own."

### Let's Build It

We need a **variable** to store the car's speed. The speed will change over time — getting bigger when we accelerate, smaller when we brake or coast.

**Step 1: Create a speed variable**

Go to **Variables** (orange) and click "Make a Variable". Call it `speed`. Make sure "For this sprite only" is selected.

**Step 2: Update the movement code**

Replace your old script with this new one:

```
when green flag clicked
go to x: (0) y: (0)
point in direction (0)
set [speed] to (0)
forever
  if <key [up arrow] pressed?> then
    change [speed] by (0.3)
  end
  if <key [down arrow] pressed?> then
    change [speed] by (-0.5)
  end
  if <key [left arrow] pressed?> then
    turn left (3) degrees
  end
  if <key [right arrow] pressed?> then
    turn right (3) degrees
  end
  move (speed) steps
  set [speed] to ((speed) * (0.95))
end
```

**What changed:**
- We **set speed to 0** at the start (car begins stationary)
- **Up arrow** doesn't move the car directly — it increases `speed` by 0.3 (gentle acceleration)
- **Down arrow** decreases `speed` by 0.5 (braking is stronger than acceleration — just like a real car)
- `move (speed) steps` — the car moves by whatever the current speed is
- `set speed to (speed * 0.95)` — this is **friction**. Every frame, the speed is multiplied by 0.95, which means it shrinks by 5%. So the car gradually slows down on its own

> **For grown-ups:** The `* 0.95` line is the key physics trick. It means speed decays exponentially — fast speeds drop quickly, slow speeds linger. This gives a natural "coasting" feel. If the child asks "why 0.95?", try changing it to 0.8 (lots of friction, like driving on sand) or 0.99 (almost no friction, like ice). This is a great way to build intuition for how friction works.

**Step 3: Add a speed limit**

Cars can't go infinitely fast. Add this inside the `forever` loop, after the arrow key checks but before the `move` block:

```
if <(speed) > (5)> then
  set [speed] to (5)
end
if <(speed) < (-3)> then
  set [speed] to (-3)
end
```

This caps the car at 5 forward and 3 backward (reversing is always slower).

**Step 4: Try it!**

Click the green flag. Hold the up arrow — watch the car gradually pick up speed. Let go — it coasts. Press down — it brakes. Notice how it doesn't stop immediately.

### Try It!

- Accelerate to top speed, then let go. How far does the car coast?
- Try to stop the car on an exact spot. It's harder now!
- Hold the down arrow while moving forward — feel how braking works
- What happens if you hold down the down arrow when the car is stopped? (It reverses!)

### Want More?

Make the speed variable visible on the stage (tick the checkbox next to `speed` in the Variables palette). You now have a speedometer! Watch it go up and down as you drive.

For a fancier speedometer, you could create a second sprite that's a horizontal bar, and set its size to match the speed value.

---

## Session 3: Turning the Wheel

*Steering and turning radius*

### What We Already Know

You know about turning — quarter turns (right angles), half turns, full turns. You probably know that when you turn the steering wheel of a car, the front wheels point left or right, and that's what makes the car turn.

Here's something you might have noticed: if a car is standing still and you turn the steering wheel, the car doesn't go anywhere. It just sits there with the wheels pointed sideways. The car only *actually turns* when it's moving.

### The New Idea: Steering and Turning Radius

This is one of the most important physics ideas in our game:

**How fast you're going changes how sharply you can turn.**

Think about riding a bicycle:
- When you're going slowly, you can turn really tightly — almost spinning on the spot
- When you're going fast, you have to make a big, wide turn
- When you're standing still, you can turn the handlebars, but the bike doesn't change direction at all

This is called the **turning radius**. Slow = tight turns. Fast = wide turns.

This is exactly why parking needs slow speed. You need to make tight turns to fit into a space, and you can only make tight turns when you're going slowly.

> **For grown-ups:** The real physics here involves the relationship between velocity, steering angle, and the resulting circular arc. For an actual car, the turning radius depends on the wheelbase length and steering angle: R = L / tan(steering_angle). We're simplifying this to "turning amount is proportional to speed" which captures the essential insight. The key idea — that turning effectiveness depends on forward motion — is genuinely important and often surprises children (and adults).

### Let's Build It

We're going to change the steering so it depends on speed. We'll also add a visual indicator showing which way the front wheels are pointing.

**Step 1: Create a steering variable**

Go to **Variables** and make a new variable called `steering`. This represents the position of the steering wheel — negative means turned left, positive means turned right, zero means straight.

**Step 2: Update the steering code**

Replace the left/right arrow parts of your script:

```
when green flag clicked
go to x: (0) y: (0)
point in direction (0)
set [speed] to (0)
set [steering] to (0)
forever
  if <key [up arrow] pressed?> then
    change [speed] by (0.3)
  end
  if <key [down arrow] pressed?> then
    change [speed] by (-0.5)
  end
  if <key [left arrow] pressed?> then
    set [steering] to (-5)
  else
    if <key [right arrow] pressed?> then
      set [steering] to (5)
    else
      set [steering] to (0)
    end
  end
  turn right ((steering) * ((speed) / (3))) degrees
  move (speed) steps
  set [speed] to ((speed) * (0.95))
  if <(speed) > (5)> then
    set [speed] to (5)
  end
  if <(speed) < (-3)> then
    set [speed] to (-3)
  end
end
```

**The key new line is:**

```
turn right ((steering) * ((speed) / (3))) degrees
```

This says: "Turn by the steering amount, but multiply it by how fast we're going (divided by 3 to keep the numbers sensible)."

So:
- Standing still (speed = 0): steering × 0 = **no turning**
- Creeping (speed = 1): steering × 0.33 = **tiny turn**
- Medium speed (speed = 3): steering × 1 = **normal turn**
- Top speed (speed = 5): steering × 1.67 = **bigger turn per frame, but the car covers more ground, so the arc is wider**

This feels much more realistic than the old way.

> **For grown-ups:** We divide speed by 3 (a medium speed value) so that at medium speed, the car turns by the base steering amount. This is a scaling trick to keep the numbers feeling right. The child doesn't need to understand the division — just the result: "the car turns more when it's going faster, and not at all when it's stopped."

**Step 3: Add a wheel indicator**

Let's show which way the front wheels are pointing. The simplest way:

1. Create three costumes for your car sprite:
   - **straight** — the car with front wheels pointing straight (your current drawing)
   - **left** — a copy where the front wheel rectangles are rotated slightly to the left
   - **right** — a copy where the front wheel rectangles are rotated slightly to the right

2. Add this code inside the `forever` loop:

```
if <(steering) < (0)> then
  switch costume to [left]
else
  if <(steering) > (0)> then
    switch costume to [right]
  else
    switch costume to [straight]
  end
end
```

Now you can see the wheels turn when you steer!

**Step 4: Try it!**

Click the green flag. Drive around. Notice:
- You can't turn while stopped
- Slow speed = tight turns
- Fast speed = wider turns
- The wheels show which way you're steering

### Try It!

- Drive in a circle at slow speed. Now try the same circle at top speed. What happens?
- Try to drive in a perfect square: forward, right angle turn, forward, right angle turn... (Hint: you'll need to slow down for the corners!)
- Drive forward, then let go of up arrow and steer while coasting. The turning gets tighter as you slow down!

### Want More?

Try changing the steering value from 5 to 8 or 3. What feels better? Racing drivers call this "steering sensitivity" — some like tight steering, some like gentle steering. Find what feels best for your game.

---

## Session 4: Walls and Bumps

*Collision detection*

### What We Already Know

In science, you've learned about **forces** — pushes and pulls. When you push a toy car into a wall, the wall pushes back. The car stops. It can't go through the wall because two solid things can't be in the same place at the same time.

This is true in games too. We need our car to know when it's hit something.

### The New Idea: Collision

A **collision** is when two objects touch or overlap. In a game, we need to check for this every single moment (every "frame"). If the car touches a wall:

1. **Stop moving** (set speed to 0)
2. **Push back** a tiny bit so the car isn't stuck inside the wall
3. **Tell the player** (a bump sound, a visual flash, etc.)

In real life, collisions happen because of forces. In a game, we fake it: we just check "is the car touching something it shouldn't be?" and if so, we undo the movement.

> **For grown-ups:** Real game physics engines use sophisticated collision detection and response (separating axis theorem, impulse resolution, etc.). In Scratch, we use colour-based collision which is much simpler but works well for our purposes. The "push back" step is important — without it, the car can get stuck in the wall because it moved partially inside it before the collision was detected. Our approach is to remember the last safe position and snap back to it.

### Let's Build It

**Step 1: Design the course**

Click on the **Stage**, then the **Backdrops** tab. Draw a course:

1. Fill the whole backdrop with a colour for the road — **light grey** works well
2. Use the **rectangle tool** with a **dark brown or black** colour to draw walls around the edge of the stage
3. Add some inner walls to make a simple course — like an L-shaped corridor or a car park layout
4. Leave an open starting area and a clear path to where the parking spot will go later

**Important:** Use one specific colour for all walls (like dark brown, hex #663300, or black). We'll detect this colour to know when the car has hit a wall.

**Step 2: Add position memory variables**

We need to remember where the car was *before* it moved, so we can push it back on collision. Create two new variables:

- `last x` (for this sprite only)
- `last y` (for this sprite only)

**Step 3: Update the code for collision**

Here's the updated script. The new parts are marked with comments:

```
when green flag clicked
go to x: (-180) y: (-120)
point in direction (0)
set [speed] to (0)
set [steering] to (0)
forever
  -- Remember where we are before moving --
  set [last x] to (x position)
  set [last y] to (y position)

  -- Steering --
  if <key [left arrow] pressed?> then
    set [steering] to (-5)
  else
    if <key [right arrow] pressed?> then
      set [steering] to (5)
    else
      set [steering] to (0)
    end
  end

  -- Acceleration and braking --
  if <key [up arrow] pressed?> then
    change [speed] by (0.3)
  end
  if <key [down arrow] pressed?> then
    change [speed] by (-0.5)
  end

  -- Speed limits --
  if <(speed) > (5)> then
    set [speed] to (5)
  end
  if <(speed) < (-3)> then
    set [speed] to (-3)
  end

  -- Apply steering and movement --
  turn right ((steering) * ((speed) / (3))) degrees
  move (speed) steps

  -- Friction --
  set [speed] to ((speed) * (0.95))

  -- Collision check --
  if <touching color (#663300)?> then
    go to x: (last x) y: (last y)
    set [speed] to (0)
    start sound [Boing]
  end

  -- Costume for wheel indicator --
  if <(steering) < (0)> then
    switch costume to [left]
  else
    if <(steering) > (0)> then
      switch costume to [right]
    else
      switch costume to [straight]
    end
  end
end
```

**The new collision section does three things:**

1. `touching color (#663300)?` — checks if the car sprite is overlapping the wall colour
2. `go to x: (last x) y: (last y)` — snaps the car back to where it was before it moved
3. `set speed to 0` + `start sound Boing` — stops the car and plays a bump sound

> **For grown-ups:** To pick the right colour in the `touching color` block, click on the colour swatch in the block, then click the eyedropper tool, and click on the wall colour on your backdrop. This ensures it's the exact right shade. The "Boing" sound is built into Scratch — go to the Sounds tab, click the speaker icon to browse, and add it (or choose another sound you like).

**Step 4: Start position**

Notice we changed `go to x: (0) y: (0)` to `go to x: (-180) y: (-120)`. Put the starting position somewhere sensible on your course — a clear area away from walls. You might need to adjust these numbers for your course layout.

**Step 5: Try it!**

Click the green flag. Drive your car around the course. When you hit a wall — bonk! You stop dead and hear a sound. The car bounces back to its last position.

### Try It!

- Drive the full course without hitting a single wall
- Try hitting a wall at top speed vs. low speed. The snap-back feels different!
- Find the tightest corner on your course. Can you get around it? (Remember: slow down for tight turns!)

### Want More?

Add a crash counter! Create a variable called `crashes` (for all sprites). Set it to 0 when the green flag is clicked. Inside the collision `if` block, add `change [crashes] by (1)`. Now you can see how many times you've crashed. Can you do the whole course with zero crashes?

---

## Session 5: Park It!

*The parking challenge*

### What We Already Know

You've fitted shapes into spaces before — jigsaw puzzles, shape sorters, even tidying up a shelf so everything fits. You know that to fit something into a space, it needs to be the right size, in the right place, and pointing the right way.

### The New Idea: Parking as a Physics Puzzle

Parking is hard because you have to get **three things right at the same time:**

1. **Position** — the car has to be in the right place (x and y)
2. **Direction** — the car has to be facing the right way (angle)
3. **Speed** — the car has to be nearly stopped (you can't park at 50 miles per hour!)

Each of these on its own is easy. Driving to a spot? Easy. Turning to face the right way? Easy. Stopping? Easy. But doing all three *together* is the challenge. This is what makes parking a proper physics puzzle.

And here's the thing: because you can only turn well when you're moving slowly (remember Session 3?), you have to do the hard part — fine-tuning your position and angle — at exactly the speed where your controls are most sensitive. That's why even grown-ups find it tricky!

> **For grown-ups:** This is a great moment to connect to the mathematical idea of degrees of freedom. The car has three variables to control simultaneously (x, y, angle), which is what makes parking a challenging control problem. Professional game designers call this kind of challenge "multi-axis alignment" — the player must satisfy several constraints at once. You might also mention to your child that real self-driving cars find parking to be one of the hardest tasks too!

### Let's Build It

**Step 1: Create the parking spot**

Create a new sprite (click the paintbrush icon):

1. Draw a rectangle outline — just the border, no fill. Make it big enough that the car fits inside with a little room to spare, but not much. The car should just fit.
2. Use a bright colour like **green** or **yellow** for the outline so it's easy to see
3. Name this sprite "ParkingSpot"

Position it on the stage where you want the parking challenge to be. A good spot is at the end of your course, perhaps in a corner or between two walls. Set its x and y position in the code:

```
when green flag clicked
go to x: (150) y: (100)
point in direction (0)
```

(Adjust the position to fit your course layout.)

**Step 2: Add the parking detection**

The parking spot sprite needs to constantly check whether the car has parked successfully. Add this script to the **ParkingSpot** sprite:

```
when green flag clicked
go to x: (150) y: (100)
point in direction (0)
set [parked] to (0)
forever
  if <<touching [Car]?> and <([speed] of [Car]) < (0.5)>> then
    if <<([speed] of [Car]) > (-0.5)> and <(abs of (([direction] of [Car]) - (0))) < (20)>> then
      set [parked] to (1)
      start sound [Collect]
      say [Parked!] for (2) seconds
      stop [all]
    end
  end
end
```

Wait — that's a lot of conditions! Let's break it down:

1. `touching [Car]?` — the car is overlapping the parking spot
2. `speed of Car < 0.5` AND `speed of Car > -0.5` — the car is nearly stopped (speed close to zero)
3. `abs of (direction of Car - 0) < 20` — the car is pointing roughly the right way (within 20 degrees of the target direction, which is 0 = up)

All three must be true at the same time. Position + Speed + Direction.

> **For grown-ups:** The `abs` block is in the Operators category (green). If your child asks what "abs" means, say "it just throws away the minus sign — it tells us how far from zero, whether plus or minus." The value 20 (degrees of tolerance) is adjustable — start generous and tighten it later for more challenge. The target direction (0 in our code) should match the direction you want the car to face when parked — if your spot faces right, use 90.

**Step 3: Build the `abs` block in Scratch**

Scratch doesn't have a built-in `abs` block, but it has a maths function that does the same thing. In the Operators (green) category, you'll find a block that looks like:

```
( [abs] of ( ) )
```

Use it like this: `(abs of (([direction] of [Car]) - (0)))`

This calculates how far off the car's direction is from the target, ignoring whether it's off to the left or right.

**Step 4: Add a "Collect" or happy sound**

Go to the **Sounds** tab on the ParkingSpot sprite. Click the speaker icon to browse Scratch's sound library. Find something celebratory — "Collect", "Win", or "Tada" all work well. Add it to the sprite.

**Step 5: Create the `parked` variable**

Make a variable called `parked` (for all sprites). We'll use this in Session 6 for scoring, but for now it just records that you've done it.

**Step 6: Try it!**

Click the green flag. Drive to the parking spot. Line up carefully. Slow down. Match the angle. When all three conditions are met — PARKED! Happy sound, celebration message, game stops.

This is the moment. This is what we've been building towards. It's hard, and it's *supposed* to be hard. That's what makes it satisfying when you nail it.

### Try It!

- Park the car. How many attempts does it take?
- Try approaching the spot from different angles. Which approach is easiest?
- Can you park with zero crashes? (Check your crashes counter from Session 4)
- What happens if you try to drive into the spot fast? The speed check stops you from "cheating"!

### Want More?

Add a second parking spot somewhere trickier — maybe you have to reverse into it, or it's between two walls. Duplicate the ParkingSpot sprite and reposition it. You can make the game require parking in both spots by checking both `parked` variables.

---

## Session 6: Make It a Real Game

*Polish, scoring, and the full experience*

### What We Already Know

You know about counting and timing. You know what a "personal best" is — your best score that you try to beat. You know that the best games have a beginning, a middle, and an end.

Right now, our game works, but it just... starts. There's no "ready, set, go." There's no score at the end. There's no way to try again. Let's fix that.

### The New Idea: Game Loop

Every game has a **loop**:

1. **Start** — show the title, wait for the player
2. **Play** — the main game
3. **End** — show the result (score, time, etc.)
4. **Again?** — let the player try again

This isn't really physics — it's game design. But it's what turns a physics simulation into a *game*.

> **For grown-ups:** The game loop is a fundamental concept in computer science and game development. It's worth noting to your child that every game they've ever played has this loop — from simple mobile games to complex console games. The loop is what makes a game repeatable and engaging. The timer and crash counter together create a simple scoring system that encourages both speed and care — a natural tension that makes the game interesting.

### Let's Build It

**Step 1: Add a timer**

Scratch has a built-in timer. We just need to use it.

Add to the **car sprite's** green flag script, right after the starting setup:

```
reset timer
```

The timer will now count from 0 when the game starts.

To show the time when you park, update the ParkingSpot sprite's parking detection. Change:

```
say [Parked!] for (2) seconds
```

to:

```
say (join [Parked in ] (join (round (timer)) [ seconds!])) for (3) seconds
```

This will say something like "Parked in 14 seconds!"

**Step 2: Make sure crashes show**

If you did the stretch activity in Session 4, you already have a `crashes` variable. If not, create one now (for all sprites) and add this to your car's green flag script:

```
set [crashes] to (0)
```

And add this inside the collision `if` block in the car's code:

```
change [crashes] by (1)
```

**Step 3: Add a start screen**

Create a new sprite called "StartScreen". Draw a nice title:

1. Use the text tool to write "PARK LIKE A PRO" in big, bold letters
2. Underneath, add "Press SPACE to start"
3. Make the background of the costume transparent

Add this code to the StartScreen sprite:

```
when green flag clicked
show
go to x: (0) y: (0)
go to [front] layer
wait until <key [space] pressed?>
hide
broadcast [start game]
```

Now update your **car sprite** and **ParkingSpot sprite**: change `when green flag clicked` to `when I receive [start game]` for the main game code. Keep a small `when green flag clicked` script on each that just hides them or sets them up in their starting state.

**Car sprite — two scripts:**

```
when green flag clicked
hide
go to x: (-180) y: (-120)
point in direction (0)
```

```
when I receive [start game]
show
set [speed] to (0)
set [steering] to (0)
set [crashes] to (0)
reset timer
forever
  ... (all the driving code from before)
end
```

**ParkingSpot sprite — two scripts:**

```
when green flag clicked
show
go to x: (150) y: (100)
point in direction (0)
```

```
when I receive [start game]
set [parked] to (0)
forever
  ... (parking detection code from before)
end
```

**Step 4: Add a result screen**

When the player parks successfully, instead of just saying "Parked!" and stopping, let's show a proper result.

In the ParkingSpot's parking detection, replace the `stop [all]` with:

```
broadcast [game over]
stop [other scripts in sprite]
```

Create a new sprite called "ResultScreen". Draw a background and add:

```
when green flag clicked
hide

when I receive [game over]
show
go to [front] layer
say (join (join [Time: ] (join (round (timer)) [s])) (join [ | Crashes: ] (crashes)))
wait (3) seconds
say [Press SPACE to play again!]
wait until <key [space] pressed?>
hide
broadcast [start game]
```

Now the game loops: start → play → result → play again!

**Step 5: Try it!**

Click the green flag. You see the title screen. Press space. Drive, park, celebrate! See your time and crash count. Press space to play again. It's a real game!

### Try It!

- Play 3 rounds. What's your best time?
- Try to get 0 crashes AND a fast time. It's a trade-off — going fast means more crashes!
- Show someone else and watch them play. Is the game fun for them?
- What would you change to make it harder? Easier?

### Want More?

- Add more parking spots — the player must park in all of them to win
- Add a "level" system: Level 1 has one spot, Level 2 has two spots in harder positions
- Add a "best time" variable that remembers the best score across rounds
- Change the backdrop for each level to create different course layouts

---

## Quick Reference: Scratch Blocks We Used

| Block | Category | What it does |
|-------|----------|-------------|
| `when green flag clicked` | Events | Starts the script |
| `when I receive [message]` | Events | Starts on broadcast |
| `broadcast [message]` | Events | Sends a message to all sprites |
| `go to x: y:` | Motion | Sets position |
| `point in direction` | Motion | Sets which way sprite faces |
| `move (n) steps` | Motion | Moves forward (or backward if negative) |
| `turn right/left (n) degrees` | Motion | Rotates the sprite |
| `x position` / `y position` | Motion | Current position |
| `direction` | Motion | Current angle |
| `forever` | Control | Loops forever |
| `if <> then` | Control | Checks a condition |
| `if <> then else` | Control | Checks with alternative |
| `wait until <>` | Control | Pauses until condition is true |
| `stop [all]` | Control | Stops everything |
| `key [x] pressed?` | Sensing | Is a key held down? |
| `touching [sprite]?` | Sensing | Sprite overlap check |
| `touching color [#]?` | Sensing | Touching a colour? |
| `timer` / `reset timer` | Sensing | Built-in stopwatch |
| Variables | Variables | Store numbers that change |
| `set / change variable` | Variables | Update variable values |
| `join` | Operators | Combine text |
| `round` | Operators | Round a number |
| `abs of` | Operators | Distance from zero |
| `show` / `hide` | Looks | Make sprite visible/invisible |
| `switch costume` | Looks | Change appearance |
| `say [x] for (n) seconds` | Looks | Speech bubble |
| `go to [front] layer` | Looks | Put sprite on top |
| `start sound` | Sound | Play a sound effect |

---

## What's Next?

You've built a real game! Here are some ideas if you want to keep going:

**Session 7: Reverse!**
Put the car in reverse gear. When speed is negative, steering works *backwards* — turning left makes the back of the car go right. This is why reversing into a parking space is so tricky. Try adding parallel parking!

**Session 8: Traffic!**
Add other cars on the course. Start with parked cars that are just obstacles. Then try making one drive back and forth on a path. Now you have to time your moves!

**Session 9: Different Cars**
What if your car was longer? Shorter? In real life, longer cars are harder to park. Try making a stretched "limo" version and see how much harder it gets. Shorter cars (like a Smart car) are much easier. This is physics in action — the wheelbase length changes the turning radius.

---

*Made with curiosity and Scratch. Happy parking!*
