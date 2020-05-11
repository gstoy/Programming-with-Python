Показване на готови изображения
--------------------------------

Рисуването на основни форми може да бъде забавно, а понякога и предизвикателство. И все пак би било още по-забавно да можем да комбинираме нашата рисунка с готови снимки или снимки. В PyGame среда това е много просто. Нека разгледаме следния пример: 

.. image:: ../../_images/tree.png
   :width: 50px

.. image:: ../../_images/apple_small.png
   :width: 50px

.. image:: ../../_images/basket.png
   :width: 50px


.. activecode:: PyGame__images_trees_and_apples1
   :nocodelens:
   :enablecopy:
   :modaloutput:
   :includesrc: src\PyGame\1_Drawing\9_UsingImages\trees_and_apples1.py

В тази програма имаме две нови функции на PyGame:

- Функция :code:`pg.image.load` зарежда изображението от диска. Предаваме името на файла, съдържащ изображението, на тази функция (пътят до файла може да бъде включен) и в резултат на това той връща изображението във формат, подходящ за програма. Трябва да запишем този резултат в някаква променлива (в примера това е променливата *tree_image*);

- Функция :code:`blit` показва изображение в даден прозорец. Аргументите на тази функция са променлива, съдържаща изображението (резултат от функция *pg.image.load*) и позиция :math:`(x, y)' в прозореца, където искаме изображението да се показва. В позицията, която сме задали, ще се появи горният ляв ъгъл на изображението. В примера задаваме позицията :math:`(0, 0)`, така че горният ляв ъгъл на изображението се появява в горния ляв ъгъл на прозореца.

Опитайте да въведете различни стойности на координатите вместо :math:`(0, 0)`, за да получите по-добро разбиране за това как работи *blit* функцията. Можем да наблюдаваме, че показването на готови изображения е подобно на показването на подвижни рисунки с помощта на котва.

Можете също да опитате да покажете едно изображение на множество места на екрана, както направихме с основните форми. Просто извикайте функцията *blit* няколко пъти с различни стойности за местоположението на дисплея.

Когато показвате изображение на няколко места, изображенията могат да се припокриват. Затова трябва да се внимава за реда на показване. В нашия случай първо трябва да покажем дървото, което си представяме като по-нататък, а след това дървото, което си представяме като по-близко. В противен случай финалната сцена може да изглежда погрешна, както показва следната снимка.

.. image:: ../../_images/PyGame/trees_and_apples_bad.png
   :width: 600px
   :align: center 
      
Обектите, които възприемаме като по-нататък, обикновено са в горната част на изображението, което означава, че имат по-малка :math:`y` координата, въпреки че това не винаги може да е вярно. В този и подобни примери ще бъде достатъчно да се придържаме към това просто правило: **по-добре е първо да се покажат обекти с по-малкa** :math:`y` **координата**. 

Задачи за упражнение
'''''''''''''''''''''

.. questionnote::

    **Задача - дървета**

    В следната програма коригирайте реда на позициите на дърветата в списъка и след това добавете оператор, за да нарисувате дърво на позиция (*x*, *y*) в цикъла.

.. activecode:: PyGame__images_trees3
    :nocodelens:
    :enablecopy:
    :modaloutput:
    :playtask:
    :includexsrc: src\PyGame\1_Drawing\9_UsingImages\trees_and_apples3.py
    
    tree_image = pg.image.load("tree.png")  # image of a tree
    canvas.fill(pg.Color("darkgreen"))
    tree_pos = [(240, 290), (400, 200), (550, 170), (120, 150), (200, 70)]
    
    for x, y in tree_pos:
        pass # complete the program



.. questionnote::

    **Задача - ябълки**

    Завършете програмата, като нарисувате дървото с ябълките (както е в примера).

.. activecode:: PyGame__images_trees2
    :nocodelens:
    :enablecopy:
    :modaloutput:
    :playtask:
    :includexsrc: src\PyGame\1_Drawing\9_UsingImages\trees_and_apples2.py
    
    tree_image = pg.image.load("tree.png")  # image of a tree
    apple_image = pg.image.load("apple_small.png")  # image of an apple
    apple_positions = ((43,191), (61, 158), (124, 145), (134, 175), (160, 180))

    # complete: paint the background in dark green, draw a tree and apples on it
   

After you finish the program, you can also try modifying the program to display an apple tree 100 pixels to the right and 50 pixels lower.

.. questionnote::

    **Задача - шахмат**

    Напишете програма, която очертава позиция в шах, както е в примера. Файловете за празна шахматна дъска, бял крал, бял топ и черен крал са съответно: "chess_table.png", "white_king.png", "white_rook.png", "black_king.png".
    
.. image:: ../../_images/chess_table.png
   :width: 50px

.. image:: ../../_images/white_king.png
   :width: 50px
    
.. image:: ../../_images/white_rook.png
   :width: 50px
   
.. image:: ../../_images/black_king.png
   :width: 50px

.. activecode:: PyGame__images_chess_mate
    :nocodelens:
    :enablecopy:
    :modaloutput:
    :playtask:
    :includexsrc: src\PyGame\1_Drawing\9_UsingImages\chess_mate.py
    


.. questionnote::

    **Задача - овощна градина**
    
    
    В следващата задача е стартирано рисуването на овощната градина. Ако стартираме програмата, ще забележим някои несъответствия. Един от проблемите е, че ябълките се намират само на първото дърво и те трябва да бъдат разположени на всяко дърво, подредени по един и същи начин. В допълнение, второто дърво отляво припокрива най-лявото дърво, но не припокрива ябълките си. Трябва да покажем дървото, което показваме по-рано, заедно с неговите ябълки, преди да преминем към следващото дърво.

Коригирайте програмата така, че да показва полученото изображение, като щракнете върху бутона „Play Task“.

.. activecode:: PyGame__images_trees_and_apples4
    :nocodelens:
    :enablecopy:
    :modaloutput:
    :playtask:
    :includexsrc: src\PyGame\1_Drawing\9_UsingImages\trees_and_apples4.py
   
    tree_image = pg.image.load("tree.png")  # image of a tree
    apple_image = pg.image.load("apple_small.png")  # image of an apple
    apple_positions = ((43,191), (61, 158), (124, 145), (134, 175), (160, 180))

    for tree_x, tree_y in ((0, 0), (200, 70), (120, 150), (240, 290), (550, 170), (400, 200)):
        canvas.blit(tree_image, (tree_x, tree_y))
        
    for apple_x, apple_y in apple_positions:
        canvas.blit(apple_image, (apple_x, apple_y))


