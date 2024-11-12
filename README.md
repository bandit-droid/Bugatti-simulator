# Bugatti-simulator
bugatti veyron simulator
pip install pygame
import pygame
import sys

# Initialize Pygame
pygame.init()

# Screen settings
SCREEN_WIDTH, SCREEN_HEIGHT = 800, 600
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("Bugatti Veyron Roaming the Street")

# Colors
WHITE = (255, 255, 255)
GRAY = (50, 50, 50)
BLUE = (0, 0, 255)

# Car settings
CAR_WIDTH, CAR_HEIGHT = 60, 120
car_x, car_y = SCREEN_WIDTH // 2 - CAR_WIDTH // 2, SCREEN_HEIGHT - CAR_HEIGHT - 10
car_speed = 5

# Street lines settings
LINE_WIDTH, LINE_HEIGHT = 10, 50
line_x = SCREEN_WIDTH // 2 - LINE_WIDTH // 2
line_y = 0
line_speed = 5

# Game loop
running = True
clock = pygame.time.Clock()

while running:
    # Event handling
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # Control car with arrow keys
    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT] and car_x > 0:
        car_x -= car_speed
    if keys[pygame.K_RIGHT] and car_x < SCREEN_WIDTH - CAR_WIDTH:
        car_x += car_speed
    if keys[pygame.K_UP] and car_y > 0:
        car_y -= car_speed
    if keys[pygame.K_DOWN] and car_y < SCREEN_HEIGHT - CAR_HEIGHT:
        car_y += car_speed

    # Update line position to simulate movement
    line_y += line_speed
    if line_y > SCREEN_HEIGHT:
        line_y = -LINE_HEIGHT

    # Draw background and street
    screen.fill(GRAY)

    # Draw lane divider line
    for offset in range(0, SCREEN_HEIGHT, LINE_HEIGHT * 2):
        pygame.draw.rect(screen, WHITE, (line_x, line_y + offset, LINE_WIDTH, LINE_HEIGHT))

    # Draw the car (as a rectangle for simplicity)
    pygame.draw.rect(screen, BLUE, (car_x, car_y, CAR_WIDTH, CAR_HEIGHT))

    # Update display
    pygame.display.flip()
    clock.tick(30)

# Quit Pygame
pygame.quit()
sys.exit()
