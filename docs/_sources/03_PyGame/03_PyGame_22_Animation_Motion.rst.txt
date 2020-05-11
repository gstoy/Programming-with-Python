Движение на рисунки
--------------------

Анимациите, които видяхме досега, се основават на показване на различно изображение, което сме подготвили предварително във всеки кадър. Сега също ще преместваме показаните изображения, така че едно и също изображение да се появява на различни места в прозореца, тоест да се движи.

Нека първо да разгледаме един пример:

.. image:: ../../_images/car.png
   :width: 50px

.. activecode:: PyGame__anim_car_oneway
    :nocodelens:
    :enablecopy:
    :modaloutput:
    :includesrc: src/PyGame/2_Animation/2b_Anim_Motion/car_rightwards_only.py

Както преди, имаме функция *new_frame*, която показва изображение във всеки кадър. Новото в този пример е, че позицията на това изображение се променя от кадър в кадър.

Изображението е показано така, че горният му ляв ъгъл да се появи в точката (*car_x*, *car_y*). За да може колата да се движи вдясно, във всеки кадър увеличаваме *x* координатата на изображението. Имаме предвид само, че когато колата отиде твърде далеч отдясно, връщаме колата така, че десният й край да се подравнява с левия ръб на прозореца. По този начин колата започва постепенно да се появява отново вляво.

~~~~

По подобен начин можем да движим и рисунки, които сами рисуваме (не само готови изображения). По този начин можем да преместим изображението или рисунката във всяка посока. Ето един пример:

.. activecode:: PyGame__anim_billiards
    :nocodelens:
    :enablecopy:
    :modaloutput:
    :includesrc: src/PyGame/2_Animation/2b_Anim_Motion/billiards.py

Забележете как проверяваме дали топката докосва ръба на екрана. Крайната дясна част на топката има координата *x*, равна на :math:`cx + r`. Ако тази стойност беше равна на ширината на прозореца, това би означавало, че топката докосва десния ръб на прозореца, а ако :math:`cx + r> width`, това означава, че топката вече частично е преминала вдясно ръб на прозореца. В този случай, с командата :math:`dx = -dx`, като се започне от следващия кадър, стойността, обратна на тази досега, ще бъде добавена към координатата *x* на топката, тоест топката ще отсега нататък се движат 3 пиксела вляво. Това ще изглежда, че топката отскочи от десния ръб на прозореца.

Забележете още един детайл: вместо :math:`cx + r> width`, бихме могли да използваме и :math:`cx + r> = width` и програмата ще работи почти същото. Но тъй като топката **не се движи с един пиксел**, тя не би била валидна, ако използвахме условието :math:`cx + r == width`, защото тогава топката може да пропусне позицията, която проверяваме и минете през ръба на прозореца.

Ние подробно анализирах случая на десния ръб на прозореца и същото разсъждение беше приложено и към други ръбове, когато програмата се пишеше. Общият ефект на двете команди *if* е, че топката отскача от всеки ръб на прозореца.

Проверете дали разбирате това, като отговорите на следните въпроси.

Движение на рисунки - въпроси
'''''''''''''''''''''''''''''

.. dragndrop:: pygame__anim_quiz_bounce1
    :feedback: Опитай пак!
    :match_1: for left edge ||| if cx - r < 0
    :match_2: for right edge ||| if cx + r > width
    :match_3: for top edge ||| if cy - r < 0
    :match_4: for bottom edge ||| if cy + r > height

    Съпоставете проверката дали топката от предишния пример е преминала определен ръб към съответната команда *if*.

.. mchoice:: pygame__anim_quiz_bounce2
    :answer_a: дясно
    :answer_b: горе
    :answer_c: ляво
    :answer_d: долу
    :correct: c
    :feedback_a: Опитай пак
    :feedback_b: Опитай пак
    :feedback_c: Вярно!
    :feedback_d: Опитай пак

    На каква страна се премества изображение, като добавя отрицателна стойност към координатата си *x*?

.. mchoice:: pygame__anim_quiz_bounce3
    :answer_a: if x + im_width < 0:
    :answer_b: if y + im_height < 0:
    :answer_c: if x < 0:
    :answer_d: if y < 0:
    :correct: b
    :feedback_a: Опитай пак
    :feedback_b: Вярно!
    :feedback_c: Опитай пак
    :feedback_d: Опитай пак

    Нека размерите на дадено изображение са *im_width* и *im_height*, а горният му ляв ъгъл (*x*, *y*). Как да проверим дали изображението е преминало напълно през горния ръб на прозореца и няма ли част от него да се вижда?

.. dragndrop:: pygame__anim_quiz_bounce4
    :feedback: Опитай пак!
    :match_1: the image came out through the left edge of the window ||| x + im_width < 0
    :match_2: the image began to come out through the left edge of the window ||| x < 0
    :match_3: the image came out through the right edge of the window ||| x > width
    :match_4: the image began to come out through the right edge of the window ||| x + im_width > width

    Нека 'width' е ширината на прозореца, 'im_width' ширината на изображението и (x, y) горния ляв ъгъл на изображението. Съобразете логическите условия с тяхното значение.

.. mchoice:: pygame__anim_quiz_bounce5
    :answer_a: x = width; dx = -10
    :answer_b: x = width + im_width; dx = -10
    :answer_c: x = width - im_width; dx = -10
    :answer_d: x = width + im_width; dx = 10
    :correct: a
    :feedback_a: Вярно!
    :feedback_b: Не, това е далеч от десния край
    :feedback_c: Не, по този начин цялото изображение вече е в прозореца.
    :feedback_d: Не, изображението е твърде далеч и ще продължава да става все по-далеч.

    Let *width* be the width of the window, *im_width* the width of the image, (*x*, *y*) the upper left corner of the image and *dx* the value by which the *x* coordinate of the image will be changed later. What commands will cause the image to begin to appear entering the window through the right edge?

Task - a car going left-right
'''''''''''''''''''''''''''''

Нека * width * е ширината на прозореца, *im_width* ширината на изображението, (*x*, *y*) горния ляв ъгъл на изображението и *dx* стойността, с която *x* координатата на изображението ще бъде променено по-късно. Какви команди ще накарат изображението да започне да се показва, влизайки в прозореца през десния ръб?

.. activecode:: PyGame__anim_car_right_left
    :nocodelens:
    :enablecopy:
    :modaloutput:
    :playtask:
    :includehsrc: src/PyGame/2_Animation/2b_Anim_Motion/car_right_left.py
    
    import pygame as pg, pygamebg
    (width, height) = (400, 300)
    canvas = pygamebg.open_window(width, height, "Car")
    
    car_rightwards_image = pg.image.load("car.png") 
    # creating flipped image (symmetric with respect to the vertical axis)
    car_leftwards_image = pg.transform.flip(car_rightwards_image, True, False)
    car_images = (car_rightwards_image, car_leftwards_image)
    fps = 50
    
    def new_frame():
        pass
        
    pygamebg.frame_loop(fps, new_frame)

        
