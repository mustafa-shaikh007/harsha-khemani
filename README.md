import turtle


wn = turtle.Screen()
wn.title("Ping Pong ball")                  
wn.bgcolor("black")                           
wn.setup(width=800, height=600)         
wn.tracer(0)                                  # animation will be  set to zero              

# Score
Score_a = 0 
Score_b = 0


# Paddle A
paddle_a = turtle.Turtle()
paddle_a.speed(0)
paddle_a.shape("square")
paddle_a.color("red")
paddle_a.shapesize(stretch_wid=5, stretch_len=1)
paddle_a.penup()                                        # this is eliminate the lining caused by the movieing of the paddle
paddle_a.goto(-350,0)



# Paddle B
paddle_b = turtle.Turtle()
paddle_b.speed(0)
paddle_b.shape("square")
paddle_b.color("red")
paddle_b.shapesize(stretch_wid=5, stretch_len=1)
paddle_b.penup()
paddle_b.goto(350,0)

# Ball
Ball = turtle.Turtle()
Ball.speed(0)
Ball.shape("circle")
Ball.color("white")
Ball.penup()
Ball.goto(0,0)
Ball.dx = 0.30                                          # speed \ animation of the ball at x-coordinate 
Ball.dy = -0.30                                         # speed \ animation of the ball at y-coordinate


# pen
pen = turtle.Turtle()
pen.speed(0)
pen.color('white')
pen.penup()
pen.hideturtle()                                      # this will hide the turtle of the score
pen.goto(0, 260)
pen.write("Player A: 0  Player B: 0", align="center", font=("courier", 24, "bold"))



# Function
def paddle_a_up():
    y = paddle_a.ycor()                                   # movement of the paddle A at y-coordinate in upward direction 
    y += 20                                   
    paddle_a.sety(y)                                      # sets the new position of the paddle A at y-coordinate in upward direction


def paddle_a_down():
    y = paddle_a.ycor()                                   # movement of the paddle A at y-coordinate in downward direction
    y -= 20
    paddle_a.sety(y)                                      # sets the new position of the paddle A at y-coordinate in downward direction



def paddle_b_up():
    y = paddle_b.ycor()                                   # movement of the paddle B at y-coordinate in upward direction                                   
    y += 20
    paddle_b.sety(y)                                      # sets the new position of the paddle B at y-coordinate in upward direction


def paddle_b_down():
    y = paddle_b.ycor()                                  # movement of the paddle B at y-coordinate in downward direction
    y -= 20
    paddle_b.sety(y)                                     # sets the new position of the paddle B at y-coordinate in downward direction

# keyboard binding
wn.listen()                                               # this function listnes what we press on the keyboard
wn.onkeypress(paddle_a_up, "w")                           # onkeypress is the function which moves the paddle when we press the key 
wn.onkeypress(paddle_a_down, "s")
wn.onkeypress(paddle_b_up, "Up")
wn.onkeypress(paddle_b_down, "Down")


# main game loop
while True:
    wn.update()                                         # this updates the game on every animtion or move 




   # move the Ball
   Ball.setx(Ball.xcor() + Ball.dx)                    # this sets the new postion of the ball moving at x-coordinate
   Ball.sety(Ball.ycor() + Ball.dy)                    # this sets the new positon of the ball moving at y-coordinate


   # Border Checking
   if  Ball.ycor() > 290:                             # this is used for the colision of the ball at the boder of y +ve coordinate 
        Ball.sety(290)
        Ball.dy *= -1


   if  Ball.ycor() < -290:                            # this is used for the collision of the ball at the border of y -ve coordinate
        Ball.sety(-290)
        Ball.dy *= -1  


   if  Ball.xcor() > 390:                             # this is the position of the ball which is in the center of the screen
        Ball.goto(0,0)
        Ball.dx *= -1
        Score_a += 1                                 #  ball pases the x +ve border the opponent get +1 score 
        pen.clear()                                  # this clears the previous score and updates the recent one 
        pen.write("Player A: {}  Player B: {}".format(Score_a, Score_b), align="center", font=("courier", 24, "bold"))



   if  Ball.xcor() < -390:
        Ball.goto(0,0)
        Ball.dx *= -1
        Score_b += 1
        pen.clear()
        pen.write("Player A: {}  Player B: {}".format(Score_a, Score_b), align="center", font=("courier", 24, "bold"))



   # paddle and ball collision
   if (Ball.xcor() > 340 and Ball.xcor() < 350) and (Ball.ycor() < paddle_b.ycor() + 50 and Ball.ycor() > paddle_b.ycor() -50):
        Ball.setx(340)                                # for the collision of the ball with the paddle B and bounce back
        Ball.dx *= -1

   if (Ball.xcor() < -340 and Ball.xcor() > -350) and (Ball.ycor() < paddle_a.ycor() + 50 and Ball.ycor() > paddle_a.ycor() -50):
        Ball.setx(-340)                              # for the collision of the ball with the paddle A and bounce back 
        Ball.dx *= -1
        
        
        
   ![Screenshot (231)](https://user-images.githubusercontent.com/89350004/130361654-42cbdb8c-aba5-4785-bba3-8750cc378f96.png)

