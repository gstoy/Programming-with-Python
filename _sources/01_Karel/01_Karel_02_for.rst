Съкратете програмите си
=======================

В предишната глава имаше задачи, при които би било удобно да имаме по-кратък начин да посочим някои повтарящи се действия. Например, Карел трябваше да извърви три стъпки напред. В случай на само три стъпки е достатъчно лесно да напишете три пъти операцията move (), но когато Karel трябва да направи, да речем, дванадесет стъпки напред, ако напишем:

.. activecode:: Karel_for_12_steps_manual
   :passivecode: true
   
   move(); move(); move(); move(); move()
   move(); move(); move(); move(); move()
   move(); move()

такъв начин на писане на програми е по-предразположен към грешки и също така е по-труден за четене. Ако смятате, че дори дванадесет повторения не са проблем, имайте предвид, че в света на програмирането не е рядкост цикълът да бъде повторен милион пъти.

*For* цикълът
---------------

 По-добър начин да се уточни подобна маневра би било да се каже „дванадесет пъти напред“. За да повторим цикъла определен брой пъти, използваме *for* оператор. Най-често използваната форма на този цикъл в Python изглежда така:

.. activecode:: Karel_for_syntax
   :passivecode: true
   
   for i in range(n):
       statement_1
       ...
       statement_k

По-късно ще видим и някои други форми на цикъла for.

Примерът с дванадесет повторения на една стъпка напред може да бъде написан по този начин:
      
.. activecode:: Karel_for_12_steps_loop
   :passivecode: true
   
   for i in range(12):
       move()


Тук даваме малко по-подробно описание на цикъла. Понастоящем не е необходимо да го разбирате напълно - използването и правилата за писането му ще станат по-ясни със следните примери. Ако имате нужда от повече подробности за for по-късно, можете да се върнете към това обяснение (но имайте предвид, че то не описва други форми на цикъла for).

.. infonote::

   - Според правилата за писане на програми в Python, ``for`` и ``in``, както и двоеточието ``:`` в края на реда са задължителни условия на оператора for.
   
   - Буквата i тук служи като мястото, където съхраняваме броя на повторенията. 
   
   - ``range(n)`` представлява диапазон от цели числа, започващи с 0, и n показва колко числа съдържа този диапазон. Например, обхват (3) е диапазонът, съдържащ числата 0, 1, 2, а диапазонът (7) е диапазонът на числата 0, 1, 2, 3, 4, 5, 6.

   - Следващите редове съставят така нареченото тяло на цикъла for. Това могат да бъдат всякакви оператори в Python, включително за управление на Karel, други за оператори или някои операции, които все още не сме споменавали. В тялото на цикъла може да има един или повече такива оператори.

   В i в диапазон (3) се интерпретира като: „стойност i в диапазона [0, 1, 2]“. Това означава, че операторите в тялото на оператора for се изпълняват веднъж за i = 0, за i = 1 и за i = 2, така че общо три пъти. Засега няма да използваме стойността на i в тялото на оператора, така че само трябва да знаем колко стойности има в диапазона (това е числото в скоби зад диапазона на думите), тъй като операциите в тялото ще бъдат изпълнява този брой пъти.

   За да се изясни какви оператори са в тялото на *for*, тези оператори се пишат с отстъпи (преместени надясно), всички за същия брой интервали. Можем да изберем броя на интервалите за отстъпи за всяко за операция. Добра практика е обаче винаги да избираме един и същ номер, защото по този начин ще свикнем с определеното оформление на програмата и кодът ще бъде по-четим. Най-често срещаният избор за отстъп са 4 пространства, така че ние също ще го приемем.

*For* е известен също като цикъл, тъй като следвайки операторита, които изпълняваме, когато стигнем до оператора for, ние преглеждаме няколко пъти през операторите в неговото тяло. Терминът „цикъл“ е по-малко прецизен, както скоро ще видим, операторът for не е единственият цикъл, който съществува. Думата "цикъл" обикновено се използва, когато е ясно (или не е от значение) за кой точно изказване на цикъла говорим, тъй като е по-лесно да се каже, например, "тяло на цикъла", а не за "тяло на оператора".

Задачи за упражнения
--------------------

Преместете се петнадесет полета напред и вземете топката 
''''''''''''''''''''''''''''''''''''''''''''''''''''''''

.. questionnote::

   Напишете програма, въз основа на която Карел ще се премести на поле (16, 1) и ще вземе топката.

По-дълга програма ви очаква в областта на решението. Опитайте да го замените с for. В случай, че вашето решение с for statement не работи (което често се случва в началото), можете да видите нашето решение, като кликнете върху бутона „Solution“ по-долу.

.. karel:: Karel_for_15_steps_and_take
   :blockly:

   {
      setup:function() {
          var world = new World(16, 1);
          world.setRobotStartAvenue(1);
          world.setRobotStartStreet(1);
          world.setRobotStartDirection("E");
          world.putBall(16, 1);
      
         var robot = new Robot();
      
         var code = ["from karel import *",
                     "move(); move(); move(); move(); move()",
                     "move(); move(); move(); move(); move()",
                     "move(); move(); move(); move(); move()",
                     "pick_ball()"];
                  
         return {robot:robot, world:world, code:code};
      },
      
      isSuccess: function(robot, world) {
         return robot.getBalls() === 1;
      }
   }

.. reveal:: Karel_for_15_steps_and_take_reveal
   :showtitle: Solution
   :hidetitle: Hide solution

   .. activecode:: Karel_for_15_steps_and_take_solution
      :passivecode: true
      
      from karel import *
      for i in range(15):
          move()
      pick_ball()

Преминете едно поле напред и съберете 10 топки
''''''''''''''''''''''''''''''''''''''''''''''

.. questionnote::

  Има едно поле пред Карел, а на него има 14 топки. Карел трябва да вземе точно десет топки.
  
.. karel:: Karel_for_one_square_take_10_balls
   :blockly:

   {
        setup:function() {
           var world = new World(2, 1);
           world.setRobotStartAvenue(1);
           world.setRobotStartStreet(1);
           world.setRobotStartDirection("E");
           
           world.putBalls(2, 1, 14);

           var robot = new Robot();

           var code = ["from karel import *",
                       "move()",
                       "# Complete the program",
                       ""];
           return {robot:robot, world:world, code:code};
        },
    
        isSuccess: function(robot, world) {
           return robot.getBalls() == 10;
        },
   }
   
.. reveal:: Karel_for_one_square_take_10_balls_reveal
   :showtitle: Solution
   :hidetitle: Hide solution

   .. activecode:: Karel_for_one_square_take_10_balls_solution
      :passivecode: true
      
      from karel import *
      move()
      for i in range(10):
          pick_ball()


Вземете по една топка от всеки от следващите 8 полета
'''''''''''''''''''''''''''''''''''''''''''''''''''''

.. questionnote::

  Пред Карел има осем квадрата, а на всеки от тях има по една топка. Карел трябва да вземе всички топки.
  
Забележете, че в цикъла трябва да присъстват две неща: придвижване напред и вземане на топката.

.. karel:: Karel_for_EightSquaresOneBallEach_TakeAllBalls
   :blockly:

   {
        setup:function() {
           var numAvenues = 9;
           var world = new World(numAvenues, 1);
           world.setRobotStartAvenue(1);
           world.setRobotStartStreet(1);
           world.setRobotStartDirection("E");
           
         for (var k = 2; k <= numAvenues; k++)
            world.putBall(k, 1);

           var robot = new Robot();

           var code = ["from karel import *",
                       "# Complete the program",
                       ""];
           return {robot:robot, world:world, code:code};
        },
    
        isSuccess: function(robot, world) {
           return robot.getBalls() == world.getAvenues() - 1;
        },
   }
   
.. reveal:: Karel_for_EightSquaresOneBallEach_TakeAllBalls_reveal
   :showtitle: Solution
   :hidetitle: Hide solution

   .. activecode:: Karel_for_EightSquaresOneBallEach_TakeAllBalls_solution
      :passivecode: true
      
      from karel import *
      for i in range(8):
          move()
          pick_ball()


Вземете по 5 топки от всеки от следващите три полета
''''''''''''''''''''''''''''''''''''''''''''''''''''

.. questionnote::

  Пред Карел има три квадрата, а на всеки от тях има по пет топки. Карел трябва да вземе всички топки.
  
.. karel:: Karel_for_Take_5_5_5
   :blockly:

   {
        setup:function() {
           var world = new World(4, 1);
           world.setRobotStartAvenue(1);
           world.setRobotStartStreet(1);
           world.setRobotStartDirection("E");
           
           world.putBalls(2, 1, 5);
           world.putBalls(3, 1, 5);
           world.putBalls(4, 1, 5);
           
           var robot = new Robot();

           var code = ["from karel import *",
                       "# Complete the program",
                       ""];
           return {robot:robot, world:world, code:code};
        },
    
        isSuccess: function(robot, world) {
           return robot.getBalls() == 15;
        },
   }
   
.. reveal:: Karel_for_Take_5_5_5_reveal
   :showtitle: Solution
   :hidetitle: Hide solution
   
   .. activecode:: Karel_for_Take_5_5_5_solution
      :passivecode: true
      
      from karel import *
      move()
      for i in range(5):
          pick_ball()
      move()
      for i in range(5):
          pick_ball()
      move()
      for i in range(5):
          pick_ball()
