Разчитане на бутоните на мишката
--------------------------------

Информация за текущо натиснатите бутони на мишката се предоставя от функцията ``pg.mouse.get_press()``. Тази функция връща набор от три елемента (подреден троен), които се използват като логически стойности. Елементите на кортежа съответстват съответно на левия, средния и десния бутон на мишката. Стойност *True* показва, че в момента е натиснат бутон, и *False*, че не е.

Примерът по-долу показва как да четете кои бутони на мишката се натискат. Това е частта от програмата, където това се случва:

.. activecode:: PyGame__interact_put_ball_into_box_part
    :passivecode: true

    pressed_mouse_button = pg.mouse.get_pressed()

    if pressed_mouse_button[2]: # right button - new game
        (x, y) = (width//2, height//2) # return the ball to the center
        won, lost = False, False # the player has neither won nor lost
        
    if pressed_mouse_button[0]: # left button - move the ball
        (xm, ym) = pg.mouse.get_pos() # mouse position coordinates
        # the ball moves away from the mouse for another half of that distance
        x = x - 0.5 * (xm - x)
        y = y - 0.5 * (ym - y)

Комплектът *pressed_mouse_button* получава три стойности, върнати чрез функцията *pg.mouse.get_press()*. Тогава обикновено използваме тези стойности в операторите *if*. Например *if pressed_mouse_button[2]* означава "ако е натиснат десен бутон" (0 за ляво, 1 за средно и 2 за дясно).

Примери и задачи
''''''''''''''''''

.. questionnote::

    **Пример - сложете топката в кутията** 
    
    Докато левият бутон на мишката се държи натиснат, топката се отдалечава от курсора. Целта е да поставите топката в червената кутия, като преместите мишката и натиснете левия бутон. Натискането на десния бутон връща играта в началото.
    
Първо изучете внимателно функцията *new_frame()* и след това разгледайте и останалите части на кода. Изпробвайте програмата и вижте дали работи, както сте очаквали, след като прочетете описанието.

.. activecode:: PyGame__interact_put_ball_into_box
    :nocodelens:
    :enablecopy:
    :modaloutput:
    :includesrc: src/PyGame/3_Interaction/3b_Mouse_readkey/put_ball_into_box.py    



.. questionnote::

    **Задача - до и от мишката:** 
    
     Завършете програмата, така че да работи както е показано в примера (бутон „Play Task“).
     
    - Когато се натисне левия бутон на мишката, топката трябва да се отдалечи от мишката, както в примера „поставете топката в полето“ по-горе, но не на половин разстояние, а само на една десета от разстоянието до мишката.
    - Когато левият бутон на мишката не е натиснат, топката трябва да се приближи с една десета от разстоянието до мишката (както в задачата „към мишката“ в предишния урок).

.. activecode:: PyGame__interact_to_and_from_mouse
    :nocodelens:
    :modaloutput:
    :playtask:
    :includehsrc: src/PyGame/3_Interaction/3b_Mouse_readkey/to_and_from_mouse.py
    
    import pygame as pg, pygamebg
    (width, height) = (400, 400)
    canvas = pygamebg.open_window(width, height, "Ball following the mouse")

    (x, y) = (width // 2, height // 2) # ball starts from center of the window

    def new_frame():
        global x, y
        
        # ADD THE MISSING PART
        
        # draw a green ball on a white background
        canvas.fill(pg.Color("white")) 
        pg.draw.circle(canvas, pg.Color("green"), (int(x), int(y)), 10)

    pygamebg.frame_loop(50, new_frame)


.. questionnote::

    **Задача - лазер:** 
    
    Завършете програмата, така че да работи както е показано в примера (бутон „Play Task“).
    
    Докато левият бутон на мишката се държи натиснат, "лазерът" е включен, в противен случай той е изключен. Докато лазерът е включен, енергията му намалява с 1 (но не под 0), а когато е изключена, енергията се увеличава с 2 (но не над 100).


.. activecode:: PyGame__interact_laser
    :nocodelens:
    :modaloutput:
    :playtask:
    :includehsrc: src/PyGame/3_Interaction/3b_Mouse_readkey/laser.py

    import pygame as pg, pygamebg
    width, height = 400, 400
    canvas = pygamebg.open_window(width, height, "Laser")

    laser_on = False
    energy = 25 # how full is the laser from 0 to 100

    def draw():
        canvas.fill(pg.Color("black")) # background
        
        # the indicator shows how full the laser is
        pg.draw.rect(canvas, pg.Color("green"), (10, 10, 100, 10), 1)
        pg.draw.rect(canvas, pg.Color("green"), (10, 10, energy, 10))
        
        if laser_on:
            reach = (4 * energy, height - 4 * energy)
            pg.draw.line(canvas, pg.Color("red"), (0, height), reach, 5)
        
    def new_frame():
        global energy, laser_on
        
        # READ THE STATE OF THE LEFT MOUSE BUTTON AND SET THE VALUES
        # OF THE GLOBAL VARIABLES energy, laser_on

        draw()

    pygamebg.frame_loop(15, new_frame)


.. commented out

    .. questionnote::

        **Задача - цвят на фона:** Този прост пример само илюстрира четенето на състоянието на бутоните на мишката. Докато левият бутон е натиснат, фонът става по-светъл, а докато десният бутон е натиснат, фонът става по-тъмен.
                

    .. activecode:: PyGame__interact_bg_color
        :nocodelens:
        :modaloutput:
        :includesrc: src/PyGame/3_Interaction/3b_Mouse_readkey/bg_color.py

