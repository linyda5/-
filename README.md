from pygame import *

back = (200,255,255)
win_width = 600
win_heigh = 500
window = display.set_mode((win_width, win_heigh))
window.fill(back)


clock = time.Clock()
FPS = 60 
game = True
finish = False

class GameSprite(sprite.Sprite):
   def __init__(self, player_image, player_x, player_y, player_speed, wight, height):
       super().__init__()
       self.image = transform.scale(image.load(player_image), (wight, height)) 
       self.speed = player_speed
       self.rect = self.image.get_rect()
       self.rect.x = player_x
       self.rect.y = player_y


   def reset(self):
       window.blit(self.image, (self.rect.x, self.rect.y))




class Player(GameSprite):
   def update_r(self):
       keys = key.get_pressed()
       if keys[K_UP] and self.rect.y > 5:
           self.rect.y -= self.speed
       if keys[K_DOWN] and self.rect.y < win_height - 80:
           self.rect.y += self.speed
   def update_l(self):
       keys = key.get_pressed()
       if keys[K_w] and self.rect.y > 5:
           self.rect.y -= self.speed
       if keys[K_s] and self.rect.y < win_height - 80:
           self.rect.y += self.speed



rack1 = Player('png-transparent-badminton-racket-shuttlecock-badminton-racket-glass-sport-sporting-goods', 30, 200, 4, 50, 150) 
rack2 = Player('png-transparent-badminton-racket-shuttlecock-badminton-racket-glass-sport-sporting-goods', 520, 200, 4, 50, 150)
ball = GameSprite('ball.png', 200, 200, 4, 50, 50)


while game:
    for e in event.get():
        if e.type == QUIT:
            game = False
    if finish != True:
        window.fill(back)
        rack1.update_l()
        rack2.update_r()
        rack1.reset()
        rack2.reset()
        ball.reset()
        
        
        

    display.update()
    clock.tick(FPS)
-
