## <p align="center"> EX.NO : 11 -- Mini Project... </p>

#### DATE : 25.10.2024      
#### NAME : Anto Richard. S
#### REGISTER NUMBER : 212221240005
#### SLOT : 4H2-1

### Aim : 

To write a Python program to simulate a 2D game titled "Bubble Popper: A 2D Frenzy" where a player-controlled character pops bubbles while competing against an AI-controlled character.

### Algorithm :

#### 1.Initialization :
*   Import the required libraries (pygame, random, math).
  
*   Set up the game screen and initialize Pygame.
  
*   Define global constants such as screen dimensions, colors, and speeds.
  
*   Create classes for the player, bubbles, and the AI.

#### 2. Player and AI Movement :

*   Implement the Player class with methods for movement via arrow keys.
  
*   Implement the AIPlayer class with logic to move towards the nearest bubble.

#### 3. Bubble Generation and Collision Detection :

*   Periodically spawn bubbles at random positions on the screen.
  
*   Detect collisions between the player or AI and bubbles.
  
*   Update scores based on bubbles popped by each character.

#### 4. Scoring and Game Display :

*   Display scores for both the player and AI at the top of the screen.
  
*   Use a gradient background to enhance the visual appeal.

#### 5. Game Loop :

*   Continuously update player and AI positions.
  
*   Render all elements, including the gradient background, characters, and bubbles.
  
*   Detect and handle events like quitting the game.

### Program :

```python

import pygame
import random
import math

# Initialize pygame
pygame.init()

# Screen dimensions
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Bubble Popper")

# Colors
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
BLUE = (0, 0, 255)
AI_COLOR = (100, 100, 100)  # Distinct color for AI character
PLAYER_COLOR = (50, 150, 255)  # Player Color (light blue)
BUBBLE_COLOR = (135, 206, 250)  # Light sky blue

# Background pattern - Gradient from light blue to white
def draw_gradient_background():
    for y in range(HEIGHT):
        # Create a smooth transition of colors
        color_ratio = y / HEIGHT
        r = int(135 + (255 - 135) * color_ratio)  # Gradient for Red channel
        g = int(206 + (255 - 206) * color_ratio)  # Gradient for Green channel
        b = 250  # Fixed Blue channel for a sky-blue color
        pygame.draw.line(screen, (r, g, b), (0, y), (WIDTH, y))  # Draw a line from left to right

# Player class
class Player(pygame.sprite.Sprite):
    def __init__(self):
        super().__init__()
        self.image = pygame.Surface((40, 40), pygame.SRCALPHA)
        pygame.draw.circle(self.image, PLAYER_COLOR, (20, 20), 20)  # Draw a circle for the player
        self.rect = self.image.get_rect(center=(WIDTH // 2, HEIGHT - 50))
        self.speed = 5

    def update(self):
        keys = pygame.key.get_pressed()

        # Horizontal movement
        if keys[pygame.K_LEFT]:
            self.rect.x -= self.speed
        if keys[pygame.K_RIGHT]:
            self.rect.x += self.speed

        # Vertical movement
        if keys[pygame.K_UP]:
            self.rect.y -= self.speed
        if keys[pygame.K_DOWN]:
            self.rect.y += self.speed

        # Keep player within screen bounds
        self.rect.x = max(0, min(self.rect.x, WIDTH - self.rect.width))
        self.rect.y = max(0, min(self.rect.y, HEIGHT - self.rect.height))  # Prevent going off-screen vertically

# Bubble class
class Bubble(pygame.sprite.Sprite):
    def __init__(self):
        super().__init__()
        self.image = pygame.Surface((30, 30), pygame.SRCALPHA)
        pygame.draw.circle(self.image, BUBBLE_COLOR, (15, 15), 15)  # Draw a bubble
        pygame.draw.circle(self.image, (255, 255, 255), (15, 15), 10)  # Add a glossy effect in the middle
        self.rect = self.image.get_rect(
            center=(random.randint(15, WIDTH - 15), random.randint(15, HEIGHT - 15))
        )

# AI-controlled player
class AIPlayer(pygame.sprite.Sprite):
    def __init__(self):
        super().__init__()
        self.image = pygame.Surface((40, 40), pygame.SRCALPHA)
        pygame.draw.circle(self.image, AI_COLOR, (20, 20), 20)  # Draw a circle for AI player
        self.rect = self.image.get_rect(center=(WIDTH // 2, HEIGHT - 50))
        self.speed = 4  # Slightly slower than player for balance

    def update(self, bubbles, player):
        # Move AI towards the closest bubble if bubbles exist
        if bubbles:
            # Calculate distance to each bubble manually
            closest_bubble = min(bubbles, key=lambda bubble: (
                (self.rect.centerx - bubble.rect.centerx) ** 2 + 
                (self.rect.centery - bubble.rect.centery) ** 2
            ))
            dx = closest_bubble.rect.centerx - self.rect.centerx
            dy = closest_bubble.rect.centery - self.rect.centery
            distance = max((dx ** 2 + dy ** 2) ** 0.5, 1)  # Avoid division by zero
            self.rect.x += self.speed * (dx / distance)
            self.rect.y += self.speed * (dy / distance)

        # Check if AI gets too close to the player and temporarily stop or change direction
        if self.rect.colliderect(player.rect):
            self.speed = 0  # AI stops when it collides with player
        else:
            self.speed = 4  # Reset speed if not colliding

# Initialize player, AI, and groups
player = Player()
ai_player = AIPlayer()
bubbles = pygame.sprite.Group()
all_sprites = pygame.sprite.Group(player, ai_player)
clock = pygame.time.Clock()

# Game variables
running = True
player_score = 0
ai_score = 0
font = pygame.font.SysFont(None, 36)

# Main game loop
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # Update player
    player.update()
    # Update AI separately with bubbles argument
    ai_player.update(bubbles, player)

    # Randomly add bubbles with a reduced frequency
    if random.randint(1, 50) == 1:
        bubble = Bubble()
        bubbles.add(bubble)
        all_sprites.add(bubble)

    # Collision detection for player
    player_hits = pygame.sprite.spritecollide(player, bubbles, True)
    player_score += len(player_hits)

    # Collision detection for AI
    ai_hits = pygame.sprite.spritecollide(ai_player, bubbles, True)
    ai_score += len(ai_hits)

    # Drawing everything
    screen.fill(WHITE)  # Clear screen with white
    draw_gradient_background()  # Draw the gradient background
    all_sprites.draw(screen)

    # Display scores
    player_score_text = font.render(f"Player Score: {player_score}", True, BLACK)
    ai_score_text = font.render(f"AI Score: {ai_score}", True, AI_COLOR)
    screen.blit(player_score_text, (10, 10))
    screen.blit(ai_score_text, (10, 50))

    pygame.display.flip()
    clock.tick(30)  # Lower frame rate to reduce CPU usage

pygame.quit()

```

### Output :

![games_mini_project](https://github.com/user-attachments/assets/9bf1cb65-f62d-4248-819c-a0cf11796542)

### Result :

Thus, the "Bubble Popper: A 2D Frenzy" game with player and AI interaction was successfully created.

                                                                                                              
