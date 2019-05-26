# ping-pong-game
created a ping pong name

#turn this into my first AI program 
#test as you go (step by step)
import turtle

wn = turtle.Screen()
wn.title("Dave's Ping Pong Game")
wn.bgcolor("black")
wn.setup(width=800, height=600)
wn.tracer(0) 						#stops window from updating to speed up games 

#score 
score_a = 0
score_b = 0

#paddle 1
paddle_a = turtle.Turtle()			#module followed by class name
paddle_a.speed(0)					#speed of animation
paddle_a.shape("square")
paddle_a.color("cyan")
paddle_a.shapesize(stretch_wid=5,stretch_len=1)			#object is 20x2
														#stretching width by x5
paddle_a.penup()															
paddle_a.goto(-350,0)


#paddle 2
paddle_b = turtle.Turtle()			#module followed by class name
paddle_b.speed(0)					#speed of animation
paddle_b.shape("square")
paddle_b.color("purple")
paddle_b.shapesize(stretch_wid=5,stretch_len=1)			#object is 20x2
														#stretching width by x5
paddle_b.penup()															
paddle_b.goto(350,0)				#paddle is now on the right


#ball
ball = turtle.Turtle()			#module followed by class name
ball.speed(0)					#speed of animation
ball.shape("circle")
ball.color("yellow")

ball.penup()															
ball.goto(0,0)
ball.dx = 1					#every time ball moves, it moves by 0.2 pixels
ball.dy = -1


#pen (used for scoring)
pen = turtle.Turtle()
pen.speed(0)
pen.color("white")
pen.penup()
pen.hideturtle()
pen.goto(0,260)
pen.write("Autobots: 0 Decepticons: 0", align="center", font=("Helvetica", 24, "normal"))

#functions
#paddle_a
def paddle_a_up():
	y = paddle_a.ycor()			#ycor method is from turtle method. returns y coordinate
	y += 100						#adds twenty pixels to y coordinate
	paddle_a.sety(y)
	
def paddle_a_down():
	y = paddle_a.ycor()			#ycor method is from turtle method. returns y coordinate
	y -= 100						#adds twenty pixels to y coordinate
	paddle_a.sety(y)
	
#paddle_b
def paddle_b_up():
	y = paddle_b.ycor()			#ycor method is from turtle method. returns y coordinate
	y += 100						#adds twenty pixels to y coordinate
	paddle_b.sety(y)
	
def paddle_b_down():
	y = paddle_b.ycor()			#ycor method is from turtle method. returns y coordinate
	y -= 100						#adds twenty pixels to y coordinate
	paddle_b.sety(y)
	
# keyboard binding 
wn.listen()							#listen to keyboard input
wn.onkeypress(paddle_a_up, "w")		#when user pres w call paddle_a_up
wn.onkeypress(paddle_a_down, "s")

wn.onkeypress(paddle_b_up, "Up")		#when user pres Up call paddle_b_up
wn.onkeypress(paddle_b_down, "Down")
#main game loop 
'''every time loop run, update screen'''
while True:
	wn.update()	
	
	#move the ball
	ball.setx(ball.xcor() + ball.dx)	#get current x coordinate 			
	ball.sety(ball.ycor() + ball.dy)		
	
	#border checking
	#up and down
	if ball.ycor() > 290:
		ball.sety(290)
		ball.dy *= -1					#reverses direction of ball
		
	if ball.ycor() < -290:
		ball.sety(-290)
		ball.dy *= -1					#reverses direction of ball
		
	#border checking
	#left and right
	if ball.xcor() > 390: 
		ball.goto(0,0)					#reset to 0,0
		ball.dx *= -1
		score_a += 1					#add one to player a's score
										#before calling the pen.write
										#clear the score to input a new one
		pen.clear()
		pen.write("Autobots: {} Decepticons: {}".format(score_a, score_b), align="center", font=("Helvetica", 24, "normal"))
		
	if ball.xcor() < -390: 
		ball.goto(0,0)					#reset to 0,0
		ball.dx *= -1
		score_b += 1
		
		pen.clear()
		pen.write("Autobots: {} Decepticons: {}".format(score_a, score_b), align="center", font=("Helvetica", 24, "normal"))
		
		
	#paddle and ball collisions
	if (ball.xcor() > 340 and ball.xcor() < 350) and (ball.ycor() < paddle_b.ycor() + 40 and ball.ycor() > paddle_b.ycor() - 40):
		ball.setx(340)
		ball.dx *= -1
		
	if (ball.xcor() < -340 and ball.xcor() < -350) and (ball.ycor() < paddle_a.ycor() + 40 and ball.ycor() > paddle_a.ycor() - 40):
		ball.setx(-340)
		ball.dx *= -1
