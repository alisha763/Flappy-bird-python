Re-import required modules after environment reset

import os import shutil

Re-create the demo project directory and files

project_path = "/mnt/data/flappy-bird-python" os.makedirs(project_path, exist_ok=True)

Python script for the Flappy Bird game (main.py)

main_py_code = ''' import pygame import random import sys

pygame.init()

Screen settings

WIDTH, HEIGHT = 400, 600 screen = pygame.display.set_mode((WIDTH, HEIGHT)) pygame.display.set_caption("Flappy Bird - Demo by Alisha")

Colors and fonts

WHITE = (255, 255, 255) clock = pygame.time.Clock() font = pygame.font.SysFont(None, 40)

Bird settings

bird = pygame.Rect(100, 250, 30, 30) gravity = 0.5 bird_movement = 0

Pipe settings

pipe_width = 70 pipe_gap = 200 pipes = []

def draw_pipes(pipes): for pipe in pipes: pygame.draw.rect(screen, (0, 255, 0), pipe)

def move_pipes(pipes): for pipe in pipes: pipe.x -= 5 return [pipe for pipe in pipes if pipe.x + pipe_width > 0]

def create_pipe(): height = random.randint(100, 400) top = pygame.Rect(WIDTH, 0, pipe_width, height) bottom = pygame.Rect(WIDTH, height + pipe_gap, pipe_width, HEIGHT - height - pipe_gap) return top, bottom

Main game loop

def main(): global bird_movement score = 0 pipes.extend(create_pipe()) running = True

while running:
    screen.fill(WHITE)
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()
        if event.type == pygame.KEYDOWN and event.key == pygame.K_SPACE:
            bird_movement = -8

    bird_movement += gravity
    bird.y += int(bird_movement)

    # Pipe management
    if pipes[-1].x < 200:
        pipes.extend(create_pipe())
    pipes[:] = move_pipes(pipes)

    # Collision
    for pipe in pipes:
        if bird


