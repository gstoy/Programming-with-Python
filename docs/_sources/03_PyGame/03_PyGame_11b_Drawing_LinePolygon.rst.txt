Рисуване на прави линии и многоъгълници
----------------------------------------

Функциите за чертане на прави линии и многоъгълници са подобни на функциите за рисуване на правоъгълници, елипси и кръгове, които вече сме научили. Тук се използват и параметрите *canvas*, *color* и *thickness*, със същото значение като преди. Ще обясним новите параметри, докато ги срещнем.

Тук ще повторим "празната" програма, която се справя само с библиотеката PyGame и прозореца за рисуване (и не чертае нищо от себе си), в случай че искате да опитате нещо бързо.

.. activecode:: pygame__drawing_primirives_def_copy
    :nocodelens:
    :modaloutput: 
    :enablecopy:

    # -*- acsection: general-init -*-
    import pygame as pg, pygamebg
    canvas = pygamebg.open_window(200, 200, "Pygame")
    canvas.fill(pg.Color("gray"))
    # -*- acsection: main -*-



    # -*- acsection: after-main -*-
    pygamebg.wait_loop()
 

Рисуване на лния
''''''''''''''''

За да нарисуваме линия използваме функцията ``pg.draw.line``, със или без параметъра за дебелина. 

.. code::

    pg.draw.line(canvas, color, point1, point2, thickness)
    pg.draw.line(canvas, color, point1, point2)


- Параметрите *point1*, *point2* са точки на екрана, които представляват крайните точки на линейния сегмент. Отново се посочва точка като кортеж или списък от 2 елемента. Елементите на този кортеж или списък са координатите на точката в прозореца, в който рисуваме.
- При тази функция пропускането на дебелината има различно значение, отколкото при другите функции, което е да се използва дебелината на линията по подразбиране от 1 пиксел.

Например командата::

.. activecode:: pygame__drawing_line_def
    :passivecode: true

    pg.draw.line(canvas, pg.Color("blue"), (20, 10), (40, 30), 2)
    
ще нарисува синя линия с широчина 2 пиксела от точка :math:`(20, 10)` до точка :math:`(40, 30)`.

.. image:: ../../_images/PyGame/drawing_line.png
   :width: 200px   
   :align: center 

Рисуване на многоъгълник 
''''''''''''''''''''''''

За да нарисуваме многоъгълник използваме командата ``pg.draw.polygon``, която също има две форми:

.. code::

    pg.draw.polygon(canvas, color, point_list, thickness)
    pg.draw.polygon(canvas, color, point_list)

- Параметърът *point_list* представлява списък от върхове на многоъгълника, който рисуваме. Например [(50, 250), (150, 150), (250, 250)] е списък от 3 точки.
- Тук отново използваме формата без параметъра *дебелина*, когато искаме полигонът да бъде запълнен с посочения цвят (ако посочим ширина, ще се очертае многоъгълна линия с тази ширина).

Например следното изявление рисува триъгълник, оцветен с :math:`(0, 100, 36)` color. Върховете на триъгълника са :math:`(50, 100)`, :math:`(150, 150)` и :math:`(150, 50)`.

.. activecode:: pygame__drawing_polygon_def
    :passivecode: true

    pg.draw.polygon(canvas, (0, 100, 36), [(50, 100), (150, 150), (150, 50)])

.. image:: ../../_images/PyGame/drawing_polygon.png
   :width: 200px   
   :align: center 

В допълнение към изброените и описани функции има и други функции за рисуване в модула ``pg.draw``, но тук няма да се занимаваме с тях. Ако се интересувате да научите повече за тези функции, можете да намерите допълнителна, например на `<https://www.pygame.org/docs/ref/draw.html>` __

Функции за рисуване - въпроси
'''''''''''''''''''''''''''''

Проверете знанията си за функциите за рисуване:

.. parsonsprob:: pygame__drawing_quiz_arg_order

   В какъв ред са дадени следните аргументи във функцията `pg.draw.line`
   -----
   
   canvas
   color
   first point coordinates
   second point coordinates
   thickness

.. mchoice:: pygame__drawing_quiz_polygon_args1
   :answer_a: pg.draw.polygon(canvas, color, [(0, 0), (50, 100), (100, 0)])
   :answer_b: pg.draw.polygon(canvas, color, (0, 0), (50, 100), (100, 0))
   :answer_c: pg.draw.polygon(canvas, color, (0, 0, 50, 100, 100, 0))
   :answer_d: pg.draw.polygon(canvas, color, [0, 0, 50, 100, 100, 0])
   :correct: a
   :feedback_a: Вярно
   :feedback_b: Опитай пак
   :feedback_c: Опитай пак
   :feedback_d: Опитай пак

   Искаме да нарисуваме триъгълник. В каква форма могат да се посочват координатите на точките?

.. mchoice:: pygame__drawing_quiz_polygon_args2
   :multiple_answers:
   :answer_a: pg.draw.polygon(canvas, color, [(0, 0), (50, 100), (100, 0)], 7)
   :answer_b: pg.draw.polygon(canvas, color, [(0, 0), (0, 50), (50, 50), (50,  0)])
   :answer_c: pg.draw.polygon(canvas, color, [(0, 0), (50, 100), (100, 0)])
   :answer_d: pg.draw.polygon(canvas, color, [(0, 0), (0, 50), (50, 50), (50,  0)], 4)
   :correct: b, c
   :feedback_a: Вярно
   :feedback_b: Опитай пак
   :feedback_c: Опитай пак
   :feedback_d: Вярно

   Кой от следните полигони не може да бъде изготвен с множество повиквания на функцията ``pg.draw.line`` ?
   
.. dragndrop:: pygame__drawing_quiz_function_names
    :feedback: Опитай пак!
    :match_1: Line segment|||pg.draw.line
    :match_2: Polygon|||pg.draw.polygon
    :match_3: Rectangle|||pg.draw.rect
    :match_4: Circle|||pg.draw.circle

    Съберете изявленията за рисуване и формите, които рисуват.
    
.. parsonsprob:: pygame__drawing_quiz_general_arg_order

   Сортиране според типичния ред на аргументите във функциите за рисуване:
   -----
   canvas
   color
   coordinates
   thickness

   
.. mchoice:: pygame__drawing_quiz_point_list
   :answer_a: Кръг
   :answer_b: Елипса
   :answer_c: Полигон
   :answer_d: Линеен сегмент
   :answer_e: Квадрат
   :correct: c
   :feedback_a: Опитай пак
   :feedback_b: Опитай пак
   :feedback_c: Вярно
   :feedback_d: Опитай пак
   :feedback_e: Опитай пак

   Когато рисувате коя от следните форми са координатите, дадени под формата на списък на подредени двойки?


Рисуване според инструкциите
'''''''''''''''''''''''''''''

.. questionnote::

    **Плашило:** Начертайте плашило на бял фон. Състои се от следните части:
    
    - глава: черен кръг, широк 6 пиксела, центриран в точка (150, 70), с радиус 50
    - тяло: права черна линия, широка 6 пиксела, от точка (150, 120) до точка (150, 300)
    - ръце: права черна линия, широка 6 пиксела, от точка (80, 170) до точка (220, 170)
    - ляв крак: права черна линия, широка 6 пиксела, от точка (150, 300) до точка (90, 480)
    - десен крак: права черна линия, широка 6 пиксела, от точка (150, 300) до точка (210, 480)

.. activecode:: pygame__drawing_scarecrow
   :nocodelens:
   :enablecopy:
   :modaloutput:
   :playtask:
   :includexsrc: src/PyGame/1_Drawing/1_BasicExamples/scarecrow.py
   
.. questionnote::

    **Дърво:** Начертайте дърво на бял фон. Състои се от следните части:

    - дънер: правоъгълник, изпълнен с цвят (97, 26, 9), размер 40 x 50, с горен ляв връх в точка (130, 250) 
    - горна част на върха на дървот: триъгълник, изпълнен с цвят (0, 100, 36), с върхове (50, 250), (150, 150) и (250, 250) 
    - средна част на дървото: триъгълник, изпълнен с цвят (0, 100, 36), с върхове (75, 200), (150, 100) и (225, 200) 
    - долната част на дървото триъгълник, изпълнен с цвят (0, 100, 36), с върхове (100, 150), (150, 50) и (200, 150)
    
.. activecode:: pygame__drawing_tree
   :nocodelens:
   :enablecopy:
   :modaloutput:
   :playtask:
   :includexsrc: src/PyGame/1_Drawing/1_BasicExamples/tree.py


Рисунки изненада
'''''''''''''''''

За да видите чертежа в следващите задачи, трябва да напишете правилните кодове и да стартирате програмата си.

.. questionnote::

     **Изненада 1-свържете точките:** Дадени са върховете на многоъгълник. Начертайте полигона, изпълнен с цвят "каки" на "тъмнозелен" фон.

.. activecode:: pygame__drawing_giraffe
   :nocodelens:
   :enablecopy:
   :modaloutput:
   :includexsrc: src/PyGame/1_Drawing/2_ByInstructions/giraffe.py

.. questionnote::

    **Изненада 2:** - Използвайки цвят "лимонов цвят" И нарисувайте::
    
    - Запълнена елипса, вписана в правоъгълник, чиято горна лява върха е на (75, 100), ширината й е 150, а височината му е 180; 
    - Линия с ширина 6, от точка (130, 110) до точка (120, 20);
    - Друга линия с ширина 6, от точка (170, 110) до точка (180, 20);
    - Запълнен кръг с радиус 10 пиксела, центриран в точка (120, 20);
    - Запълнен кръг с радиус 10 пиксела, центриран в точка (180, 20);
    
     С черен цвят нарисувайте още две запълнени елипси:

    - една, вписана в правоъгълник, чийто горен ляв връх е в точка (110, 140), ширината му е 30, а височината му е 50;
    - и една, вписана в правоъгълник, чийто горен ляв връх е в точка (160, 140), ширината му е 30, а височината му е 50;


.. activecode:: pygame__drawing_ant
   :nocodelens:
   :enablecopy:
   :modaloutput:
   :includexsrc: src/PyGame/1_Drawing/2_ByInstructions/insect.py
   
