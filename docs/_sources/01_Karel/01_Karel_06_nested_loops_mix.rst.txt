Комбиниране на цикли
====================

Видяхме, че в тялото на един оператор можем да поставим няколко различни оператора. Подобно на оператора for, в оператора while също можем (в допълнение към други команди) да поставим нов оператор на цикъл и той може да бъде или време, или цикъл. По този начин можем да изградим различни комбинации от вмъкнати цикли.

Когато двата цикъла са вкарани един в друг, ние ги наричаме двоен цикъл, докато три вложени цикли се наричат троен цикъл. По подобен начин можем да вмъкнем произволен брой цикли един в друг, просто рядко се нуждаем от голям брой вмъкнати цикли.

В този урок ще практикуваме писане на комбинации от вмъкнати *for*  и *while*.

Различни двойни и множество цикли - задачи
------------------------------------------

Вземете 4 топки на всяко поле до края на реда
''''''''''''''''''''''''''''''''''''''''''''''

.. questionnote::

  Пред Карел има едно или повече полета, като на всяко от тези полета има четири топки (без началното поле). Карел трябва да ги вземе всички.
  
Сега, докато стигне до стената, Карел трябва да повтори стъпването си напред и да вземе 4 топки. Опитайте да допълните програмата.

Спомнете си, както в по-ранните примери за вмъкване на цикли, операторът в тялото на вътрешния цикъл (тук това ще бъде командата pick_ball ()) трябва да бъде по-нататък с отстъпи.

.. karel:: Karel_while__many_squares_four_bals_per_square
   :blockly:

   {
      setup:function() {
         function random(n) {
            return Math.floor(n * Math.random());
         }

         var N = 2 + random(9);
         var world = new World(N, 1);
         world.setRobotStartAvenue(1);
         world.setRobotStartStreet(1);
         world.setRobotStartDirection("E");
         for (var k = 2; k <= N; k++)
             world.putBalls(k, 1, 4);
      
         var robot = new Robot();
      
         var code = ["from karel import *",
                     "while front_is_clear():",
                     "    move()",
                     "    # add missing statements",
                     ""];
                     //from karel import *
                     //while front_is_clear():
                     //    move()
                     //    for i in range(4):
                     //        pick_ball()
         return {robot:robot, world:world, code:code};
      },
      
      isSuccess: function(robot, world) {
         var N = world.getAvenues();
         for (var k = 1; k <= N; k++)
            if (world.getBalls(k, 1) > 0)
               return false;
               
         return true;
      }
   }
   
..  commented out
    .. reveal:: Karel_while__many_squares_four_bals_per_square_reveal
       :showtitle: Solution
       :hidetitle: Hide solution
    
       .. activecode:: Karel_while__many_squares_two_bals_per_square_solution
          :passivecode: true
          
          from karel import *
          while front_is_clear():
              move()
              for i in range(4):
                  pick_ball()
   
   
Вземете всички топчета
''''''''''''''''''''''

.. questionnote::

  Има поне едно поле пред Карел и може да има произволен брой от тях. На всеки от полетата пред Карел има нула или повече топки (началният квадрат е празен). Карел трябва да вземе всички топки.

Тази задача е обобщаването на предишната, така че програмата, която решава тази задача, може да се използва и в предишната. Разликата е, че сега вътрешният цикъл трябва да бъде с оператор *while*, докато в предишната задача би могъл да бъде и с оператор *for*.

Отново командата pick_ball () трябва да бъде вкарано по-навътре. По този начин, той ще се повтори, докато състоянието на вътрешния while стане вярно, тоест докато има топка на полето, на което се намира Карел в този момент. Вземането на всички топки, заедно с инструкцията за движение се повтаря във външния while цикъл, стига да има полета пред Карел. Общият ефект от вмъкването на цикли е, че всичките топки от всеките полета ще бъдат взети.

.. karel:: Karel_while__many_squares_many_balls
   :blockly:

   {
      setup:function() {
         function random(n) {
            return Math.floor(n * Math.random());
         }

         var N = 2 + random(9);
         var world = new World(N, 1);
         world.setRobotStartAvenue(1);
         world.setRobotStartStreet(1);
         world.setRobotStartDirection("E");
         
         for (var k = 2; k <= N; k++) {
            let B = random(7);
            world.putBalls(k, 1, B);
         }
      
         var robot = new Robot();
      
         var code = ["from karel import *",
                     "while front_is_clear():",
                     "    # go forward",
                     "    while ... # finish the program",
                     ""];
         return {robot:robot, world:world, code:code};
      },
      
      isSuccess: function(robot, world) {
         var N = world.getAvenues();
         for (var k = 1; k <= N; k++)
            if (world.getBalls(k, 1) > 0)
               return false;
               
         return true;
      }
   }

Донесете всички топчета
'''''''''''''''''''''''

.. questionnote::

  Пред Карел има пътека с неизвестна дължина. Карел трябва да събере всички топки от всички полета и дасе върне в началото.

Програмата е разбита на по-малки парчета от коментарите. Добавете липсващите оператори.

.. karel:: Karel_while__bring_all_balls
   :blockly:

   {
      setup:function() {
         function random(n) {
            return Math.floor(n * Math.random());
         }

         var N = 2 + random(9);
         var world = new World(N, 1);
         world.setRobotStartAvenue(1);
         world.setRobotStartStreet(1);
         world.setRobotStartDirection("E");
         
         for (var k = 1; k <= N; k++) {
            let B = random(7);
            world.putBalls(k, 1, B);
         }
      
         var robot = new Robot();
         
         var code = ["from karel import *",
                     "# use double loop to take all balls from all squares",
                     "",
                     "",
                     "turn_left(); turn_left()                # turn back",
                     "# tell Karel to go back to the starting square ",
                     "# (that is, to move forward while he can)",
                     "",
                     "while any_balls_with_karel():",
                     "    # drop one ball",
                     ""];

           return {robot:robot, world:world, code:code};
        },
    
        isSuccess: function(robot, world) {
           var N = world.getAvenues();
           for (var k = 2; k <= N; k++)
              if (world.getBalls(k, 1) > 0)
                 return false;
               
           if (robot.getBalls() > 0)
                 return false;
                 
           return true;
        },
   }

..  commented out
    .. reveal:: Karel_while__bring_all_balls_reveal
       :showtitle: Solution
       :hidetitle: Hide solution

       .. activecode:: Karel_while__bring_all_balls_solution
          :passivecode: true
          
          from karel import *
          while front_is_clear():          # bring all balls from all squares
              move()
              while is_ball_on_square():
                  pick_ball()
                
          turn_left(); turn_left()         # turn back
          
          while front_is_clear():          # go back to the starting square
              move()
              
          while any_balls_with_karel():    # drop all the balls
              drop_ball()


Горе и долу
'''''''''''

.. questionnote::

  Карел е на правоъгълна дъска с неизвестен размер (броят на колоните винаги е нечетен), без топки по полетата. Целта е Карел да достигне долния десен ъгъл. За да постигне това, Карел ще трябва да се движи през колоните последователно нагоре и надолу.
  
   Лабиринтът би могъл да изглежда ето така:

   .. image:: ../../_images/Karel/While_UpDown.jpg
      :width: 600px   
      :align: center

.. karel:: Karel_while__up_col_down_col
   :blockly:

   {
      setup:function() {
         function random(n) {
            return Math.floor(n * Math.random());
         }

         var X2 = 1 + random(4);
         var Y = 2 + random(5);
         var world = new World(2*X2+1, Y);
         world.setRobotStartAvenue(1);
         world.setRobotStartStreet(1);
         world.setRobotStartDirection("E");
            
         world.addEWWall(1, 1, 1);
         for (let x = 0; x < X2; x++) { 
            world.addNSWall(2*x + 1, 2, Y - 1);
            world.addNSWall(2*x + 2, 1, Y - 1);
         }
         
         var robot = new Robot();
         
         var code = ["from karel import *",
                     "# add the missing statements",
                     ""];
                     //from karel import *
                     //while front_is_clear():        # while you are not in the bottom right corner
                     //    move(); turn_left()            # enter the next column and turn north
                     //    while front_is_clear():        # go to the top edge
                     //        move()
                     //
                     //    turn_right(); move(); turn_right() # move to the next column and turn south
                     //    while front_is_clear():        # go to the bottom edge
                     //        move()
                     //
                     //    turn_left()                    # turn east
    
         return {robot:robot, world:world, code:code};
      },
    
      isSuccess: function(robot, world) {
         return robot.getAvenue() == world.getAvenues() &&
            robot.getStreet() == 1;
      },
   }

.. reveal:: Karel_while__up_col_down_col_reveal
   :showtitle: Hint
   :hidetitle: Hide hint

   .. activecode:: Karel_while__up_col_down_col_solution
      :passivecode: true
      
      from karel import *
      while front_is_clear(): # while you are not in the bottom right corner
          move(); turn_left()     # enter the next column and turn north
          ... # finish this part  # go to the top edge

          turn_right(); move()    # move to the next column
          turn_right()            # turn south
          ... # finish this part  # go to the bottom edge

          turn_left()             # turn east

Стълбище
''''''''

.. questionnote::

  Карел трябва да се изкачи по първите стълби, след това да слезе по другите и да се озове в долния десен ъгъл. Размерът на таблицата не е известен, но броят на колоните винаги ще бъде нечетен. Таблицата може да изглежда така:
  
   .. image:: ../../_images/Karel/While_Stairs.jpg
      :width: 600px   
      :align: center

.. karel:: Karel_while__stairs
   :blockly:

   {
      setup:function() {
         function random(n) {
            return Math.floor(n * Math.random());
         }

         var Y = 2 + random(6);
         var X = 2 * Y - 1;
         var world = new World(X, Y);
         world.setRobotStartAvenue(1);
         world.setRobotStartStreet(1);
         world.setRobotStartDirection("E");

         // Vertical walls
         for (let y = 1; y < Y; y++) world.addNSWall(y, y, 1); // low left
         for (let y = 1; y < Y; y++) world.addNSWall(X - 1 - y, y, 1); // low right
         for (let y = 3; y <= Y; y++) world.addNSWall(y - 2, y, 1); // high left
         for (let y = 2; y <= Y; y++) world.addNSWall(X + 1 - y, y, 1); // high right
         
         // Horizontal walls
         for (let y = 1; y < Y - 1; y++) world.addEWWall(y + 1, y, 1); // low left
         for (let y = 2; y < Y; y++) world.addEWWall(y - 1, y, 1); // high left
         for (let y = 1; y < Y - 1; y++) world.addEWWall(X - 1 - y, y, 1); // low right
         for (let y = 1; y < Y; y++) world.addEWWall(X + 1 - y, y, 1); // high right

         var robot = new Robot();
         
         var code = ["from karel import *",
                     "# add missing statements",
                     ""];
                     //from karel import *
                     //turn_left()                       # northwards
                     //while front_is_clear():           # while there are stairs up
                     //    move(); turn_right(); move(); turn_left() #    climb up one stair
                     //
                     //turn_right(); turn_right()        # southwards
                     //
                     //while front_is_clear():           # while there are srairs down
                     //    move(); turn_left(); move(); turn_right() #    come down one stair 
    
         return {robot:robot, world:world, code:code};
      },
    
      isSuccess: function(robot, world) {
         return robot.getAvenue() == world.getAvenues() &&
            robot.getStreet() == 1;
      },
   }

.. reveal:: Karel_while__stairs_reveal
   :showtitle: Hint
   :hidetitle: Hide hint

   .. activecode:: Karel_while__stairs_solution
      :passivecode: true
      
      from karel import *
      turn_left()                        # northwards
      while front_is_clear():            # while there are stairs up
          move(); turn_right(); move(); turn_left() # climb up one stair

      turn_right(); turn_right()         # southwards
      
      while ... # add the condition      # while there are srairs down
          ... # add 4 statements             # come down one stair


Спирала вляво
'''''''''''''

.. questionnote::

  Във всички показани случаи Карел трябва да стигне до полето, отбелязано с червен кръг (в тази задача няма топки).
   
   .. image:: ../../_images/Karel/While_SpiralLeft.jpg
      :width: 600px   
      :align: center


.. karel:: Karel_while__spiral_left
   :blockly:

   {
      setup:function() {
         function random(n) {
            return Math.floor(n * Math.random());
         }

      var N = 1 + random(7);
      var world = new World(N, N);
      world.setRobotStartAvenue(1);
      world.setRobotStartStreet(1);
      world.setRobotStartDirection("E");
      
      var i = 1;
      for (let d = N - 1; d > 0; d -= 2) { world.addEWWall(i, i, d); i++; }
      i = 2;
      for (let d = N - 2; d > 0; d -= 2) { world.addEWWall(i, N+1-i, d); i++; }
      i = 2;
      for (let d = N - 2; d > 0; d -= 2) { world.addNSWall(N+1-i, i, d); i++; }
      i = 1;
      for (let d = N - 3; d > 0; d -= 2) { world.addNSWall(i, i+2, d); i++; }
   
      var robot = new Robot();
      
      var code = ["from karel import *",
                  "# finish the incomplete statements",
                  "while front_is_clear():",
                  "    while ... ",
                  "        ... ",
                  "    turn_left()",
                  ""];

        return {robot:robot, world:world, code:code};
     },
 
     isSuccess: function(robot, world) {
        var N = world.getAvenues();
        return robot.getStreet() === Math.floor((N+2)/2) &&
           robot.getAvenue() === Math.floor((N+1)/2);
     },
   }

.. reveal:: Karel_while__spiral_left_reveal
   :showtitle: Solution
   :hidetitle: Hide solution

   .. activecode:: Karel_while__spiral_left_solution
      :passivecode: true
      
      from karel import *
      while front_is_clear():
          while front_is_clear():
              move()
          turn_left()

