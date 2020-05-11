Рисуване с помощта на цикли
------------------------------

Помислете за следната задача: нека нарисуваме 6 кръга, както е на тази снимка:

.. image:: ../../_images/PyGame/target.png
   :width: 300px
   :align: center 

Разглеждайки снимката, можем да предположим (или би могло да се каже в проблемната настройка), че кръговете са еднакво разположени. Това означава, че разликата в радиуса на всеки два съседни кръга е една и съща.

Избираме размера на кръговете да е възможно най-голям, но да се побере в дадено чертожно пространство от 300x300 пиксела. Тъй като ширината на прозореца е 300 пиксела, радиусът на най-големия кръг е 150. За разликата на радиусите на двете съседни кръгове можем да вземем :math:`{150 \ over 6} = 25`. Това дава радиуси от 25, 50, 75, 100, 125, 150.

Въз основа на изчислените стойности можем да напишем програма като тази:

.. activecode:: PyGame_loop__target_fixed
   :nocodelens:
   :enablecopy:
   :modaloutput:
   :includesrc: src\PyGame\1_Drawing\7a_UsingLoops\Examples\circles_target_fixed.py

Нека си представим, че след това ни беше дадена новата задача да направим същата рисунка, но с 5 кръга. Това е много малка промяна, нали? Трябва да можем да използваме повторно решената по-рано задача.

Когато започнем да работим върху рисунка с 5 кръга, виждаме, че може да се използва много малко от предишната програма. Всъщност можем да използваме само идеята и размерът на кръговете трябва да се изчислява от нулата.

Ако бяхме написали програмата по различен начин, персонализирането й щеше да бъде много по-лесно. Можем например да запишем броя на кръговете в променлива и след това да използваме тази променлива при всички необходими изчисления. Тази програма ще изглежда така:

.. activecode:: PyGame_loop__target_flexible
   :nocodelens:
   :enablecopy:
   :modaloutput:
   :includesrc: src\PyGame\1_Drawing\7a_UsingLoops\Examples\circles_target_flexible.py

В тази програма е достатъчно да промените само едно число, така че да нарисува произволен брой кръгове.

Както казахме по-рано, много рисунки имат някаква закономерност, като симетрия или някаква повтаряща се част (и много други, по-сложни модели). Ако разберем закономерността на такива рисунки и я изразим математически, ще можем да я използваме, когато пишем програма за изготвяне на такива рисунки, както направихме в предишния пример. По този начин получаваме програма, която е много по-лесно да се модифицира, за да се получи друга, подобна рисунка. За рисунки с голям брой повторения на част (идентични или леко модифицирани) програмата, която използва редовност, също ще бъде много по-къса.

.. infonote::

    Много програми, използвани от милиони хора, непрекъснато се усъвършенстват и усъвършенстват и се публикуват нови версии на такива програми. Следователно промените в програмата са нещо напълно нормално, което се случва непрекъснато. Подобна е ситуацията и с програмите, които сами пишем. Когато пишем програма, лесно може да се случи, че по-късно мислим за нещо ново и искаме да модифицираме част от програмата, която вече е написана.

    Ето защо, когато пишем програми, трябва да имаме предвид, че някой (вероятно сами) ще иска да създаде подобна програма и може да иска да използва програмата ни като първоначална версия.

Нека да разгледаме друг пример как можем да използваме закономерностите в чертежа, за да напишем по-гъвкава програма (програма, която е по-лесна за адаптиране към малко по-различна цел).

Пример - антена
'''''''''''''''''

Вече видяхме програма, която рисува тази антена. Сега програмата е написана така, че да не е твърде трудно да промените броя на напречните сегменти, разстоянието между тях, разликата в дължините на последователни сегменти и други подобни.

.. activecode:: PyGame_loop__antenna
   :nocodelens:
   :enablecopy:
   :modaloutput:
   :includesrc: src\PyGame\1_Drawing\7a_UsingLoops\Examples\antenna1.py

Част от програмата, която рисува напречните сегменти на антената, може да бъде написана, както следва:

.. code::

    for i in range(6):
        pg.draw.line(canvas, pg.Color('darkgray'), (120 - 10 * i,  75 + 25 * i), (180 +  10 * i,  75 + 25 * i), 1 + i//2)

Програмата, написана по този начин, би била малко по-къса, но първата е по-ясна, така че всяка има своите предимства. Нека само да отбележим, че и двете програми са по-добри, отколкото да рисуваме по 6 линии един по един за напречни сегменти (ние преди това). Ако тази част от програмата се състоеше от шест обаждания към функцията за изтегляне на линия, би било по-трудно да се модифицира и коригира програмата, за да се очертае различна антена.

Равнопоставени числа
'''''''''''''''''''''

И в двата предишни примера беше необходимо да се изброят една или повече серии от еднакви разстояния. В задачата с кръгове това бяха числа 25, 50, 75, 100, 125, 150 (радиуси на кръгове), а в задачата с антената ни бяха нужни колкото четири серии от числа - *x* и *y* координати на краищата на напречните сегменти на антената. По-специално, тези числа са:

- *x* coordinates of left ends: 120, 110, 100, 90, 80, 70
- *y* coordinates of left ends: 75, 100, 125, 150, 175, 200
- *x* coordinates of right ends: 180, 190, 200, 210, 220, 230
- *y* coordinates of right ends: 75, 100, 125, 150, 175, 200

Видяхме, че има различни начини да получим ценностите, от които се нуждаем. Например в задача с концентрични кръгове, стойности 25, 50, 75, 100, 125, 150, бихме могли да получим по някой от следните (еднакво добри) начини:

..  code::

    for r in range(25, 151, 25):
        pg.draw.circle(canvas, pg.Color("red"), center, r, 2)

..  code::

    for i in range(br_krugova):
        pg.draw.circle(canvas, pg.Color("red"), center, round(25 + i * 25), 2)

..  code::

    r = 25
    for _ in range(br_krugova):
        pg.draw.circle(canvas, pg.Color("red"), center, r, 2)
        r += 25

В общия случай, ако трябва да получим поредица от стойности на *a*, *a+d*, *a+2d*, ... *a+(n-1)d*, предишните три метода могат да бъдат използва се както следва:

..  code::

    for x in range(a, a + n*d, d):
        print(x)

..  code::

    for i in range(n):
        print(a+i*d)

..  code::

    x = a
    for _ in range(n):
        print(x)
        x += d

Ще видим, че много задачи с рисуване на еднакви дистанционни форми могат да бъдат решени чрез прилагане на контури като тази.

Обърнете внимание, че функцията ``range`` със стъпка (с три аргумента) трябва да получава цели аргументи, така че в ситуации, в които стъпката не е цяло число, нейното използване не е възможно.

Когато имаме нужда (както при задаване на антена) да направим няколко серии в един цикъл, първият режим е по-малко удобен, така че трябва да изберем един от другите два начина.

Следващите въпроси ще ви помогнат да затвърдите знанията си за формиране на серия от еднакви разстояния от числа.

.. dragndrop:: pygame__loop_quiz_match_series
    :feedback: try again!
    :match_1: 100, 200, 300, 400, 500|||for i in range(100, 600, 100)
    :match_2: 100, 300, 500|||for i in range(100, 601, 200)
    :match_3: 100, 200, 300, 400, 500, 600|||for i in range(100, 601, 100)
    :match_4: 200, 300, 400, 500, 600|||for i in range(200, 601, 100)

    Съберете серия от числа с цикъла, който ги е генерирал.
     
.. dragndrop:: pygame__loop_quiz_match_series2
    :feedback: try again!
    :match_1: 100, 150, 200, 250, 300|||x = 100 + i*50
    :match_2: 50, 150, 250, 350, 450|||x = 50 + i*100
    :match_3: 0, 100, 200, 300, 400|||x = i*100
    :match_4: 100, 200, 300, 400, 500|||x = 100+i*100

    Съпоставете получените числа с израза "for i in range (5):" с цикъла, който ги генерира.
    

.. mchoice:: pygame__loop_quiz_range01
    :answer_a: x = 25 * i + 50
    :answer_b: x = (25 + i) * 50
    :answer_c: x = 25 * 2*i+1
    :answer_d: x = 25 + 50 * i
    :correct: d
    :feedback_a: No.
    :feedback_b: No.
    :feedback_c: No.
    :feedback_d: Correct!
    
    Кое трябва да бъде използвано в цикъла.
    
    .. code::
    
        for i in range(19):
            x = ???
            ...
            
    за да има *x* същата стойност, както в цикъла

    .. code::
    
        for x in range(25, 500, 50):
            ...
            
Задачите за упражнение са следните.

Стълба
''''''

Променете програмата така, че стъпалата на стълбата да бъдат очертани в цикъл.

.. activecode:: PyGame_loop__ladder
    :nocodelens:
    :enablecopy:
    :modaloutput:
    :playtask:
    :includexsrc: src\PyGame\1_Drawing\7a_UsingLoops\Tasks\ladder.py

    canvas.fill(pg.Color("green")) # paint background

    pg.draw.line(canvas, pg.Color("brown"), (100, 10), (100, height - 10), 10)    # left side
    pg.draw.line(canvas, pg.Color("brown"), (200, 10), (200, height - 10), 10)    # right side

    # change (rewrite) this part
    pg.draw.line(canvas, pg.Color("brown"), (100,  50), (200, 50), 10) # step
    pg.draw.line(canvas, pg.Color("brown"), (100, 100), (200, 100), 10) # step
    pg.draw.line(canvas, pg.Color("brown"), (100, 150), (200, 150), 10) # step
    pg.draw.line(canvas, pg.Color("brown"), (100, 200), (200, 200), 10) # step
    pg.draw.line(canvas, pg.Color("brown"), (100, 250), (200, 250), 10) # step

   
.. reveal:: PyGame_loop__ladder_reveal
    :showtitle: Съвет
    :hidetitle: Скрий 

    Вместо 5 редови извода за рисуване, можете да използвате цикъл от следната форма: 
    
    .. code::
    
        for y in ???:
            pg.draw.line(canvas, pg.Color("brown"), (100, y), (200, y), 10)
            
    To complete the loop correctly, you need to answer the following question:
    
    .. mchoice:: pygame__loop_quiz_range1
        :answer_a: range(0, 50, 250)
        :answer_b: range(250, 50)
        :answer_c: range(50, 251, 50)
        :answer_d: range(50, 250, 50)
        :correct: c
        :feedback_a: No, the first number is not appropriate for that range.
        :feedback_b: No, try again.
        :feedback_c: Correct!
        :feedback_d: No, the last number is not appropriate for that range.
        
        Which of the ranges offered gives values 50, 100, 150, 200, 250?

          
Дървета
''''''''

Променете програмата така, че едно дърво да бъде нарисувано във всяко или трите преминавания през цикъла.

.. activecode:: PyGame_loop__trees
    :nocodelens:
    :enablecopy:
    :modaloutput:
    :playtask:
    :includexsrc: src\PyGame\1_Drawing\7a_UsingLoops\Tasks\trees.py
   
    canvas.fill(pg.Color("green")) # paint background

    pg.draw.rect(canvas, pg.Color("brown"), (40, 180, 20, 100))        # first tree
    pg.draw.ellipse(canvas, pg.Color("darkgreen"), (10, 50, 80, 150))  # first treetop
    pg.draw.rect(canvas, pg.Color("brown"), (140, 180, 20, 100))       # second tree
    pg.draw.ellipse(canvas, pg.Color("darkgreen"), (110, 50, 80, 150)) # second treetop
    pg.draw.rect(canvas, pg.Color("brown"), (240, 180, 20, 100))       # third tree
    pg.draw.ellipse(canvas, pg.Color("darkgreen"), (210, 50, 80, 150)) # third treetop

.. reveal:: PyGame_loop__trees_reveal
    :showtitle: Съвет
    :hidetitle: Скрий съвета

    Програмата би изглеждала така:
    
    .. activecode:: PyGame_loop__trees_solution
        :nocodelens:
        :enablecopy:
        :modaloutput:
        :includexsrc: src\PyGame\1_Drawing\7a_UsingLoops\Tasks\trees.py

        canvas.fill(pg.Color("green")) # paint background

        for i in range(3):
            pg.draw.rect(canvas, pg.Color("brown"), (???, 180, 20, 100))        # tree
            pg.draw.ellipse(canvas, pg.Color("darkgreen"), (???, 50, 80, 150))  # treetop

    
    при което вместо въпросните знаци трябва да се поставят подходящи изрази за координатата *x*. Когато *i* приема стойностите 0, 1, 2 в ред, изразът в първия израз трябва да приема стойностите 40, 140, 240, а изразът във втория израз трябва да приема стойностите 10, 110, 210.


Решетка
''''''''

Променете програмата така, че вертикалните линии да бъдат начертани в един цикъл, а хоризонталните линии във втория.

.. activecode:: PyGame_loop__grid
    :nocodelens:
    :enablecopy:
    :modaloutput:
    :playtask:
    :includexsrc: src\PyGame\1_Drawing\7a_UsingLoops\Tasks\grid.py
    
    pg.draw.line(canvas, pg.Color("black"), (10, 10), (10, height - 10), 1)
    pg.draw.line(canvas, pg.Color("black"), (30, 10), (30, height - 10), 1)
    pg.draw.line(canvas, pg.Color("black"), (50, 10), (50, height - 10), 1)
    pg.draw.line(canvas, pg.Color("black"), (70, 10), (70, height - 10), 1)
    pg.draw.line(canvas, pg.Color("black"), (90, 10), (90, height - 10), 1)
    pg.draw.line(canvas, pg.Color("black"), (110, 10), (110, height - 10), 1)
    pg.draw.line(canvas, pg.Color("black"), (130, 10), (130, height - 10), 1)
    pg.draw.line(canvas, pg.Color("black"), (150, 10), (150, height - 10), 1)
    pg.draw.line(canvas, pg.Color("black"), (170, 10), (170, height - 10), 1)
    pg.draw.line(canvas, pg.Color("black"), (190, 10), (190, height - 10), 1)
    pg.draw.line(canvas, pg.Color("black"), (210, 10), (210, height - 10), 1)
    pg.draw.line(canvas, pg.Color("black"), (230, 10), (230, height - 10), 1)
    pg.draw.line(canvas, pg.Color("black"), (250, 10), (250, height - 10), 1)
    pg.draw.line(canvas, pg.Color("black"), (270, 10), (270, height - 10), 1)
    pg.draw.line(canvas, pg.Color("black"), (290, 10), (290, height - 10), 1)
    pg.draw.line(canvas, pg.Color("black"), (310, 10), (310, height - 10), 1)
    pg.draw.line(canvas, pg.Color("black"), (330, 10), (330, height - 10), 1)
    pg.draw.line(canvas, pg.Color("black"), (350, 10), (350, height - 10), 1)
    pg.draw.line(canvas, pg.Color("black"), (370, 10), (370, height - 10), 1)
    pg.draw.line(canvas, pg.Color("black"), (390, 10), (390, height - 10), 1)
    pg.draw.line(canvas, pg.Color("black"), (410, 10), (410, height - 10), 1)
    pg.draw.line(canvas, pg.Color("black"), (430, 10), (430, height - 10), 1)
    pg.draw.line(canvas, pg.Color("black"), (450, 10), (450, height - 10), 1)
    pg.draw.line(canvas, pg.Color("black"), (470, 10), (470, height - 10), 1)
    pg.draw.line(canvas, pg.Color("black"), (490, 10), (490, height - 10), 1)
    
    pg.draw.line(canvas, pg.Color("black"), (10, 10), (width - 10, 10), 1)
    pg.draw.line(canvas, pg.Color("black"), (10, 30), (width - 10, 30), 1)
    pg.draw.line(canvas, pg.Color("black"), (10, 50), (width - 10, 50), 1)
    pg.draw.line(canvas, pg.Color("black"), (10, 70), (width - 10, 70), 1)
    pg.draw.line(canvas, pg.Color("black"), (10, 90), (width - 10, 90), 1)
    pg.draw.line(canvas, pg.Color("black"), (10, 110), (width - 10, 110), 1)
    pg.draw.line(canvas, pg.Color("black"), (10, 130), (width - 10, 130), 1)
    pg.draw.line(canvas, pg.Color("black"), (10, 150), (width - 10, 150), 1)
    pg.draw.line(canvas, pg.Color("black"), (10, 170), (width - 10, 170), 1)
    pg.draw.line(canvas, pg.Color("black"), (10, 190), (width - 10, 190), 1)
    pg.draw.line(canvas, pg.Color("black"), (10, 210), (width - 10, 210), 1)
    pg.draw.line(canvas, pg.Color("black"), (10, 230), (width - 10, 230), 1)
    pg.draw.line(canvas, pg.Color("black"), (10, 250), (width - 10, 250), 1)
    pg.draw.line(canvas, pg.Color("black"), (10, 270), (width - 10, 270), 1)
    pg.draw.line(canvas, pg.Color("black"), (10, 290), (width - 10, 290), 1)

