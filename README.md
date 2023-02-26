import pygame
import random

# Initialize Pygame
pygame.init()

# Set the game window dimensions
window_width = 400
window_height = 400

# Set the colors
black = (0, 0, 0)
white = (255, 255, 255)
green = (0, 255, 0)

# Create the game window
game_window = pygame.display.set_mode((window_width, window_height))

# Set the game title
pygame.display.set_caption('Snake Game')

# Set the clock
clock = pygame.time.Clock()

# Set the font for the score
font_style = pygame.font.SysFont(None, 30)

def display_score(score):
    score_text = font_style.render("Score: " + str(score), True, black)
    game_window.blit(score_text, [0, 0])

# Set the snake size and speed
snake_size = 10
snake_speed = 15

# Define the snake function
def snake(snake_size, snake_list):
    for x in snake_list:
        pygame.draw.rect(game_window, green, [x[0], x[1], snake_size, snake_size])

# Define the game loop
def game_loop():
    game_over = False
    game_close = False

    # Set the initial position of the snake
    x1 = window_width / 2
    y1 = window_height / 2

    # Set the initial change in position of the snake
    x1_change = 0
    y1_change = 0

    # Create the initial snake list
    snake_list = []
    length_of_snake = 1

    # Set the initial position of the food
    food_x = round(random.randrange(0, window_width - snake_size) / 10.0) * 10.0
    food_y = round(random.randrange(0, window_height - snake_size) / 10.0) * 10.0

    # Start the game loop
    while not game_over:

        # Check if the game is over
        while game_close == True:
            game_window.fill(white)
            score = length_of_snake - 1
            display_score(score)
            message = font_style.render("You Lost! Press Q-Quit or C-Play Again", True, black)
            game_window.blit(message, [window_width/6, window_height/3])
            pygame.display.update()

            # Wait for user input to play again or quit
            for event in pygame.event.get():
                if event.type == pygame.KEYDOWN:
                    if event.key == pygame.K_q:
                        game_over = True
                        game_close = False
                    if event.key == pygame.K_c:
                        game_loop()

        # Get events from the user
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                game_over = True
            if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_LEFT:
                    x1_change = -snake_size
                    y1_change = 0
                elif event.key == pygame.K_RIGHT:
                    x1_change = snake_size
                    y1_change = 0
                elif event.key == pygame.K_UP:
                    y1_change = -snake_size
                    x1_change
