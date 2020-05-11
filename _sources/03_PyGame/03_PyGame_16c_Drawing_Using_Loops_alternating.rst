
Правяне на по-сложни рисунки с помощта на цикли
------------------------------------------------

Редовността, която искаме да използваме в чертежите, може да бъде по-сложна, сравнена с предишни проблеми. Ето няколко примера:

.. image:: ../../_images/PyGame/repeat_alternating.png 
   :width: 800px
   :align: center 

Във всички тези случаи все още съществува закономерност и може да се използва при писане на програми. Можем също да наблюдаваме, че всички примери на снимката имат нещо общо, което е, че две правила се появяват последователно. Например при тухлена рисунка първият ред от тухли започва с цялата тухла, вторият - с половин тухла, третият отново с цялата тухла и т.н. По същия начин осветените и тонирани прозорци се появяват последователно на чертежа на сградата.

Поради редуването на двете правила във всички чертежи, програмите, които ги рисуват, също ще имат някои прилики. Нека разгледаме примери за код.

Пример - цип
''''''''''''''''


За да нарисуваме такъв цип, със сигурност ще нарисуваме линиите в контур. От чертежа се вижда, че всеки следващ ред е еднакъв брой пиксели по-нисък от предишния, така че не трябва да има проблем с изчисляването на *y* координатата. Ситуацията с *x* координатите е малко по-трудна, защото те се променят според малко по-сложно правило.

Можем да разрешим този проблем, като използваме оператора *if* в цикъла. След като нарисуваме една линия, проверяваме коя от двете възможни стойности :math:`x` координата на началото на реда има. Ако тя има първата стойност - ние я присвояваме втората и обратно. Ето как изглежда в програмата:

.. activecode:: PyGame_drawing_loops_zipper1
   :nocodelens:
   :enablecopy:
   :modaloutput:
   :includesrc: src\PyGame\1_Drawing\7c_Loops_alternating\Examples\zipper1.py

Друга възможност за решаване на проблема с *x* координатите е да нарисувате две линии в един цикъл, например:

.. activecode:: PyGame_drawing_loops_zipper2
   :nocodelens:
   :enablecopy:
   :modaloutput:
   :includesrc: src\PyGame\1_Drawing\7c_Loops_alternating\Examples\zipper2.py


Пример - Тухли
''''''''''''''''

Вече споменахме, че редовете от тухли последователно започват с цялата тухла и половината от тухлата. Ето защо при рисуването на тухли можем да използваме някоя от същите две идеи, както в предишния пример.

Нека дължината на тухлата се обозначава с :math:`a`, а височината й с :math:`h`. Получаваме цялата тухла в началото на реда, като изчертаваме правоъгълник на дадена височина, с :math:`x` координата, равна на нула. Половината от тухла в началото на ред може да се получи, като се изчертае цяла тухла, изместена от :math:`a \ над 2` вляво, тоест чрез начертаване на правоъгълник с: math:` x` координата, равна на :code:`-a // 2`. Така се вижда само дясната половина на тухлата. Остава да се реши, когато нарисуваме изместена тухла и кога обикновена.

Едното решение е да съхранявате началото на реда от тухли в променлива, наречете го *x_start*. След изчертаване на всеки ред проверяваме дали променливата *x_start* има стойност нула или :code:`-a // 2`. Както в предишния пример, независимо от двете стойности, които имаме, ние ще присвоим другата стойност на променливата, така че в следващия ред чертежът на тухлите ще започне различно.

Попълнете незавършени операции за настройка на променливата x_start

.. activecode:: PyGame_drawing_loops_bricks1
    :nocodelens:
    :enablecopy:
    :modaloutput:
    :playtask:
    :includexsrc: src\PyGame\1_Drawing\7c_Loops_alternating\Examples\bricks1.py

    canvas.fill(pg.Color("red"))
    brick_a, brick_h = 80, 40
    x_start = 0
    for y0 in range(0, height, brick_h): # For each row of bricks
        for x0 in range(x_start, width, brick_a): # For each brick in the row
            pg.draw.rect(canvas, pg.Color("black"), (x0, y0, brick_a, brick_h), 1)
            
        if x_start == x_start: # fix the line
            x_start = -brick_a//2
        else:
            x_start = x_start # fix the line

Втората идея е да изчертаем по две тухли на всеки проход през двойния контур: този, който нарисувахме в първото решение, и тухлата отдолу и наполовина от него. Забележете, че в този случай цикълът от *y0* има два пъти стъпката, защото вътрешният цикъл извлича два реда тухли.

Попълнете незавършени изявления за рисуване на правоъгълници

.. activecode:: PyGame_drawing_loops_bricks2
    :nocodelens:
    :enablecopy:
    :modaloutput:
    :includexsrc: src\PyGame\1_Drawing\7c_Loops_alternating\Examples\bricks2.py

    canvas.fill(pg.Color("red"))
    brick_width, brick_height = 80, 40
    for y0 in range(0, height, 2 * brick_height):
        for x0 in range(0, width, brick_width):
            # draw the first brick
            pg.draw.rect(???) # complete the statement as before
            
            # the second brick is in the following row, displaced by half its width
            x1, y1 = x0 - brick_width//2, y0 + brick_height 
            pg.draw.rect(???) # draw the brick below and half-left of the previous one


Задачи за упражнение
'''''''''''''''''''''

.. questionnote:: 

    **Задача-шахматна дъска**

    Начертайте шахматна дъска през целия прозорец (квадратчетата на дъската трябва да са 50х50 пиксела). Долният ляв квадрат трябва да е тъмен. 

По-голямата част от програмата е написана, опитайте се да я завършите.

.. activecode:: PyGame_drawing_loops_chessboard
    :nocodelens:
    :enablecopy:
    :modaloutput:
    :playtask:
    :includexsrc: src\PyGame\1_Drawing\7c_Loops_alternating\Tasks\chessboard1.py
    
    canvas.fill(pg.Color("gray")) # background - light squares
    
    # square size
    num_squares = 8
    square_width = width / num_squares
    square_height = height / num_squares

    # go through all the squares
    for i in range(num_squares):
        for j in range(num_squares):
            # paint black squares only
            if (i + j) % 2 != 0:
                pass # fix the statement


.. questionnote::

    **задача-сграда**

    Променете програмата по-долу, така че прозорците да бъдат нарисувани в двоен цикъл.

Частта, след промяната, може да започва така:

.. code::

    for y in range(5):     # floor
        for x in range(2): # side of the building (0 - left, 1 - right)
            if (x+y) % 2 == 0:
                color = ...


.. activecode:: PyGame_drawing_loops_building_alternating
    :nocodelens:
    :enablecopy:
    :modaloutput:
    :playtask:
    :includexsrc: src\PyGame\1_Drawing\7c_Loops_alternating\Tasks\building_alternating.py
    
    pg.draw.rect(canvas, pg.Color("darkgray"), (120, 50, 60, 140)) # building

    # change this part
    pg.draw.rect(canvas, pg.Color('yellow'), (130,  60, 15, 15))
    pg.draw.rect(canvas, pg.Color('black'), (155,  60, 15, 15))
    pg.draw.rect(canvas, pg.Color('black'), (130,  80, 15, 15))
    pg.draw.rect(canvas, pg.Color('yellow'), (155,  80, 15, 15))
    pg.draw.rect(canvas, pg.Color('yellow'), (130, 100, 15, 15))
    pg.draw.rect(canvas, pg.Color('black'), (155, 100, 15, 15))
    pg.draw.rect(canvas, pg.Color('black'), (130, 120, 15, 15))
    pg.draw.rect(canvas, pg.Color('yellow'), (155, 120, 15, 15))
    pg.draw.rect(canvas, pg.Color('yellow'), (130, 140, 15, 15))
    pg.draw.rect(canvas, pg.Color('black'), (155, 140, 15, 15))

    pg.draw.rect(canvas, pg.Color("black"),  (140, 160, 20, 30))   # door

~~~~

Ако не сте имали големи трудности с всички тези задачи, опитайте се да решите и една по-трудна.

.. questionnote::

    **Задача - предизвикателство: паркет**

    Напишете програма, която показва паркета (можете да видите снимката на паркета, когато щракнете върху бутона „Play Task“, а картината е същата като в началото на тази страница, вдясно). Целта, разбира се, е да нарисувате дъските на пода в множество контури. Размерите на дъската са 10х60, а цветовете са златист и кафяв.
    
Скелетът на програмата най-общо би могъл да изглежда така:

.. code::

    for row ...
        for column ...
            if ...
                for floorboard in range(6):
                    pg.draw.rect(...)
            else:
                for floorboard in range(6):
                    pg.draw.rect(...)


.. activecode:: PyGame_drawing_loops_parquet
    :nocodelens:
    :enablecopy:
    :modaloutput:
    :playtask:
    :includexsrc: src\PyGame\1_Drawing\7c_Loops_alternating\Tasks\parquet.py
