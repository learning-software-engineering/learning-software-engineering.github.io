# Introduction to Pygame

## Table of Contents

- [Brief Introduction](#Breif Introduction)
- [Installment](#Installment)
- [Basic Setup](#Basic Setup)
- [Event Control](#Event Control)
- [Sprites](#Sprites)
  - [Creating a Sprite](#Creating a Sprite)
  - [Add Control to the Sprite](#Add Control to the Sprite)
  - [Add Animations](#Add Animations)
- [Surface](#Surface)
- [Mixer (Sound Effects)](#Mixer (Sound Effects))
  - [Sound](#Sound)
  - [Music](#Music)
- [Conclusion](#Conclusion)
- [Reference](#Reference)



## Breif Introduction

Pygame is an open-source Python library for making video games and multimedia applications. It simplifies game development with easy-to-use tools for graphics, sounds, and user input. Based on the SDL library, Pygame supports a wide range of operations from 2D graphics to handling events. Since its launch in 2000 by Pete Shinners, it has become popular among beginners and experienced programmers alike due to its comprehensive documentation, tutorials, and an active community. Ideal for prototypes and small to medium projects, Pygame is valued for its ease of use, flexibility, and quick development cycle.



## Installment

Python is requried inorder to install Pygame, which can be downloaed from [python.org](https://www.python.org). The latest version is preferred, but Python version 3 or higher is compatible. 

The easiest method to install Pygame is using via the pip tool. Open a comfortable terminal and run the following command if you are a mac user:

`python3 -m pip install -U pygame --user`

For window installment, replace 'python3' with 'py'. Upon success, we should be able to run an example game:

`python3 -m pygame.examples.aliens`

Upon success we should see the following window:

![[game.png]]



## Basic Setup

The first step is to import Pygame and initialize its modules in `main.py`.

```python
import pygame
import sys

# Initialize Pygame
pygame.init()
```

We then want to step up the screen display.

```python
# Set the screen dimensions
screen_width = 800
screen_height = 600

# Create the screen
screen = pygame.display.set_mode((screen_width, screen_height))

# Set a title for the window
pygame.display.set_caption('A Small Game')
```

Create a game loop that would keep the game running. In addition, event handling, updates and drawing on the screen are also included in this running loop.

```python
# Game loop
running = True
while running:
	# Event handing
	for event in pygame.event.get():
    if event.type == pygame.QUIT:
      running = False
      
# Add game logic here

# Refresh the screen
screen.fill((0, 0, 0))  # Fill the screen with black
pygame.display.flip()

# Quit Pygame
pygame.quit()
sys.exit()
```

To running our game, we would simply run `main.py`



## Event Control

Event control is a fundamental aspect of game development in Pygame, allowing us to respond to user inputs like keyboard presses, mouse clicks, and other events.

In Pygame, events are checked in the main game loop. We will use `pygame.event.get()` in the `pygame.event` module to get a list of all events and then iterate over this list to respond to specific events [Event].

```python
while running:
    # Event handling
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        elif event.type == pygame.KEYDOWN:
            if event.key == pygame.K_ESCAPE:
                running = False
            # We can add more key event handlers here
        elif event.type == pygame.MOUSEBUTTONDOWN:
            # Respond to mouse clicks
            if event.button == 1:  # Left click
                print("Left mouse button clicked at position", event.pos)
            elif event.button == 3:  # Right click
                print("Right mouse button clicked at position", event.pos)
```



## Sprites

At a fundamental level, a sprite is essentially an image that can move or be controlled within our game. For better performance, consider using images with smaller sizes or scaling them down if necessary.

We can add sprites to our game by incorporating the following code in `main.py`

```python
# Create sprite instance and group
player = Player()
all_sprites = pygame.sprite.Group()
all_sprites.add(player)
```



### Creating a Sprite 

To create a player character, we will inherit from the `pygame.sprite.Sprite` class [Sprite]. Within this class, we have the ability to customize the appearance and dimensions of the sprite.

```python
class Player(pygame.sprite.Sprite):
    def __init__(self):
        super().__init__()
        self.image = pygame.image.load('player.png').convert_alpha()  # Load the image
        self.rect = self.image.get_rect()  # Get the rectangular area
        self.rect.x = 100  # Initial X position
        self.rect.y = 100  # Initial Y position
```



### Add Control to the Sprite

The most basic method to add controls to sprites in Pygame is to modify the sprite's position based on keyboard input. This is typically done inside the game loop where we check for events (like key presses) and then update the sprite's position accordingly.

Inside the game loop, we will need to check for `KEYDOWN` and `KEYUP` events to determine when a key is pressed and when it's released. Based on these events, you can update the sprite's velocity or position.

```python
keys_pressed = pygame.key.get_pressed()  # Get the state of all keyboard buttons
player.update(keys_pressed)  # Update player position based on key presses
```

Update the `Player` class that updates sprite positions to react to the keyboard inputs.

```python
def animate(self):
        now = pygame.time.get_ticks()
        if now - self.last_updated > self.animation_speed:
            self.last_updated = now
            self.current_frame = (self.current_frame + 1) % len(self.frames)
            self.image = self.frames[self.current_frame]

def update(self, keys_pressed):
        self.animate()  # Call animate method to handle frame update
        if keys_pressed[pygame.K_LEFT]:
            self.rect.x -= self.speed
        if keys_pressed[pygame.K_RIGHT]:
            self.rect.x += self.speed
        if keys_pressed[pygame.K_UP]:
            self.rect.y -= self.speed
        if keys_pressed[pygame.K_DOWN]:
            self.rect.y += self.speed
```



### Add Animations

As previously discussed, sprites are essentially moving images. To create animation, we need to update the sprite's current image in accordance with the elapsed time, thereby creating the visual effect of animation.

Load all the animation frames into a list. This allows usto easily cycle through the images.

```python
self.frames = [pygame.image.load(f"frame_{i}.png").convert_alpha() for i in range(1, 4)] 
self.current_frame = 0
self.image = self.frames[self.current_frame]  # Start with the first frame
```

The example integrates animation with movement, so the sprite animates continuously as it moves. We can modify the `animate` method to play animations based on specific actions (e.g., walking, jumping) by selecting different frame lists according to the sprite's state.



## Surface

In Pygame, a `Surface` is a fundamental object where we can draw shapes, images, or text [Surface]. Essentially, it represents an image or a part of the screen where we can perform graphical operations. 

We can create additional surfaces onto which we'll draw before integrating them into the main display surface. Here's how to create a simple surface of a solid color.

```python
# Create a new surface with dimensions 200x150
surf = pygame.Surface((200, 150))

# Fill the surface with a color (e.g., red)
surf.fill((255, 0, 0))
```

We can draw shapes on the surface

```python
# Draw a blue rectangle on 'surf'
pygame.draw.rect(surf, (0, 0, 255), (50, 50, 100, 50))
```

"Blitting" is a term used in computer graphics meaning to transfer data from one surface to another. In Pygame, we blit our created surface onto the main display surface to make it visible.

```python
# Coordinates where we want to blit the surface on the main screen
position = (300, 225)

# Blit 'surf' onto the main screen at the specified position
screen.blit(surf, position)
```

This is the output of the above example:

![[surface.png]]



## Mixer (Sound Effects) 

Integrating music and sound effects into Pygame projects can significantly enhance the user's gaming experience, making it more immersive and engaging. Pygame's `pygame.mixer` module provides a straightforward way to add audio to the games [Mixer]. It supports various audio formats and provides functionalities to control playback, such as volume adjustment, looping, and pausing. First of all we shall initialize a mixer:

```python
# Initialize the mixer module
pygame.mixer.init()
```



### Sound

To play a sound effect, like a jump sound or an explosion, we first need to load the sound file into a `Sound` object and then play it.

```python
jump_sound = pygame.mixer.Sound("jump.wav")  # Load a sound

# To play the sound
jump_sound.play()
```

We can adjust the volume of sound effects and music, where 0.0 is silent and 1.0 is the maximum volume.

```python
# Set the volume for a sound effect
jump_sound.set_volume(0.5)

# Set the volume for the music
pygame.mixer.music.set_volume(0.5)
```



### Music

The `pygame.mixer.music` module is a part of Pygame that provides a simple way to handle background music in games or applications [Music]. In order to use the `pygame.mixer.music` module, we also need to initialize a mixer.

```python
# Load background music
pygame.mixer.music.load('background_music.mp3')

# Play the music
pygame.mixer.music.play(loops=-1)  # loops=-1 makes the music play indefinitely
```

The `pygame.mixer.music` module provides several functions to control music playback, including pausing, unpausing, and stopping the music.

```python
# Pause the music
pygame.mixer.music.pause()

# Unpause the music
pygame.mixer.music.unpause()

# Stop the music
pygame.mixer.music.stop()
```



## Conclusion

This brief introduction only scratches the surface of what Pygame offers. It's a powerful library for game development in Python, packed with features for graphics, sound, and handling user input. Pygame supports animated sprites, collision detection, camera following, and more, making it possible to create complex games. It also works with other Python libraries, enhancing its capabilities for game AI and physics. Whether you're starting out or have experience in game development, Pygame provides the tools to build everything from simple puzzles to complex, engaging games.



## Reference

- [Getting Started](https://www.pygame.org/wiki/GettingStarted)
- [Event](https://www.pygame.org/docs/ref/event.html)
- [Sprite](https://www.pygame.org/docs/ref/sprite.html)
- [Surface](https://www.pygame.org/docs/ref/surface.html)
- [Mixer](https://www.pygame.org/docs/ref/mixer.html)
- [Music](https://www.pygame.org/docs/ref/music.html)

