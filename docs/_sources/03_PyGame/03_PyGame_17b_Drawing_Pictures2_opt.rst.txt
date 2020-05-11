Показване на готови изображения - задачи
-----------------------------------------

Научихме се как да покажем готово изображение, така че горният му ляв ъгъл да е в дадена позиция на екрана. В някои ситуации позицията на горния ляв ъгъл на изображението няма да ни е известна, но ще трябва да се изчисли. В такива случаи може да е необходимо да се знае ширината и височината на изображението. В библиотеката PyGame на Python за изображението ``im`` ширината и височината на това изображение са дадени съответно като ``im.get_width()`` и ``im.get_height()``.

Кошници
'''''''

Изпълнете следната програма, за да получите снимката, както в примера. Позициите на дърветата са дадени и до всяко дърво трябва да се нарисува кошница, така че долните десни ъгли на изображенията на кошницата и дърветата да се припокриват.

За да изпълните тази задача, трябва да изчислите за всяка изтеглена кошница позицията на горния й ляв ъгъл, което може да се извърши, като се започне от координатите на горния ляв ъгъл на дървото, като се използват ширините и височините на двете изображения.

.. image:: ../../_images/tree.png
   :width: 50px

.. image:: ../../_images/apple_small.png
   :width: 50px

.. image:: ../../_images/basket.png
   :width: 50px

.. activecode:: PyGame__pictures_baskets1
    :nocodelens:
    :enablecopy:
    :modaloutput:
    :playtask:
    :includexsrc: src\PyGame\1_Drawing\9_UsingImages\trees_baskets.py

    tree_image = pg.image.load("tree.png")  # image of a tree
    basket_image = pg.image.load("basket.png")  # image of a basket
    tree_positions = ((200, 70), (120, 150), (240, 290), (550, 170), (400, 200))


Бране на ябълки
''''''''''''''''

Изпълнете следната програма, за да получите снимката, както в примера. Решението на тази задача се получава чрез добавяне на предишната програма - копирайте я и добавете ябълки към дърветата и към кошниците.

.. activecode:: PyGame__pictures_baskets_apples
    :nocodelens:
    :enablecopy:
    :modaloutput:
    :playtask:
    :includexsrc: src\PyGame\1_Drawing\9_UsingImages\trees_apples_baskets.py

    tree_image = pg.image.load("tree.png")  # image of a tree
    apple_image = pg.image.load("apple_small.png")  # image of an apple
    basket_image = pg.image.load("basket.png")  # image of a basket
    apples_on_tree_positions = ((43,191), (61, 158), (124, 145), (134, 175), (160, 180))
    apples_in_basket_positions = ((15, 38), (60, 41), (22, 43), (49, 45), (34, 48))
    tree_positions = ((200, 70), (120, 150), (240, 290), (550, 170), (400, 200))



Кутии
'''''

.. questionnote:: 

    Напишете програми, които използват изображението на кутията, показано по-долу,

    .. image:: ../../_images/PyGame/box.png
        :width: 200px
        :align: center 

    и формирайте изображения, както в примери (използвайте бутона „Play Task“ във всяка задача).
      
    Координатите на изображението, тоест горният му ляв ъгъл за най-лявото поле са (60, 400), а за най-високата кутия са (420, 115). 

От дадените данни и изображения е възможно да се определят сериите *x* и *y* на координатите на изображението на всяко поле във всеки пример. Редът за показване на снимките на кутиите също трябва да се вземе предвид тук.

За да разберете по-добре как една и съща серия от числа (например 10, 15, 20, 25, 30) могат да бъдат получени в два различни реда и какво още да търсите, отговорете на поддържащия въпрос.

.. dragndrop:: console__pictures_quiz_series_negative_step
    :feedback: Try again.
    :match_1: 10, 15, 20, 25, 30 ||| for x in range(10, 35, 5)
    :match_2: 30, 25, 20, 15, 10 ||| for x in range(30, 5, -5)
    :match_3: empty series ||| for x in range(30, 10, 5)
    :match_4: 5, 15, 25 ||| for x in range(5, 35, 10)

    Съпоставете сериите от числа с операторите, които ги генерират.

.. activecode:: PyGame__pictures_boxes1
    :nocodelens:
    :enablecopy:
    :modaloutput:
    :playtask:
    :includexsrc: src\PyGame\1_Drawing\9_UsingImages\boxes1.py

.. activecode:: PyGame__pictures_boxes2
    :nocodelens:
    :enablecopy:
    :modaloutput:
    :playtask:
    :includexsrc: src\PyGame\1_Drawing\9_UsingImages\boxes2.py

.. activecode:: PyGame__pictures_boxes3
    :nocodelens:
    :enablecopy:
    :modaloutput:
    :playtask:
    :includexsrc: src\PyGame\1_Drawing\9_UsingImages\boxes3.py

