---
layout: post
title: Drawing with Python
---

In this program, I use python to draw a spiral on the screen.

```python
import turtle
import random

screen = turtle.Screen()
screen.colormode(255)
branches_drawn = 0
max_branches = 15

colors = [(79, 133, 49), (136, 189, 75), (187, 217, 114)]

def draw_branches(m, start_angle, branch_point):
    # we can use a global variable to keep track of something
    # across the whole program
    global branches_drawn
    m.color(random.choice(colors))
    if(branches_drawn > max_branches):
        # if we've draw all we want stop recursing
        return
    else:
        # draw 2 new branches and decide where to add the next one
        branches_drawn = branches_drawn + 1
        end_points = []

        # draw left branch
        m.up()
        m.goto(branch_point)
        # tilt the branch
        m.setheading(start_angle + 5 * branches_drawn)
        m.down()
        # jitter
        m.left(20 + random.randint(-5, 5))
        m.forward(20)
        end_points.append((m.xcor(), m.ycor()))

        # draw right branch
        m.up()
        m.goto(branch_point)
        # tilt the branch
        m.setheading(start_angle + 5 * branches_drawn)
        m.down()
        # jitter
        m.right(20 + random.randint(-5, 5))
        m.forward(20)
        end_points.append((m.xcor(), m.ycor()))

        # draw a set of branches at the endpoint of either the right or left
        draw_branches(m, start_angle, end_points[random.randint(0, 1)])


marker = turtle.Turtle()

# draw branches along 5 lines
for i in range(5):
    branches_drawn = 0
    angle = 360 - (360/5)*i
    draw_branches(marker, angle, (-100, -50))

screen.exitonclick()
```
