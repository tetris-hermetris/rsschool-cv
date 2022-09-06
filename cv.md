# Max Ilinov
## Contact info

* **e-mail:** [ilimaksim@gmail.com](ilimaksim@gmail.com)
* **GitHub:** [tetris-hermetris](https://github.com/tetris-hermetris)
* **Telegram** [@mylittleposter](https://t.me/mylittleposter)

## About me

I'm a typeface designer and typographic researcher with the interest in programming languages and technology in general.

I find inspiration in the origins of computer graphics, pre-Petrine writing forms and mid XX century european modernism.

Doing an ongoing research on reading process as perception of forms and ratios.

## Skills

 - Python
 - [fontTools](https://github.com/fonttools/fonttools)
 - [fontParts](https://github.com/robotools/fontParts)
 - [drawBot](https://github.com/typemytype/drawbot) / [drawbot-skia](https://github.com/justvanrossum/drawbot-skia)
 - Robofont scripting

## Code example

I like to experiment with generative graphics! The following code, if run as a drawBot script, will output a gif animation with cubes of random colors:

```python
from itertools import product

def cube(x, y, s, colors):
    fill(*colors[0])
    polygon((x, y+s/6), (x-s/2, y+s/3), (x, y+s/2), (x+s/2, y+s/3))
    fill(*colors[1])
    polygon((x, y+s/6), (x-s/2, y+s/3), (x-s/2, y-s/3), (x, y-s/2))
    fill(*colors[2])
    polygon((x, y+s/6), (x+s/2, y+s/3), (x+s/2, y-s/3), (x, y-s/2))

sign = lambda a: (a>0) - (a<0)

rColr = lambda: choice([0.0, 0.75, 1.0])

size = 18
offset = 22

palette = [(rColr(), rColr(), rColr()) for i in range(16)]    

for k in range(0, 314*2, 6):
    k = k / 100
    newPage(500, 500)
    back = palette[0]
    fill(*back)
    rect(0,0,width(), height())
    # scale(.75, center=(width()/2, width()/2))
    # translate(0, 150)
    x0, y0 = width()//2, height()//2
    for x in range(x0-size*offset+size, x0+size*offset, size):
        for y in range(y0-size*offset+size, y0+size*offset, size):
            change_color = not k % 10
            translate(0, -size/offset/10)
            sx, sy = sign(x-x0), sign(y-y0)
            x_, y_ = x - size/2.0*sy*cos(k+y), y - size/2*sx*sin(k-x)
            color_shift =  round(abs((sin((y_/(111*sin(k+1)) + k + sin(k)*10) * cos(x_/333 - k))) + 1) * 2) % (len(palette) - 3)
            if x_ + size > 0 and \
               x_ - size < width() and\
               y_ - size > 0:
                   cube(x_, y_, size, palette[-3-color_shift:])

saveImage('cubes.gif')
```

Output:

![img](assets/cubes.gif)