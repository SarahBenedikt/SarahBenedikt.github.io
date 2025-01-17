---
layout: post
title:  "How to build the Breakout Game using Pygame"
date:   2024-10-10 20:10:57 -0600
categories: coding games python
---
I rebuild a real classics of Videogames - Breakout. You can find the final version on my [GitHub](https://github.com/SarahBenedikt/Breakout) page. Here's how I built it step by step.

## Final Screen Shot
![breakout image]({{ "/assets/screenshot_breakout_1.png" | relative_url }})
*Screenshot of my breakout game*

## What did I use?
- PyCharm as IDE
- Pygame library
- Bricks and Paddle from [opengameart.org](https://opengameart.org/content/breakout-set)

## How I created the Game

### Importing Modules and Initializing Pygame
First I imported all relevant modules. The `sys` module will be needed later to close the game correctly. I used the `random` module to select different coloured bricks.

{% highlight python %}
import pygame
from sys import exit
import random
{% endhighlight %}

Then I started pygame an initiated all subparts with:

{% highlight python %}
pygame.init()
{% endhighlight %}

### Setting Up the Game Window

The game window provides the visual area where all gameplay occurs. `set_mode` defines the screen size, and the `Clock` object regulates the frame rate.

{% highlight python %}
screen = pygame.display.set_mode((800, 600))
pygame.display.set_caption('Breakout')
clock = pygame.time.Clock()
{% endhighlight %}

A stable framerate is needed to ensure the game doesn't run too fast or too slow. The game should run on a stable speed of 60 frames per second. Thats done in the game loop later:

{% highlight python %}
clock.tick(60)
{% endhighlight %}


### Loading Graphics and Fonts

Pygame uses surfaces to display objects on the screen. Surfaces can be plain colored, image-based, or text-based. The `.convert()` method is used for performace optimization.

**Plain Color Surface**

{% highlight python %}
background_surf = pygame.Surface((800, 600)).convert() # creates a surface
background_surf.fill('Red') # fill surface with red color
{% endhighlight %}

All surfaces are placed on the screen with the `.blit()` method. You do that in the game loop. The last two numbers are coordinates on the screen.
{% highlight python %}
screen.blit(background_surf, (0, 0))
{% endhighlight %}

**Image Surface**

Image surfaces load from files. It's a good practice to store them in a folder named *graphics* within the project directory. The `.convert_alpha()` method loads images with transparency support.

{% highlight python %}
paddle_surf = pygame.image.load('graphics/paddle.png').convert_alpha() # load image from file
paddle_surf = pygame.transform.rotozoom(paddle_surf, 0, 1.5) # 0 degree rotation + zooms factor 1.5
{% endhighlight %}

**Text Surface**

Text surfaces require a font style. Fonts can be loaded from a `.ttf` file. The `.render()` method generates a text surface with specified content and color.

{% highlight python %}
font = pygame.font.Font('font/Pixeltype.ttf', 40)
text_surf = font.render('000', False, (99, 155, 255)) # 000 = text, False = no round edges (AA wound be round edges), RGB color code
{% endhighlight %}

### Rectangles

Rectangles are used to detect a precise collision of surfaces. To create a rectangle out of a Surface, you use the `.get_rect` function.

{% highlight python %}
paddle_rect = paddle_surf.get_rect(midbottom=(400, 580))
{% endhighlight %}

![Rectangle Attributes image]({{ "/assets/rectangle_attributes.png" | relative_url }})

*Attributes of rectangle object in Pygame*

### The Game loop

The game loop continuously runs the game, checking for events, updating the game state, and rendering the visuals.

{% highlight python %}
while True:
# Ball Logic (Velocity, Moves)
# Paddle Grid and move
# Score
# Lives
# Game Over
# Brick Grid
# Collosion Logic
pygame.display.update() # ensures that the screen is updated regulary
{% endhighlight %}

To ensure you are able to close the game window, you need this part in the while loop:

{% highlight python %}
for event in pygame.event.get():
    if event.type == pygame.QUIT:
        pygame.quit()
        exit() #Thats part of the sys module and important to close the game correctly
{% endhighlight %}

### Keyboard Input

Keyoard inputs are defined in the game loop. I defined a funtion to handle the paddle move in this game. The `paddle_speed` is a variable which equals 10. `clamp_ip` keeps the paddle within the screen boundaries.

{% highlight python %}
def move_paddle():
    """Moves the paddle left and right when keys are pressed."""
    keys = pygame.key.get_pressed() # retuns object with all keys pressed
    if keys[pygame.K_LEFT]:
        paddle_rect.x -= paddle_speed # moves paddle to left if left arrow is pressed on keyboard
    if keys[pygame.K_RIGHT]:
        paddle_rect.x += paddle_speed # moves paddle to right if right arrow is pressed on keyboard
    paddle_rect.clamp_ip(screen.get_rect())
{% endhighlight %}

Another option to handle keyboard input, is to check if any key is pressed and match it agains the input. I used this to shoot the ball once the space key is pressed as start of my game loop:

{% highlight python %}
if event.type == pygame.KEYDOWN:
    if event.key == pygame.K_SPACE and not ball_moving:
        ball_velocity = [ball_speed, -ball_speed]
        ball_moving = True
{% endhighlight %}

In the `move_ball` function, I used `paddle_rect.clamp_ip(screen.get_rect())`to ensure the paddle stays within the game window. Another option to achieve this would be an if statement:

{% highlight python %}
if paddle_rect_left <0:
    paddle_rect_left = 0
if paddle_rect_right <800:
    paddle_rect_right = 800
{% endhighlight %}

### Mouse Input

Similar to keyboard entries, you can identify which mouse button is pressed by use the `.get_pressed` function.

{% highlight python %}
clicks = pygame.mouse.get_pressed()
{% endhighlight %}

To get the coordinates of the player mouse use `.get_pos` function:

{% highlight python %}
player_mouse = pygame.mouse.get_pos()
{% endhighlight %}

A logic to print ***collosion*** when the player mouse hits a rectangle could be:

{% highlight python %}
player_mouse = pygame.mouse.get_pos()
    if player_rect.collidepoint(player_mouse)
        print('collision')
{% endhighlight %}

### Ball Movement

The ball moves based on its velocity. Collisions with the screen edges and the paddle invert the ball's direction.

Defined variables:

{% highlight python %}
ball_velocity = [0, 0]
ball_speed = 5 # speed of ball
ball_moving = False # ball is only moving if space key is pressed
{% endhighlight %}

First I created a `reset_ball` function as I will need this later for defining the full ball handling. In case the ball gets lost, it will be placed back on the paddle.

{% highlight python %}
def reset_ball():
    """Reset ball position and velocity."""
    ball_rect.center = paddle_rect.midtop
    ball_velocity[0] = 0
    ball_velocity[1] = 0
{% endhighlight %}


Now I created a `move_ball` funtion to handle the full ball move logic:

{% highlight python %}
def move_ball():
    """Moves ball and handles life loss."""
    global ball_moving, lives
    ball_rect.x += ball_velocity[0]
    ball_rect.y += ball_velocity[1]

    # Handles ball collision on left, right and top screen borders. The ball will always bounce to the reverse direction. 

    if ball_rect.left <= 0 or ball_rect.right >= 800:
        ball_velocity[0] = -ball_velocity[0]
    if ball_rect.top <= 0:
        ball_velocity[1] = -ball_velocity[1]

    # Handles ball collision with paddle. Also in this case, the ball will bounce towards the reverse direction.

    if ball_rect.colliderect(paddle_rect) and ball_velocity[1] > 0:
        ball_velocity[1] = -ball_velocity[1]

    # Handles a ball loss scenario.

    if ball_rect.bottom >= 600:
        ball_moving = False
        lives -= 1
        reset_ball()
{% endhighlight %}

### Random Brick Creation

First I loadad all the graphics for the bricks from the `graphics` directory.

{% highlight python %}
brick_colors = ['dark', 'green', 'orange', 'purple', 'yellow', 'red']
bricks = {}
for color in brick_colors:
    brick_surf = pygame.image.load(f'graphics/brick_{color}.png').convert_alpha()
    brick_surf = pygame.transform.rotozoom(brick_surf, 0, 1.5)
    bricks[color] = brick_surf
{% endhighlight %}

Next I created a list of brick rectangles to define the grid for the bricks.

{% highlight python %}
brick_width = bricks['red'].get_width()
brick_height = bricks['red'].get_height()
brick_rows = 8
brick_cols = 15
brick_padding = 5
brick_grid = []
{% endhighlight %}

The function `create_brick_grid` covers the creation of bricks on the game screen.

{% highlight python %}
def create_brick_grid():
    """Creates a new grid of bricks for the current level."""
    brick_grid.clear()  # Clear existing bricks
    for row in range(brick_rows):
        brick_row = []
        for col in range(brick_cols):
            brick_x = col * (brick_width + brick_padding)
            brick_y = row * (brick_height + brick_padding) + 70
            brick_type = random.choice(brick_colors)
            brick_rect = bricks[brick_type].get_rect(topleft=(brick_x, brick_y))
            brick_row.append((brick_type, brick_rect))
        brick_grid.append(brick_row)
{% endhighlight %}

### Handling Brick Collisions

Collision detection checks if the ball hits a brick. If a collision occurs, the brick is removed from the list, and the ball's direction is inverted. Aditionally it increases the `score` variable by 1.
{% highlight python %}
def check_ball_brick_collision():
    """Checks collision with bricks."""
    global ball_velocity, score, text_surf
    for brick_row in brick_grid:
        for brick in brick_row:
            brick_type, brick_rect = brick
            if ball_rect.colliderect(brick_rect):
                brick_row.remove(brick)  # Remove brick upon collision

                # Bounce ball on collision
                ball_velocity[1] = -ball_velocity[1]
                score += 1  # Increase score by 1
                # Update the score display, formatted as three digits
                text_surf = font.render(f'{score:03}', False, (99, 155, 255))
                return  # Exit after first collision to prevent multiple hits in one frame
{% endhighlight %}

### Managing Lives and Game Over

The game tracks the number of lives left and displays a game over message when all lives are lost. The lives are visualized with a `heart_surf` surface.

{% highlight python %}
def draw_lives():
    """Draws the remaining lives (hearts) on the screen."""
    for i in range(lives):
        heart_x = 600 + (i * (heart_surf.get_width() + 10))  # Spacing between hearts
        heart_y = 15
        screen.blit(heart_surf, (heart_x, heart_y))


def display_game_over_message():
    """Displays 'GAME OVER' message."""
    game_over_text = font.render('GAME OVER', True, (99, 155, 255))
    game_over_rect = game_over_text.get_rect(center=(400, 250))  # Centered on the screen
    screen.blit(game_over_text, game_over_rect)

    score_text = font.render(f'SCORE: {score}', True, (99, 155, 255))
    score_rect = score_text.get_rect(center=(400, 350))  # Centered below Game Over
    screen.blit(score_text, score_rect)

{% endhighlight %}