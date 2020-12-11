import random
import pygame
pygame.init()
import tkinter
from tkinter import messagebox

#class for creating a snake
class Snake():

    #starting position, starting direction, color, length, score and high score
    def __init__(self):
        self.positions = [(random.randint(0, int(width /20 ) -1) *20, random.randint(0, int(height / 20) - 1) * 20)]
        self.direction = right
        self.color = (0, 255, 0)
        self.length = 1
        self.score = 0
        self.highScore = []

    #adds the next position to positions, where the snake is heading and pops the first position from positions
    #moves snake from one side to another
    #if snake hits itself, restarts the game
    def move(self):
        newPos = (((self.positions[0][0] + (20 * self.direction[1])) % width),
                  ((self.positions[0][1] + (20 * self.direction[0])) % height))
        self.positions.insert(0, newPos)
        if len(self.positions) > 2 and newPos in self.positions[2:]:
            self.restart()
        elif len(self.positions) > self.length:
            self.positions.pop()

    #gives score and high score on a message box
    #restarts the game to the initial state
    def restart(self):
        running = False
        score = self.score
        self.highScore.append(score)
        highScore = max(self.highScore)
        message1 = 'You ate yourself!'
        message2 = 'Score: ' + str(score) + '\nHigh Score: ' + str(highScore) + '\nPress ok to play again'
        message_box(message1, message2)
        self.positions = [(random.randint(0, int(width / 20) - 1) * 20, random.randint(0, int(height / 20) - 1) * 20)]
        self.direction = right
        self.length = 1
        self.score = 0

    #turns snake if a key is pressed
    #allows also to quit from the main loop
    def turn(self):
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.quit()
            elif event.type == pygame.KEYDOWN:
                if event.key == pygame.K_UP:
                    self.direction = up
                elif event.key == pygame.K_RIGHT:
                    self.direction = right
                elif event.key == pygame.K_DOWN:
                    self.direction = down
                elif event.key == pygame.K_LEFT:
                    self.direction = left

    #draws rectancle for each position in positions
    def draw(self, surface):
        for pos in self.positions:
            rect = pygame.Rect((pos[0], pos[1]), (20, 20))
            pygame.draw.rect(surface, (self.color), rect)

# directions a snake can go
up = (-1, 0)
right = (0, 1)
down = (1, 0)
left = (0, -1)
running = True

#class for creating apples
class Apple():

    def __init__(self):
        self.position = (random.randint(0, int(width / 20) - 1) * 20, random.randint(0, int(height / 20) - 1) * 20)
        self.color = (random.randrange(0, 255), random.randrange(0, 255), random.randrange(0, 255))

    #changes apple's position and color
    def newApple(self, snake):
        s = snake
        self.position = (random.randint(0, int(width / 20) - 1) * 20, random.randint(0, int(height / 20) - 1) * 20)
        self.color = (random.randrange(0, 255), random.randrange(0, 255), random.randrange(0, 255))
        if self.position in s.positions:
            self.newApple(s)

    #draws apple (rectangle)
    def draw(self, surface):
        rect = pygame.Rect((self.position[0], self.position[1]), (20, 20))
        pygame.draw.rect(surface, self.color, rect)


#function to draw a white surface
def draw(surface):
    color = (255, 255, 255)
    surface.fill(color)

#message box for end message
def message_box(subject, content):
    root = tkinter.Tk()
    root.attributes("-topmost", True)
    root.withdraw()
    messagebox.showinfo(subject, content)
    try:
        root.destroy()
    except:
        pass

# main loop for running the game
def main():
    global height, width, snake
    width = 400
    height = 400

    clock = pygame.time.Clock()

    screen = pygame.display.set_mode((width, height))
    pygame.display.set_caption('Snake')

    surface = pygame.Surface(screen.get_size())

    snake = Snake()
    apple = Apple()

    # draws & calls for methods if snake finds apple
    while running:
        clock.tick(10)
        snake.turn()
        if snake.positions[0] == apple.position:
            apple.newApple(snake)
            snake.length += 1
            snake.score += 1
        draw(surface)
        snake.move()
        snake.draw(surface)
        apple.draw(surface)
        screen.blit(surface, (0, 0))
        text = pygame.font.SysFont(None, 30).render("Score {0}".format(snake.score), True, (0, 0, 0))
        screen.blit(text, (5, 5))
        pygame.display.flip()

main()
