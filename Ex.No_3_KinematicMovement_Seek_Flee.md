## <p align="center"> EX.NO : 3 -- IMPLEMENTATION OF KINEMATIC MOVEMENT OF SEEK AND FLEE BEHAVIOURS... </p>

#### DATE : 16.08.2024      
#### NAME : Anto Richard. S
#### REGISTER NUMBER : 212221240005
#### SLOT : 4H2-1

### AIM : 

To write a python program to simulate the process of seek and flee behaviors using mouse movements.

### ALGORITHM :

#### Step 1 :

Import the necessary modules pygame, math, random when necessary.

#### Step 2 :

Initiate the pygame engine.

#### Step 3 :

Create a window with size (400,300).

#### Step 4 :

Create a function to simulate the seek behavior - to move towards the target.

#### Step 5 :

Create a function to simulate the flee behavior - to move away from the target.

#### Step 6 :

Update the position of object.

#### Step 7 :

Create a game loop to display the update behavior.

#### Step 8 :

Call the seek function when left mouse button is pressed.

#### Step 9 :

Call the flee function when right mouse button is pressed.

#### Step 10 :

Close the pygame window when quit icon is clicked.

#### Step 11 :

Stop the program.
    
### PROGRAM :

```python
import pygame
import random
import math

# Initialize Pygame
pygame.init()

# Constants
WIDTH, HEIGHT = 800, 600
WHITE = (255, 255, 255)
RED = (255, 0, 0)
GREEN = (0, 255, 0)
BLUE = (0, 0, 255)

# Create the screen
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Kinematic Wander, Align, Seek, Flee Example")
```

```python
# Define the Agent class
class Agent:
    def __init__(self, x, y):
        self.position = pygame.Vector2(x, y)
        self.velocity = pygame.Vector2(random.uniform(-2, 2), random.uniform(-2, 2))
        self.max_speed = 4
        self.wander_angle = 0

    def update(self):
        # Update position
        self.position += self.velocity

        # Wrap around screen edges
        if self.position.x > WIDTH: self.position.x = 0
        if self.position.x < 0: self.position.x = WIDTH
        if self.position.y > HEIGHT: self.position.y = 0
        if self.position.y < 0: self.position.y = HEIGHT

    def seek(self, target):
        desired_velocity = (target - self.position).normalize() * self.max_speed
        self.velocity = desired_velocity

    def flee(self, target):
        desired_velocity = (self.position - target).normalize() * self.max_speed
        self.velocity = desired_velocity

    def wander(self):
        wander_radius = 50
        wander_distance = 60
        change = 0.3
        
        self.wander_angle += random.uniform(-change, change)
        
        circle_center = self.velocity.normalize() * wander_distance
        displacement = pygame.Vector2(wander_radius * math.cos(self.wander_angle), wander_radius * math.sin(self.wander_angle))
        wander_velocity = circle_center + displacement
        self.velocity = wander_velocity.normalize() * self.max_speed

    def align(self, target_velocity):
        self.velocity = target_velocity.normalize() * self.max_speed

    def draw(self, screen):
        pygame.draw.circle(screen, GREEN, self.position, 8)
```

```python
# Main game loop
def main():
    clock = pygame.time.Clock()
    agent = Agent(WIDTH // 2, HEIGHT // 2)
    target = pygame.Vector2(random.randint(0, WIDTH), random.randint(0, HEIGHT))

    running = True
    while running:
        screen.fill(WHITE)
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                running = False

        # Kinematic Wander behavior
        agent.wander()

        # Kinematic Seek behavior
        agent.seek(target)

        # Kinematic Flee behavior
        mouse_pos = pygame.mouse.get_pos()
        agent.flee(pygame.Vector2(mouse_pos))

        # Optional: Kinematic Align with a fixed velocity
        # target_velocity = pygame.Vector2(2, 1)
        # agent.align(target_velocity)

        agent.update()
        agent.draw(screen)

        # Draw the target
        pygame.draw.circle(screen, RED, target, 10)

        pygame.display.flip()
        clock.tick(60)

    pygame.quit()

if __name__ == "__main__":
    main()
```

### OUTPUT :
 
![aifg-3](https://github.com/user-attachments/assets/ada40b75-111c-474f-8438-4a00822f5fd1)


### RESULT :

Thus, the simple seek and flee behavior was implemented successfully.

