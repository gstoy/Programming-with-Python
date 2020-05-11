
Преместване на чертежа
----------------------

В предишните примери направихме няколко рисунки, съставени от основни форми. По този начин беше необходимо да се определи правилната позиция за всяка от тези форми, за да се поберат всички парчета заедно. За някои чертежи беше възможно (и в някои необходими задачи) координатите на отделните точки да се изчисляват въз основа на известните координати на други точки. Това изчисление можеше да се извърши извън програмата и тогава изчислените координати просто биха могли да бъдат въведени в програмата. По-добре е обаче да извършите такива изчисления в самата програма по няколко причини:

- Може да не изчислим координатите правилно при първия опит. В такава ситуация е по-лесно да промените инструкциите за изчисление (т.е. програмата), отколкото да изчислите всичко ръчно от началото.
- Когато сами създаваме чертежа, може да се окаже, че след първата версия на програмата може да искаме да добавим нещо, например от лявата страна на чертежа, но че нямаме достатъчно място. В този случай целият чертеж трябва да бъде преместен надясно, така че *x* координатите на всички точки да бъдат увеличени с една и съща стойност. Ако ръчно сме изчислили координатите на точките, трябва да ги изчислим отново. При добре организирана програма за рисуване е достатъчно да промените едно число, за да преместите целия чертеж вдясно. Този процес може да се наложи да се повтаря няколко пъти, докато не сме доволни от позицията на изтеглената част, така че да го изпробвате е много по-лесно, когато програмата прави изчислението вместо нас.
- Ако искаме да начертаем един и същ чертеж на няколко места в прозореца, ползите от изчисляването вътре в програмата се появяват отново.

Сега ще систематизираме изчислението на координатите малко повече и ще го използваме за по-лесното преместване на изтеглените обекти. Преди да започнем, би било добре да проверите предисторията и да отговорите на тези въпроси:

.. mchoice:: PyGame__drawing_quiz_point_left
   :answer_a: (50, 60)
   :answer_b: (50, 80)
   :answer_c: (40, 70)
   :answer_d: (60, 70)
   :answer_e: (40, 60)
   :correct: c
   :feedback_a: Try again.
   :feedback_b: Try again.
   :feedback_c: Correct!
   :feedback_d: Try again.
   :feedback_e: Try again.

   Какви са координатите на точка 10 пиксела вляво от точката (50, 70)?

.. mchoice:: PyGame__drawing_quiz_point_down
   :answer_a: (50, 60)
   :answer_b: (50, 80)
   :answer_c: (40, 70)
   :answer_d: (60, 70)
   :answer_e: (40, 60)
   :correct: b
   :feedback_a: Try again.
   :feedback_b: Correct!
   :feedback_c: Try again.
   :feedback_d: Try again.
   :feedback_e: Try again.

   Какви са координатите на точка 10 пиксела под точката (50, 70)?

.. mchoice:: PyGame__drawing_quiz_rect_up_left
   :answer_a: pg.draw.rect(canvas, color, (70, 120, 50, 60))
   :answer_b: pg.draw.rect(canvas, color, (100, 150, 110, 120))
   :answer_c: pg.draw.rect(canvas, color, (100, 150, 50, 60))
   :answer_d: pg.draw.rect(canvas, color, (70, 120, 80, 90))
   :answer_e: pg.draw.rect(canvas, color, (70, 180, 80, 90))
   :correct: d
   :feedback_a: Try again.
   :feedback_b: Try again.
   :feedback_c: Try again.
   :feedback_d: Correct!
   :feedback_e: Try again.

   Правоъгълникът е нарисуван с помощта на ``pg.draw.rect(canvas, color, (100, 150, 80, 90))``. Как човек може да нарисува правоъгълник със същия размер, разположен на 30 пиксела вляво и 30 пиксела над този правоъгълник?
   
.. mchoice:: PyGame__drawing_quiz_circle_above
   :answer_a: pg.draw.circle(canvas, color, (100, 120), 40)
   :answer_b: pg.draw.circle(canvas, color, (100, 160), 40)
   :answer_c: pg.draw.circle(canvas, color, (120, 100), 40)
   :answer_d: pg.draw.circle(canvas, color, (160, 100), 40)
   :answer_e: pg.draw.circle(canvas, color, (20, 120), 40)
   :correct: a
   :feedback_a: Correct!
   :feedback_b: Try again.
   :feedback_c: Try again.
   :feedback_d: Try again.
   :feedback_e: Try again.

   Правоъгълникът е нарисуван с помощта на ``pg.draw.circle(canvas, color, (100, 200), 40)``. Как човек може да нарисува кръг със същия размер над този кръг и да го докосне?


Промени, за да направи рисунката лесно подвижна
''''''''''''''''''''''''''''''''''''''''''''''''

Нека да видим как се очертава облак в следния пример:

.. activecode:: PyGame__drawing_cloud_fixed
    :nocodelens:
    :enablecopy:
    :modaloutput:
    :includesrc: src\PyGame\1_Drawing\5_Movable\cloud_fixed.py

Представихме облака с три кръга, един по-голям в средата и два по-малки около него:

.. code::

    pg.draw.circle(canvas, pg.Color("white"), (200, 200), 50)
    pg.draw.circle(canvas, pg.Color("white"), (150, 200), 30)
    pg.draw.circle(canvas, pg.Color("white"), (250, 200), 30)

Ако искахме да нарисуваме този облак на различна височина, бихме могли да повторим тези три команди, всеки път с някаква нова стойност за :math:`y` координата на центровете на тези три кръга вместо 200, както е на първата рисунка. Например:

.. code::

    pg.draw.circle(canvas, pg.Color("white"), (200, 200), 50)
    pg.draw.circle(canvas, pg.Color("white"), (150, 200), 30)
    pg.draw.circle(canvas, pg.Color("white"), (250, 200), 30)

    pg.draw.circle(canvas, pg.Color("white"), (200, 80), 50)
    pg.draw.circle(canvas, pg.Color("white"), (150, 80), 30)
    pg.draw.circle(canvas, pg.Color("white"), (250, 80), 30)
    
    pg.draw.circle(canvas, pg.Color("white"), (200, 320), 50)
    pg.draw.circle(canvas, pg.Color("white"), (150, 320), 30)
    pg.draw.circle(canvas, pg.Color("white"), (250, 320), 30)

.. image:: ../../_images/PyGame/clouds.png
    :width: 400px
    :align: center

По този начин програмата не само се разраства по-бързо, отколкото трябва, но също така трябва да правим всяка промяна на три места (например, ако искаме да опитаме 330 вместо 320, тази промяна трябва да се извърши на три места). Три промени не са много, но ако приемем този начин на правене на нещата, бихме имали все повече проблеми в по-сложни чертежи или в сложни програми като цяло.

Вместо това е по-добре да създадете функция и да прекарате :math:`y` координата на центровете като параметър:

.. code::

    def cloud(yc):
        pg.draw.circle(canvas, pg.Color("white"), (200, yc), 50)
        pg.draw.circle(canvas, pg.Color("white"), (150, yc), 30)
        pg.draw.circle(canvas, pg.Color("white"), (250, yc), 30)

    cloud(200)
    cloud(80)
    cloud(320)

Новата програма се чете и променя по-лесно. За повече облаци или по-сложни облаци предимството на този подход би било още по-голямо.

~~~~

Сега нека помислим как трябва да преместим облака вляво или вдясно. Трябва да увеличим или намалим :math:`x` координатите на всички кръгове (200, 150, 250) с една и съща стойност. Например, ако напишем 260, 210, 310 като :math:`x` координати, целият облак ще бъде преместен с 60 пиксела вдясно.

Би било добре, ако успеем да използваме само едно число, за да определим хоризонталното положение на облака. За да постигнем това, отбелязваме, че центровете на по-малките кръгове са на 50 пиксела от центъра на средния кръг вляво и вдясно. Тези разстояния не се променят с движението на облака. Това означава, че ако обозначим :math:`x` координата на центъра на средния кръг с :math:`X_c`, тогава центровете на по-малките кръгове имат :math:`x` координати :math:`X_c - 50 `и :math:`X_c + 50`. Благодарение на това отношение (което не зависи от позицията на облака), сега можем също да въведем параметъра :math:`x` към функцията, която рисува облака:

.. code::

    def cloud(xc, yc):
        pg.draw.circle(canvas, pg.Color("white"), (xc, yc), 50)
        pg.draw.circle(canvas, pg.Color("white"), (xc - 50, yc), 30)
        pg.draw.circle(canvas, pg.Color("white"), (xc + 50, yc), 30)
        
    cloud(200, 200)
    cloud(200, 80)
    cloud(200, 320)

Всеки от тези три облака вече може лесно да бъде преместен, например, 60 пиксела вдясно, като напишете 260 като първи параметър вместо 200 във функциите. Също толкова лесно е да направите рисунка с няколко облака. Цвят или нюанс на сивото също могат да бъдат функционален параметър. По този начин някои облаци могат да бъдат по-тъмни, а някои по-светли.

Когато използваме всичко по-горе, можем да създадем програма, която рисува няколко облака от различни нюанси, например:

.. activecode:: PyGame__drawing_cloud_movable
    :nocodelens:
    :enablecopy:
    :modaloutput:
    :includesrc: src\PyGame\1_Drawing\5_Movable\clouds_movable.py

Нека обобщим с малки обобщения какво трябва да се направи, за да можем да показваме една рисунка на различни места:

- Трябва да изберем една точка, чиито координати са зададени директно. Наричаме тази избрана точка **главна точка**, (понякога тази точка се нарича и **котва**). В примера на облаците основната точка е центърът на средния кръг.
- След като изберете основната точка, координатите на всички други значими точки се определят спрямо нея чрез добавяне или изваждане на определено изместване към координатите на основната точка. В примера с облака, за да получите: math: `x` координата на центъра на левия кръг, от: math:` x` координата на основната точка (центъра на средния кръг), изваждаме 50 пиксела и за десния кръг добавяме 50 пиксела.

В общия случай на чертежа може да има форми, различни от кръгове. Значителните точки, които определят позициите на тези форми са:

- за линия: нейните краища
- за многоъгълник: неговите точки
- за кръг: неговият център
- за правоъгълник: горния му ляв ъгъл
- за елипса: горният ляв ъгъл на правоъгълника, в който е вписан този елипс

Всички тези точки трябва да бъдат дадени по отношение на основната точка, тоест техните координати трябва да бъдат изразени като координати на основната точка, увеличени или намалени с някаква стойност.

Проверете разбирането си за предишните обяснения и отговорете на въпросите.

.. mchoice:: PyGame__drawing_quiz_anchor_introduction1 
   :answer_a: pg.draw.circle(canvas, pg.Color("red"), (x, y), 50, 1)
   :answer_b: pg.draw.circle(canvas, pg.Color("red"), (x+120, y+90), 50, 1)
   :answer_c: pg.draw.circle(canvas, pg.Color("red"), (x+20, y-10), 50, 1)
   :answer_d: pg.draw.circle(canvas, pg.Color("red"), (x-20, y+10), 50, 1)
   :correct: c
   :feedback_a: Try again.
   :feedback_b: Try again.
   :feedback_c: Correct!
   :feedback_d: Try again.

   Искаме да персонализираме чертеж, състоящ се от няколко фигури, така че всичко да е нарисувано спрямо котвата с координатите `x=100`, `y=100`. Едно от твърденията, които формират рисунка, е    

   .. activecode:: PyGame__drawing_quiz_anchor_introduction_code1
      :passivecode: true
                    
      pg.draw.circle(canvas, pg.Color("red"), (120, 90), 50, 1)

   Какво изявление трябва да замени даденото?
      
.. mchoice:: PyGame__drawing_quiz_anchor_introduction2
   :answer_a: pg.draw.line(canvas, pg.Color("red"), (x-50, y-50), (150, 150))
   :answer_b: pg.draw.line(canvas, pg.Color("red"), (x-50, y-50), (x+50, y+50))
   :answer_c: pg.draw.line(canvas, pg.Color("red"), (x-50, x+50), (y-50, y+50))
   :answer_d: pg.draw.line(canvas, pg.Color("red"), (x+50, y+50), (x+150, y+150))
   :correct: b
   :feedback_a: Try again.
   :feedback_b: Correct!
   :feedback_c: Try again.
   :feedback_d: Try again.

   Искаме да персонализираме чертеж, състоящ се от няколко фигури, така че всичко да е нарисувано спрямо котвата с координатите `x=100`, `y= 100`. Едно от твърденията, които формират рисунка, е

                
   .. activecode:: PyGame__drawing_quiz_anchor_introduction_code2
      :passivecode: true
                    
      pg.draw.line(canvas, pg.Color("red"), (50, 50), (150, 150))

   Какво изявление трябва да замени даденото?
      
.. mchoice:: PyGame__drawing_quiz_anchor_introduction3
   :answer_a: pg.draw.rect(canvas, pg.Color("red"), (x-50, y-50, x, y))
   :answer_b: pg.draw.rect(canvas, pg.Color("red"), (x, y, 100, 100))
   :answer_c: pg.draw.rect(canvas, pg.Color("red"), (x+50, y+50, 100, 100))
   :answer_d: pg.draw.rect(canvas, pg.Color("red"), (x-50, y-50, 100, 100))
   :correct: d
   :feedback_a: Try again.
   :feedback_b: Try again.
   :feedback_c: Try again.
   :feedback_d: Correct!

   Искаме да персонализираме чертеж, състоящ се от няколко фигури, така че всичко да е нарисувано спрямо котвата с координатите `x=100`, `y= 100`. Едно от твърденията, които формират рисунка, е
                
   .. activecode:: PyGame__drawing_quiz_anchor_introduction_code3
      :passivecode: true
                    
      pg.draw.rect(canvas, pg.Color("red"), (50, 50, 100, 100))

   What statement should replace the given one?
      
.. mchoice:: PyGame__drawing_quiz_move_to_the_right
   :multiple_answers:
   :answer_a: Вместо pg.draw.circle(canvas, color, (x, y), r, d) ползваме pg.draw.circle(canvas, color, (x+100, y), r, d).
   :answer_b: Вместо pg.draw.circle(canvas, color, (x, y), r, d) ползваме pg.draw.circle(canvas, color, (x-100, y-100), r, d).
   :answer_c: Вместо pg.draw.rect(canvas, color, (x, y, w, h), d) ползваме pg.draw.circle(canvas, color, (x+100, y, w+100, h), d).
   :answer_d: Вместо pg.draw.rect(canvas, color, (x, y, w, h), d) ползваме pg.draw.rect(canvas, color, (x+100, y, w, h), d).
   :answer_e: Вместо pg.draw.rect(canvas, color, (x, y, w, h), d) ползваме pg.draw.rect(canvas, color, (x-100, y, w, h), d).
   :correct: a, d
   :feedback_a: Correct!
   :feedback_b: Try again.
   :feedback_c: Try again.
   :feedback_d: Correct!
   :feedback_e: Try again.

   Искаме да преместим чертеж, състоящ се от няколко форми вдясно със 100 пиксела. Маркирайте правилните твърдения. 

Следват няколко примера за преобразуване на фиксиран чертеж в подвижен.

Мече - позиция
'''''''''''''''''''''

Посочена е следната програма, която показва главата на играчката на мечката:

.. activecode:: PyGame__drawing_bear_fixed
    :nocodelens:
    :enablecopy:
    :modaloutput:
    :includesrc: src\PyGame\1_Drawing\5_Movable\teddy-bear_fixed.py





Програмата извиква седем пъти функцията *framed_circle*, която рисува дадения кръг с черна рамка (макар че можеше да бъде избегната за трите малки черни кръга). За да можем да променим позицията на чертежа, нека да изберем основната точка (котва). Направете го в центъра на голям кръг, тоест главите на мечката. Координатите на тази точка са (250, 150). Сега трябва да изразим координатите на центровете на всички останали кръгове спрямо основната точка. Вземете за пример дясното ухо на мечката.

:math:`x` координата на центъра на дясното ухо е :math:`310 = 250 + 60`, докато :math:`y` координатата е :math:`80 = 150 - 70`. От тук можем да видим, че координатите на центъра на дясното ухо могат да бъдат записани в програмата като `(cx + 60, cy - 70)`, където `(cx, cy)` са координатите на главната точка.

Следвайте същата процедура за останалите кръгове и изпълнете функцията *draw_teddy*.

.. activecode:: PyGame__drawing_bear_movable1
    :nocodelens:
    :enablecopy:
    :modaloutput:
    :playtask:
    :includexsrc: src\PyGame\1_Drawing\5_Movable\teddy-bear_movable1b.py

   
    canvas.fill(pg.Color("white")) # paint background
    
    def framed_circle(canvas, color, center, radius):
        pg.draw.circle(canvas, color, center, radius)
        pg.draw.circle(canvas, pg.Color("black"), center, radius, 1)

    def draw_teddy(cx, cy):
        framed_circle(canvas, pg.Color("yellow"), (cx - 60,  cy - 70),  45) # left ear
        # complete the program
        
    draw_teddy(width // 2, height // 2)

    
Тази програма ни позволява лесно да показваме плюшени мечета на различни места на екрана. Например, извикването на функция

.. code::

    draw_teddy(width // 2, height // 2)
    
който рисува мечка с основната точка в центъра на прозореца (както беше), може да бъде заменен със следните две:

.. code::

    draw_teddy(width // 2 - 120, height // 2)
    draw_teddy(width // 2 + 120, height // 2)

Опитайте това! Би било много по-трудно да нарисуваме друга мечка, ако не бяхме адаптирали първоначалната програма за тази употреба.

Къща - позиция
''''''''''''''''

Да речем, че сте написали тази програма и целта ви е да преработите програмата, така че къщата да бъде лесно преместена:

.. activecode:: PyGame__drawing_house_detailed_fixed
    :nocodelens:
    :enablecopy:
    :modaloutput:
    :includesrc: src\PyGame\1_Drawing\5_Movable\house2D_detailed_fixed.py

Нека основната точка е: code: `(x, y) = (50, 150)`. Попълнете започнатото ремоделиране на програмата в полето по-долу, където чертежът се извършва във функцията: code: `draw_house(x, y, wall_color)'. След като се уверите, че чертежите в двете програми изглеждат еднакво (с изключение на това, че те рисуват в прозорци с различни размери), заменете code:`draw_house(50, 150, pg.Color (" khaki "))` със следващ 4, за да получите снимката както при натискане на бутона „Play Task“:

.. code::

    draw_house(150,  90, pg.Color(220, 220, 220))
    draw_house(220, 130, pg.Color("white"))
    draw_house(350, 160, (255,255,150))
    draw_house( 50, 150, pg.Color("khaki"))

.. activecode:: PyGame__drawing_house_detailed_movable
    :nocodelens:
    :enablecopy:
    :modaloutput:
    :playtask: 
    :includexsrc: src\PyGame\1_Drawing\5_Movable\house2D_detailed_movable.py
   
    canvas.fill(pg.Color("darkgreen")) # paint background

    def draw_house(x, y, wall_color):
        pg.draw.polygon(canvas, pg.Color("red"), [(x, y), (x+???, y-???), (x+140, y)]) # roof
        pg.draw.rect(canvas, wall_color,       (x,       y,     140, 100)) # walls
        pg.draw.rect(canvas, pg.Color("brown"), (x + ???, y + ???,  30,  30)) # left window
        pg.draw.rect(canvas, pg.Color("brown"), (x + ???, y + ???, ???, ???)) # right window
        pg.draw.rect(canvas, pg.Color("brown"), (x + ???, y + ???, ???, ???)) # door
        
    draw_house( 50, 150, pg.Color("khaki"))




.. commented out

    The task is non-active (commented out) until a related technical issue is resolved.

    Task - a constantly moving drawing
    ''''''''''''''''''''''''''''''''''

    The following function draws some drawing.
       
    .. activecode:: PyGame__drawing_movable_scalable_given
        :passivecode: true

        def draw():
            prozor.fill(pg.Color("white"))
            pg.draw.circle(canvas, pg.Color("blue"), (100, 100), 60)
            pg.draw.circle(canvas, pg.Color("yellow"), (75, 75), 15)
            pg.draw.circle(canvas, pg.Color("black"), (80, 80), 5)
            pg.draw.circle(canvas, pg.Color("yellow"), (125, 75), 15)
            pg.draw.circle(canvas, pg.Color("black"), (120, 80), 5)
            pg.draw.ellipse(canvas, pg.Color("red"), (75, 110, 50, 10))

    In the program that follows, the drawing function is just started. Complete it by drawing the same drawing, but using the anchor :math:`(x, y)`, which is located in the center of the blue circle (initially this is the point :math:`(100, 100)`).

    When you finish the function, make sure it works the same as when you click the "Play task" button.

    .. activecode:: PyGame__drawing_movable
       :nocodelens:
       :enablecopy:
       :modaloutput:
       :playtask:
       :includexsrc: src\PyGame\1_Drawing\5_Movable\movable_scalable.py
       
                     
       def draw():
           canvas.fill(pg.Color("white"))

.. commented out

    .. reveal:: PyGame__drawing_movable_reveal
       :showtitle: Show solution
       :hidetitle: Hide solution

       .. activecode:: PyGame_movable_code
          :passivecode:

          def draw():
              canvas.fill(pg.Color("white"))
              pg.draw.circle(canvas, pg.Color("blue"), (x, y), 60)
              pg.draw.circle(canvas, pg.Color("yellow"), (x-25, y-25), 15)
              pg.draw.circle(canvas, pg.Color("black"), (x-20, y-20), 5)
              pg.draw.circle(canvas, pg.Color("yellow"), (x+25, y-25), 15)
              pg.draw.circle(canvas, pg.Color("black"), (x+20, y-20), 5)
              pg.draw.ellipse(canvas, pg.Color("red"), (x-25, y+10, 50, 10))
           

