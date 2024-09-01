## <p align="center"> EX.NO : 5 -- IMPLEMENTATION OF JUMP BEHAVIOUR... </p>

#### DATE : 23.08.2024                                                                           
#### REGISTER NUMBER : 212221240005

### AIM :

To write a python program to simulate Jumbing behavior. 

### ALGORITHM :

#### Step 1 : 

Start the program.

#### Step 2 :

Import the necessary modules.

#### Step 3 :

Initiate the pygame engine and window.

#### Step 4 :

Specify the necessary parameter for player height, depth, gravity, jump power.

#### Step 5 :

Create a game loop to simulate the continuous behavior.

#### Step 6 :

If Quit button is pressed then quit the pygame window.

#### Step 7 :

Move the player left when left button is pressed.

#### Step 8 :

Move the player right when right button is pressed.

#### Step 9 :

If space bar is pressed then enable the jump by increasing y axis value.

#### Step 10 :

Land the player and display the player at every timestep.

#### Step 11 :

Stop the program.
    
### PROGRAM :

```python
import pygame
from pygame.locals import *
from sys import exit

sprite_image_filename = r'C:\Users\SEC\OneDrive\Pictures\Screenshots\Screenshot 2024-04-11 225559.png'
pygame.init()
screen = pygame.display.set_mode((640, 480), 0, 32)
sprite = pygame.image.load(sprite_image_filename)
screen.fill((0, 0, 0))
clock = pygame.time.Clock()
```

```python
# Speed in pixels per second
speed = 250
# The x coordinate of our sprite
x = 0.0

# Variables for jumping
y = 100
y_velocity = 0
gravity = 1000  # pixels per second squared
jump_speed = -500  # initial jump velocity
```

```python
# Flag to check if the sprite is on the ground
is_jumping = False

while True:
    for event in pygame.event.get():
        if event.type == QUIT:
            pygame.quit()
            exit()
        elif event.type == KEYDOWN:
            if event.key == K_SPACE and not is_jumping:
                y_velocity = jump_speed
                is_jumping = True
    
    # Clear the screen
    screen.fill((0, 0, 0))
    
    # Calculate the time passed
    time_passed = clock.tick(30)
    time_passed_seconds = time_passed / 1000.0
    
    # Calculate the distance moved horizontally
    distance_moved = time_passed_seconds * speed
    x += distance_moved
    
    # Calculate vertical movement
    y_velocity += gravity * time_passed_seconds
    y += y_velocity * time_passed_seconds
    
    # Check if sprite has landed on the ground
    if y >= 100:
        y = 100
        y_velocity = 0
        is_jumping = False
    
    # Draw the sprite at the new position
    screen.blit(sprite, (x, y))
    
    # If the image goes off the end of the screen, move it back
    if x > 640:
        x -= 640
    
    # Update the display
    pygame.display.update()
```

### OUTPUT :

![aifg-5](https://github.com/user-attachments/assets/8881ee51-40e5-4df8-9524-1236b0cbb63e)

### RESULT :

Thus, the simple jumping behavior  was implemented.

