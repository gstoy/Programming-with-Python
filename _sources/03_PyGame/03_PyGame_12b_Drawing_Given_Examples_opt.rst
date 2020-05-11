Drawing from reference - допълнителни примери
----------------------------------------------

Предполагаме, че вече сте придобили известни умения в четенето на координати и извикване на функции за рисуване на основни фигури. Следователно в следващите задачи ще има някои нови предизвикателства.

Много рисунки имат някаква закономерност, като аксиална симетрия или част от рисунката, повтаряща се. Ако искате да направите такава рисунка сами, за да изглежда добре, не можете да избирате всички точки напълно свободно. Вместо това трябва да се изберат някои точки и да се изчислят някои точки.

За да се доближим до създаването на изображения, които сами проектираме, начинът на уточняване на чертежите е леко променен. Рисунките все още се уточняват с примерна програма, която рисува изображение (има поговорка, че едно изображение струва 1000 думи). Новото е, че няма да е възможно да прочетете една или двете координати в някои части на изображението, но вместо това ще трябва да изчислите тези координати въз основа на известни координати.

Освен че се нуждаят от малко изчисление, чертежите в следващите задачи имат и повече подробности, така че да отнеме малко повече време.

Ограда
'''''''

В тази задача четенето на координатата :math:`x` е ограничено до първия пикет на оградата и първото пространство. Всички останали необходими координати могат да бъдат изчислени. 

.. activecode:: PyGame__drawing_fence
   :nocodelens:
   :enablecopy:
   :modaloutput:
   :playtask:
   :includexsrc: src\PyGame\1_Drawing\4_ByGrid_Additional\fence_assist.py
   
.. reveal:: PyGame__drawing_fence_reveal
   :showtitle: Show solution
   :hidetitle: Hide solution

   The complete program is provided, you can try it here as well.
	       
   .. activecode:: PyGame__drawing_fence_solution
      :nocodelens:
      :enablecopy:
      :modaloutput:
      :includesrc: src\PyGame\1_Drawing\4_ByGrid_Additional\fence.py

Сграда
''''''''

Всички прозорци на сградата са с еднакъв размер, пространствата между етажите са равни, а лявата и дясната страна на сградата са симетрични (с изключение на това, че симетричните прозорци не са непременно един и същи цвят). Използвайте тази информация, за да изчислите координатите, които не можете да четете.

.. activecode:: PyGame__drawing_building
   :nocodelens:
   :enablecopy:
   :modaloutput:
   :playtask:
   :includexsrc: src\PyGame\1_Drawing\4_ByGrid_Additional\building_assist.py
   
.. commented out 

    .. reveal:: PyGame__drawing_building_reveal
       :showtitle: Show solution
       :hidetitle: Hide solution

       The complete program is provided, you can try it here as well.
               
       .. activecode:: PyGame__drawing_building_solution
          :nocodelens:
          :enablecopy:
          :modaloutput:
          :includesrc: src\PyGame\1_Drawing\4_ByGrid_Additional\building.py

Stickman
''''''''

В този пример координатите на точките на десния крак не могат да бъдат прочетени, но са симетрични спрямо левия крак. Тъй като ширината на изображението е известна (вижте началото на програмата), координатите на двете неизвестни точки вдясно могат да бъдат изчислени с помощта на известните симетрични точки вляво.

**Съвет:** Нека :math:`A` е точка от лявата страна на изображението и :math:`B` точка от дясната страна на изображението, симетрична на точката :math:`A`. След това двете точки имат една и съща :math:`y` координата, а сумата от :math:`x` координати на точките :math:`A` и :math:`B` е равна на ширината на изображението. 

.. activecode:: PyGame__drawing_stickman
   :nocodelens:
   :enablecopy:
   :modaloutput:
   :playtask:
   :includexsrc: src\PyGame\1_Drawing\4_ByGrid_Additional\stickman_assist.py
   
.. commented out 

    .. reveal:: PyGame__drawing_stickman_reveal
       :showtitle: Show solution
       :hidetitle: Hide solution

       The complete program is provided, you can try it here as well.
               
       .. activecode:: PyGame__drawing_stickman_solution
          :nocodelens:
          :enablecopy:
          :modaloutput:
          :includesrc: src\PyGame\1_Drawing\4_ByGrid_Additional\stickman.py

Коте
'''''

Ушите на тази котка могат да бъдат изобразени като пълни триъгълници. Тъй като ушите са прикрепени към главата, два върха на всеки триъгълник могат да бъдат избрани с повече свобода (достатъчно е да ги поставите някъде вътре в кръга на главата). В допълнение към двата триъгълника, представляващи ушите, имаме и:

- два кръга (глава и върха на муцуната)
- шест елипси (очи, зеници и части на муцуната)
- шест реда (мустаци)

:math:`x` координатите от дясната страна на изображението не могат да бъдат прочетени, но те могат да бъдат изчислени с помощта на симетрия (и известната ширина на изображението - вижте началото на програмата). 


.. activecode:: PyGame__drawing_cat
   :nocodelens:
   :enablecopy:
   :modaloutput:
   :playtask:
   :includexsrc: src\PyGame\1_Drawing\4_ByGrid_Additional\cat_assist.py

.. reveal:: PyGame__drawing_cat_reveal
   :showtitle: Show solution
   :hidetitle: Hide solution

   The complete program is provided, you can try it here as well.
	       
   .. activecode:: PyGame__drawing_cat_solution
      :nocodelens:
      :enablecopy:
      :modaloutput:
      :includesrc: src\PyGame\1_Drawing\4_ByGrid_Additional\cat.py

