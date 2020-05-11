Решете няколко задачи наведнъж
==============================

Съдейки по програмите, които видяхме досега, може да се мисли, че трябва да се напише специална програма за всяка, дори малко по-различна задача. Ако това беше така, програмирането би било много, много досадна работа.

За да приложим една програма към група сходни задачи, е необходимо тази програма да се държи различно в различни ситуации. Това означава, че ни е необходим начин програмата да разбере текущата ситуация и след това да избере кои команди ще бъдат изпълнени, в зависимост от ситуацията. Под ситуацията имаме предвид броя на топките на квадрат или с Карел, положението на стените около Карел и така нататък. Програма, която би могла да получи отговори на въпросите, касаещи Карел и околностите му, също би могла да реши няколко подобни задачи или (с други думи) обща задача.

Питай Карел
-----------

В началото на уводната глава видяхме команди за Карел, с които го инструктираме да извърши някои действия (да върви напред, да завива наляво и надясно, да взема и пуска топки). Тогава споменахме, че има пет други функции, свързани с Карел. Тези пет функции се различават от предишните, тъй като, използвайки тези функции, задаваме някои въпроси и получаваме отговорите за Карел или квадрата, на който се намира. Ето тези функции:

- ``front_is_clear()`` - питаме дали Карел може да продължи напред (има ли стени пред него). Получаваме отговора „да“ или „не“.
- ``num_balls_on_square()`` - питаме колко топки има на площада, на който е Карел. Получаваме броя на топките на площада.
- ``is_ball_on_square()`` - питаме дали има поне една топка на площада на Карел. Получаваме отговора „да“ или „не“.
- ``num_balls_with_karel()`` - питаме колко топки Karel в момента има с него. Получаваме броя на топките, които държи Карел.
- ``any_balls_with_karel()`` - питаме дали Карел има поне една топка със себе си. Получаваме отговора „да“ или „не“.

Не можем да напишем тези функции за даване на отговори като отделни оператори, както досега. Вместо това ние пишем тези функции като част от някои операции на Python. Нека разгледаме примерите.

Доколкото е необходимо  (оператор *while*)
------------------------------------------

Един от начините за използване на функциите, които дават отговора е да използвате оператора *while*. Макар че операторът съществува в почти всички езици за програмиране и е написан много сходно на различни езици. В Python изглежда така:

.. activecode:: while_syntax
   :passivecode: true

   while condition:
       statement_1
       ...
       statement_k

.. infonote::

    Смисълът на оператора while е: докато условието е изпълнено, изпълнете операторът или операторите, които са написани с отметка по-долу. Състоянието на думата по-горе означава всичко, което е написано правилно в Python, и се свежда до да или не (техническият термин за това „нищо“ е логичен израз).

    Правилата за писане на *while*, изискват писане на двоеточие: след условието. След условието (и двоеточие) пишем statements, които искаме да повторим, докато условието е изпълнено, тоест докато отговорът на въпроса вътре в условието е да (или Вярно). Тези повтарящи се statements съставляват тялото на оператора while и се пишат с отстъпи в следващите редове (същият брой интервали се добавят преди всяко от повторенията).

Условието се изследва преди всяко изпълнение на операторита в тялото на оператора while. Първият път, когато условието не е изпълнено, докато изпълнението на оператора (заедно с операторите в неговото тяло) е завършено, а следващото заявление, което трябва да бъде изпълнено, е посоченото под тялото на оператора while. Например, ако изпълним:

.. activecode:: while_example
   :passivecode: true

   while front_is_clear():
       move()
   pick_ball()

Карел ще продължи напред, доколкото може, тоест, докато не получим отговор „не“ на въпроса front_is_clear (), което означава, че Карел се е натъкнал на стена. Когато приключи да се движи, Карел ще вземе топката. В случай, че Карел вече е пред стената, командата move () изобщо няма да бъде изпълнена и Karel веднага ще вземе топката.

~~~~

Всеки от следните примери и задачи е общ. Това означава, че за всяка задача при различни стартирания на програмата задачата ще изглежда подобно, но малко по-различно. Програмата трябва да бъде написана, за да реши задачата във всеки от тези подобни случаи.

Продължете напред и вземете топката
'''''''''''''''''''''''''''''''''''

.. questionnote::

   Пред Карел има един или повече квадрата, а на последния площад има една топка. Напишете програма, която ще накара Карел да вземе топката от последния квадрат.

   **Програмата трябва да се стартира многократно**, тъй като при различни стартирания светът на Карел ще има различен брой квадратчета. Ето няколко примера за това как може да изглежда задачата:

   .. image:: ../../_images/Karel/While_01.jpg
      :width: 600px   
      :align: center

Ще използваме while statement, за да преместим Карел и след това да му кажем да вземе топката.

.. karel:: Karel_while__many_squares_and_ball_at_the_end
   :blockly:

   {
      setup:function() {
         function random(n) {
            return Math.floor(n * Math.random());
         }

         var N = 2 + random(14);
         var world = new World(N, 1);
         world.setRobotStartAvenue(1);
         world.setRobotStartStreet(1);
         world.setRobotStartDirection("E");
         world.putBall(N, 1);
      
         var robot = new Robot();
      
         var code = ["from karel import *",
                     "while front_is_clear():",
                     "    move()",
                     "pick_ball()"];
         return {robot:robot, world:world, code:code};
      },
      
      isSuccess: function(robot, world) {
         return robot.getBalls() === 1;
      }
   }

.. infonote::
    
    Може да се случи, че една програма често дава добър резултат, понякога дава лош резултат или се прекъсва поради грешка. **Такава програма трябва да се счита за дефектна.** Правилната програма винаги трябва да дава правилния резултат.

Задачи за упражнения
--------------------

Вървете едно поле напред и вземете всички топки
'''''''''''''''''''''''''''''''''''''''''''''''

.. questionnote::

  Има точно едно поле пред Карел, а върху него има произволен брой топки. Карел трябва да ги вземе.
  
Следвайки инструкциите в програмата по-долу, Karel ще се опита да повтори командата pick_ball() безкрайно. Когато обаче Карел вземе всички топчета от този квадрат, ще получим съобщение за грешка, защото казахме на Карел да вземе топка от празния квадрат (не се колебайте да опитате това и да видите как изглежда съобщението за грешка). Опитайте се да коригирате програмата, така че Карел да взема топките само докато има.

.. karel:: Karel_while__one_square_many_balls
   :blockly:

   {
        setup:function() {
           function random(n) {
              return Math.floor(n * Math.random());
           }
           
           var world = new World(2, 1);
           world.setRobotStartAvenue(1);
           world.setRobotStartStreet(1);
           world.setRobotStartDirection("E");
           
           var N = random(14);
           world.putBalls(2, 1, N);

           var robot = new Robot();

           var code = ["from karel import *",
                       "move()",
                       "while True: # instead of True use the function is_ball_on_square()",
                       "    pick_ball()",
                       ""];
           return {robot:robot, world:world, code:code};
        },
    
        isSuccess: function(robot, world) {
           var N = world.getAvenues();
           for (var k = 1; k <= N; k++)
              if (world.getBalls(k, 1) > 0)
                 return false;
               
           return true;
        },
   }

.. commented out
   .. reveal:: Karel_while__one_square_many_balls_reveal
      :showtitle: Solution
      :hidetitle: Hide solution
   
      .. activecode:: Karel_while__one_square_many_balls_solution
         :passivecode: true
         
         from karel import *
         move()
         while is_ball_on_square():
             pick_ball()

Вървете колкото можете, като вземате по една топка отвсяко поле
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

.. questionnote::

   Пред Карел има едно или повече полета, а на всяко има по една топка. Напишете програма, която кара Карел да събира топките от всичките.
   
   **Стартирайте тази програма няколко пъти** за да сте сигурни, че тя решава задачата, независимо от дължината на пътя на Карел.
   
Един while цикъл трябва да се използва както за движение на Карел, така и за вземане на топките.

.. karel:: Karel_while__many_squares_and_ball_at_each
   :blockly:

   {
      setup:function() {
         function random(n) {
            return Math.floor(n * Math.random());
         }

         var N = 2 + random(8);
         var world = new World(N, 1);
         world.setRobotStartAvenue(1);
         world.setRobotStartStreet(1);
         world.setRobotStartDirection("E");
         for (var k = 2; k <= N; k++)
             world.putBall(k, 1);

         var robot = new Robot();
      
         var code = ["from karel import *",
                     "# complete the program",
                     ];
         return {robot:robot, world:world, code:code};
      },
      
      isSuccess: function(robot, world) {
         return (robot.getBalls() == world.getAvenues() - 1);
      }
   }

Преместете всички топки от последното до първото поле
'''''''''''''''''''''''''''''''''''''''''''''''''''''

.. questionnote::

   Пред Карел има един или повече квадрати, а на последния няколко топки. Карел трябва да вземе всички топчета от последния квадрат и да ги остави на първия квадрат.
   
   (Стартирайте програмата няколко пъти.)
   
В тази задача са необходими четири цикъла един след друг (не един вътре в друг):
 - В първия Карел стига до последния квадрат
 - Във втория Карел взема топките
 - В третия Карел се връща към началния квадрат
 - В последния Карел оставя всички топчета, които има със себе си


Разбира се, след първия или втория, Karel трябва да се обърне към стартовото поле (два пъти вляво или два пъти вдясно).

.. karel:: Karel_while__bring_balls_to_front_square
    :blockly:

    {
        setup:function() {
            function random(n) {
                return Math.floor(n * Math.random());
            }

            var N = 2 + random(5);
            var world = new World(N, 1);
            world.setRobotStartAvenue(1);
            world.setRobotStartStreet(1);
            world.setRobotStartDirection("E");
            world.putBalls(N, 1, 2 + random(4));

            var robot = new Robot();
      
            var code = ["from karel import *",
                        "# go forward while you can",
                        "# take all the balls",
                        "turn_right()",
                        "turn_right()",
                        "# go forward while  you can",
                        "# drop all the balls",
                       ];
            return {robot:robot, world:world, code:code};
        },
      
        isSuccess: function(robot, world) {
            var N = world.getAvenues();
            for (var k = 2; k <= N; k++) {
                if (world.getBalls(k, 1) > 0)
                    return false;
            }
            if (robot.getBalls() > 0)
                return false;

            return true;
        }
    }
    
.. commented out
   .. reveal:: Karel_while__bring_balls_to_front_square_reveal
       :showtitle: Solution
       :hidetitle: Hide solution
   
       .. activecode:: Karel_while__bring_balls_to_front_square_solution
           :passivecode: true
         
           from karel import *
           while front_is_clear():
               move()
           while is_ball_on_square():
               pick_ball()
           turn_right()
           turn_right()
           while front_is_clear():
               move()
           while any_balls_with_karel():
               drop_ball()

Поставете топките в горния ред
''''''''''''''''''''''''''''''

.. questionnote::

  Светът на Карел този път се състои от два реда с една и съща, но неизвестна дължина. Карел е в долния ляв ъгъл, обърнат на изток. Всички квадратчета на горния ред са празни и всеки квадрат от първия ред съдържа една топка, включително квадрата, където е Карел. Задачата на Карел е да постави по една топка върху всеки квадрат от най-горния ред.

  (Стартирайте програмата няколко пъти.)
  
.. karel:: Karel_while__put_balls_in_upper_row
   :blockly:

   {
      setup:function() {
         function random(n) {
            return Math.floor(n * Math.random());
         }

         var N = 2 + random(4);
         var world = new World(N, 2);
         world.setRobotStartAvenue(1);
         world.setRobotStartStreet(1);
         world.setRobotStartDirection("E");
         for (var k = 1; k <= N; k++)
             world.putBall(k, 1);

         var robot = new Robot();
      
         var code = ["from karel import *",
                     "# complete the program",
                     ];
         return {robot:robot, world:world, code:code};
      },
      
      isSuccess: function(robot, world) {
          var N = world.getAvenues();
          for (var k = 1; k <= N; k++) {
              if (world.getBalls(k, 1) > 0)
                  return false;
              if (world.getBalls(k, 2) != 1)
                  return false;
          }
          if (robot.getBalls() > 0)
              return false;

          return true;
      }
   }

.. reveal:: Karel_while__put_balls_in_upper_row_reveal
    :showtitle: Hint
    :hidetitle: Hide hint
    
    We give instructions that resemble the program:

    .. activecode:: Karel_while__put_balls_in_upper_row_solution
        :passivecode: true
        
        pick up the ball
        while you can go forward:
            go forward
            pick up the ball
        turn towards the top row
        get in the top row
        turn towards the beginning of the row
        drop the ball
        while you can go forward:
            go forward
            drop the ball

.. commented out
    .. reveal:: Karel_while__put_balls_in_upper_row_reveal
        :showtitle: Solution
        :hidetitle: Hide solution

        .. activecode:: Karel_while__put_balls_in_upper_row_solution
            :passivecode: true
          
            from karel import *
            pick_ball()
            while front_is_clear():
                move()
                pick_ball()
            turn_left()
            move()
            turn_left()
            drop_ball()
            while front_is_clear():
                move()
                drop_ball()
