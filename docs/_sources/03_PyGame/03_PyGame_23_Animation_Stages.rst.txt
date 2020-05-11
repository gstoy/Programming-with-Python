Анимация по етапи
-------------------

Светофар
'''''''''''''

Един от най-известните примери за устройство, което работи на етапи, е светофар. В примера на светофара ще обясним работата по етапи и как можем да анимираме събития, които се провеждат поетапно на компютър.

Има няколко състояния, в които може да бъде светофар. Например, тя може да показва червена светлина, мигаща жълта светлина, да бъде изключена и т.н. Ще наречем период, през който светофарът не променя състоянието си етап. При нормална работа на светофара, етапите се редуват циклично и всеки етап има собствена продължителност. Например вземете светофар, за който се редуват следните четири етапа: 1 - червена светлина, 2 - червена и жълта светлина, 3 - зелена светлина и 4 - жълта светлина.

За да направим анимацията по-проста, ще изразим продължителността на всеки етап в броя на кадрите (вместо секунди). Нека продължителността на посочените етапи да бъде :math:`n_1`, :math:`n_2`, :math:`n_3` и :math:`n_4` кадрите съответно. Тогава целият цикъл продължава :math:`N = n_1 + n_2 + n_3 + n_4` кадри. От тях :math:`N` кадри, първият :math:`n_1` принадлежат към първия етап, следващият :math:`n_2` към втория етап и т.н.

За да знаем към кой етап принадлежи текущият кадър, можем да въведем глобална променлива, която ще брои кадрите. Тъй като целият цикъл трае :math:`N` кадри, достатъчно е да се брои по модул :math:`N`. Това означава, че когато броячът на кадрите достигне стойността :math:`N-1`, следващата стойност е нула (отчитаме само в рамките на един цикъл). В този случай, за стойности от 0 до :math:`n_1 - 1`, кадърът принадлежи към първия етап, за стойности от :math:`n_1` до :math:`n_1 + n_2 - 1` към втория етап , за стойности от :math:`n_1 + n_2` до :math:`n_1 + n_2 + n_3 - 1` до третия етап, а за стойности от :math:`n_1 + n_2 + n_3` до :math:`N -1` до четвъртия етап.

Ето как може да изглежда програмата, базирана на тази логика:

.. activecode:: PyGame__anim_stages_traffic_lights1
    :nocodelens:
    :modaloutput:
    :includesrc: src/PyGame/2_Animation/2c_Anim_Stages/TrafficLights1.py

Задачи
'''''''

.. questionnote::

    **Етап пети:** Копирайте предишната програма, след това поставете етап за мигаща зелена светлина, след зелената светлина и преди жълтата светлина (както е показано в примера - бутон "Play Task").
    
**Съвет:** В петата фаза няма да имаме нито едно обаждане към функцията *draw_trafficlights*, а по-скоро парче код, което изглежда така:

.. code::

        if i_frame % 2 == 0:
            draw_trafficlights(...)
        else:
            draw_trafficlights(...)


.. activecode:: PyGame__anim_stages_traffic_lights1a
    :nocodelens:
    :modaloutput:
    :playtask:
    :includehsrc: src/PyGame/2_Animation/2c_Anim_Stages/TrafficLights1a.py

.. questionnote::

    **Самолет:** Напишете програма, която работи, както е показано в примера (бутон „Play Task“).  
    
    Описание на движението: равнината започва от центъра на левия ръб на прозореца. Първо се движи за 20 кадъра 2 пиксела надясно и нагоре, след това 20 кадъра 2 пиксела надясно и надолу. Когато излезе през десния ръб на прозореца, той се появява на същата височина в левия ръб. Скоростта на кадрите е 50 кадъра в секунда. 

.. image:: ../../_images/airplane.png
   :width: 50px
.. image:: ../../_images/sun.png
   :width: 50px

.. activecode:: PyGame__anim_stages_plane
    :nocodelens:
    :modaloutput:
    :playtask:
    :includehsrc: src/PyGame/2_Animation/2c_Anim_Stages/airplane.py
    
    import pygame as pg, pygamebg
    (width, height) = (800, 350)
    canvas = pygamebg.open_window(width, height, "Plane")
    
    def new_frame():
        pass
    
    pygamebg.frame_loop(50, new_frame)


    sun_image = pg.image.load("sun.png")        # image of the sun
    plane_image = pg.image.load("airplane.png") # image of the plane
    plane_width = plane_image.get_width()       # plane image width
    plane_height = plane_image.get_height()     # plane image height

    # finish the program


.. questionnote::

    **Къртица** Напишете програма, която работи както е показано в примера (бутон „Play Task“).  
    
    10 изображения се зареждат с къртица, излизаща от дупката малко повече във всяко изображение. Цикълът има четири етапа с общо 28 кадъра. 
    
    - Етап първи трае 10 кадъра и по време на този етап къртицата излиза от дупката (изображенията са показани в ред, от първи до десети).
    - Етап втори продължава 5 кадъра, през които къртицата е в най-високото положение (показано е десетото изображение).
    - Етап три трае 10 кадъра и по време на този етап къртицата влиза в дупката (изображенията се показват от десето до първо място).
    - Етап четири трае 3 кадъра и по време на него къртицата е в дупката (показано е първото изображение).

.. image:: ../../_images/mole1.png
   :width: 50px
.. image:: ../../_images/mole2.png
   :width: 50px
.. image:: ../../_images/mole3.png
   :width: 50px
.. image:: ../../_images/mole4.png
   :width: 50px
.. image:: ../../_images/mole5.png
   :width: 50px
.. image:: ../../_images/mole6.png
   :width: 50px
.. image:: ../../_images/mole7.png
   :width: 50px
.. image:: ../../_images/mole8.png
   :width: 50px
.. image:: ../../_images/mole9.png
   :width: 50px
.. image:: ../../_images/mole10.png
   :width: 50px

.. activecode:: PyGame__anim_stages_mole
    :nocodelens:
    :modaloutput:
    :playtask:
    :includehsrc: src/PyGame/2_Animation/2c_Anim_Stages/mole.py

    import pygame as pg, pygamebg
    (width, height) = (150, 150)
    canvas = pygamebg.open_window(width, height, "Mole")

    images = []   # list that will contain the images
    for i in range(1, 11): # reading images mole1.png, ..., mole10.png into the list
        image_name = "mole" + str(i) + ".png"  # building the image name from parts
        images.append(pg.image.load(image_name))

    brown = (60, 42, 3)
    Y_HORIZON = 125
    GROUND = (0, Y_HORIZON, width, height - Y_HORIZON) # part of the image under the horizon
    i_frame = 0 # frame counter
    i_image = 0

    def new_frame():
        # complete the function - calculate which image is displayed in this frame

        canvas.fill(pg.Color("skyblue"))     # paint background
        pg.draw.rect(canvas, brown, GROUND)  # paint rectangle GROUND to brown
        canvas.blit(images[i_image], (0, 0)) # display the image

    pygamebg.frame_loop(10, new_frame)
