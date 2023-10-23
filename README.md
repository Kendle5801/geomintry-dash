import pygame
import os
#initilize pygame
pygame.init()

#global cconstants
SCREEN_HIEGHT = 600
SCREEN_WIDTH = 1100

#setting up the screen
SCREEN = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HIEGHT))

#getting charecters
RUNNING = [pygame.image.load( "EdRun.png")]
JUMPING = [pygame.image.load("EdJump.png")]
DUCKING = [pygame.image.load("EdDuck.png")]

#obsticals
Renesme = [pygame.image.load("Renesme.png")]
ripshirt = [pygame.image.load("ripshirt.png")]
victoria = [pygame.image.load("victoria.png")]

#background
BG = pygame.image.load("bg.png")

#Initalizing the game
def main():
    run = True
    clock = pygame.time.Clock()
    player = Edward()

    while run:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                run = False
        
        SCREEN.fill((255,255,255))
        userInput = pygame.key.get_pressed()

        player.draw(SCREEN)
        player.update(userInput)

        pygame.display.update()
        clock.tick(30)

#Setting up the character
class Edward:
    X_POS = 80
    Y_POS = 310

#Making the character move
    def __init__(self):
        self.run_img = RUNNING
        self.jump_img = JUMPING
        self.duck_img = DUCKING

        self.ed_run = True
        self.ed_jump = False
        self.ed_duck = False

        self.step_index = 0
        self.image = self.run_img[0]
        self.ed_rect = self.image.get_rect()
        self.ed_rect.x = self.X_POS
        self.ed_rect.y = self.Y_POS

    #Setting up Movement
    def update(self, userinput):
        if self.ed_run:
            self.run()
        if self.ed_jump:
            self.jump()
        if self.ed_duck:
            self.duck()
        if self.step_index >= 10:
                self.step_index = 0      
     #Getting user input for movement            
        if userinput[pygame.K_UP] and not self.ed_jump: 
            self.ed_jump = True
            self.ed_duck = False
            self.ed_run = False
        elif userinput[pygame.K_DOWN] and not self.ed_jump:
            self.ed_duck = True
            self.ed_run = False
            self.ed_jump = False
        elif not (self.ed_jump or userinput[pygame.K_DOWN]):
            self.ed_run = True
            self.ed_duck = False
            self.ed_jump = False
#Setting up the duck animation
    def duck(self):
        pass

#Setting up the run animation
    def run(self):
        self.image = self.run_img[self.step_index // 5]
        self.ed_rect = self.image.get_rect()
        self.ed_rect.x = self.X_POS
        self.ed_rect.y = self.Y_POS
        self.step_index += 1

#Setting up the jump animation    
    def jump(self):
        pass
           
      
    def draw(self, SCREEN):
        SCREEN.blit(self.image, (self.ed_rect.x, self.ed_rect.y))
      

main()







# geomintry-dash
