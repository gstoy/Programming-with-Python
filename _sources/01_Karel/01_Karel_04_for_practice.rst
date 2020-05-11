For statement -  упражнения
============================

В този раздел ще практикуваме само използването на oператорът *for*.

Задачи за упражнения
--------------------

Три пъти нагоре и надолу
''''''''''''''''''''''''

.. questionnote::

  Карел е на правоъгълна дъска от 5 реда и 7 колони и трябва да достигне десен долен ъгъл.


Karel трябва да повтори едно сложно действие три пъти, т.е. последната колона, за да се подготвите за следващата итерация.

Завършете програмата, като вземете предвид, че броячът в циклите, които пишете, не трябва да бъде кръстен i (това име вече се използва във външния цикъл).

.. karel:: Karel_for_up_col_down_col_constant
   :blockly:

   {
      setup:function() {

         var X2 = 3;
         var Y = 5;
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
                     "for i in range(3):   # repeat everything that follows 3 times",
                     "    move(); turn_left()  # Enter the next column and turn north",
                     "    # use the for statement to tell Karel to go to the top edge",
                     "    ",
                     "    turn_right(); move() # go to the next column",
                     "    turn_right()             # turn south",
                     "    # use the for statement to tell Karel to go to the bottom edge",
                     "    ",
                     "    turn_left()          #    turn east",
                     ""];
    
         return {robot:robot, world:world, code:code};
      },
    
      isSuccess: function(robot, world) {
         return robot.getAvenue() == world.getAvenues() &&
            robot.getStreet() == 1;
      },
   }

.. reveal:: Karel_for_up_col_down_col_constant_reveal
   :showtitle: Solution
   :hidetitle: Hide solution

   .. activecode:: Karel_for_up_col_down_col_constant_solution
      :passivecode: true
      
      from karel import *
      for i in range(3):       # repeat everything that follows 3 times
          move(); turn_left()      # go to the next column and turn north
          for i_up in range(4):    # go to the top edge
              move()

          turn_right(); move()     # go to the next column
          turn_right()             # turn south
          for i_down in range(4):  # go to the bottom edge
              move()

          turn_left()              # turn east

Донесете всички топчета от всички полета
''''''''''''''''''''''''''''''''''''''''

.. questionnote::

  Карел трябва да донесе всичките 12 топки на стартовото поле.

Карел трябва да повтори „стъпка в следващата колона и да я изпразни“ четири пъти и в крайна сметка да се върне на началното поле и да пусне всички топчета. Karel може да изпразни всяка колона, като повтаря три пъти напред и вземете топката и след това се върне в долната част на колоната с лице към следващата колона.

Завършете програмата.

.. karel:: Karel_for_fetch_from_matrix
   :blockly:

   {
      setup:function() {
         var X = 5;
         var Y = 4;
         var world = new World(X, Y);
         world.setRobotStartAvenue(1);
         world.setRobotStartStreet(1);
         world.setRobotStartDirection("E");

         world.addEWWall(1, 1, 1);
         world.addNSWall(1, 2, Y - 1);
         
         for (var col = 2; col <= X; col++) {
            for (var row = 2; row <= Y; row++) {
               world.putBall(col, row);
            }
         }
         
         var robot = new Robot();
         
         var code = ["from karel import *",
                     "for i_column in range(4):      # repeat four times emptying one column",
                     "    move()                     # enter the next column",
                     "    turn_left()                # turn north",
                     "    #for ...                       # repeat 'move forward and take the ball' 3 times",
                     "",
                     "    turn_right(); turn_right() # turn south",
                     "    #for ...                   # go 3 steps forward to the bottom edge",
                     "",
                     "    turn_left()                # turn east",
                     "    ",
                     "# (Karel went through all the squares)",
                     "turn_left()                    # turn west",
                     "turn_left()",
                     "#for ...                       # come back to the starting square",
                     "    ",
                     "for i_ball in range(12):       # drop all the balls",
                     "    drop_ball()",
                     ""];
    
         return {robot:robot, world:world, code:code};
      },
    
      isSuccess: function(robot, world) {
         return world.getBalls(1, 1) == 12 &&
            robot.getAvenue() == 1 &&
            robot.getStreet() == 1;
      },
   }

.. reveal:: Karel_for_fetch_from_matrix_reveal
   :showtitle: Solution
   :hidetitle: Hide solution

   .. activecode:: Karel_for_fetch_from_matrix_solution
      :passivecode: true
      
      from karel import *
      for i_column in range(4):    # repeat emptying one column four times
          move()                       # enter the next column
          turn_left()                  # turn north
          for i_row in range(3):       # go to the top edge, picking the balls along
              move()
              pick_ball()

          turn_right(); turn_right()   # turn south
          for i_row in range(3):       # go to the bottom edge
              move()

          turn_left()                  # turn east (to the next column)
         
      turn_left()                  # turn west
      turn_left()
      for i_column in range(4):    # come back to the starting square
          move()
         
      for i_ball in range(12):     # drop all the balls
          drop_ball()


Троен цикъл
'''''''''''

.. questionnote::

  Сега има 4 топки на всеки от 6-те квадрата, подобно на предишната задача. Карел трябва да донесе всичките 24 топки на стартовия квадрат.


Единствената разлика (в сравнение с предишната задача) е, че pick_ball () трябва да бъде в допълнителен цикъл, трети по дълбочина. Също така броят на топките, които Карел пуска на стартовия квадрат (в края на програмата), е различен. Следователно, малко по-лесен начин за решаване на задачата е да копирате предишната програма и да я модифицирате.

.. karel:: Karel_for_fetch_24_from_matrix
   :blockly:

   {
      setup:function() {
         var X = 3;
         var Y = 4;
         var world = new World(X, Y);
         world.setRobotStartAvenue(1);
         world.setRobotStartStreet(1);
         world.setRobotStartDirection("E");

         world.addEWWall(1, 1, 1);
         world.addNSWall(1, 2, Y - 1);
         
         for (var col = 2; col <= X; col++) {
            for (var row = 2; row <= Y; row++) {
               world.putBalls(col, row, 4);
            }
         }
         
         var robot = new Robot();
         
         var code = ["from karel import *",
                     "# Complete the program",
                     ""];
    
         return {robot:robot, world:world, code:code};
      },
    
      isSuccess: function(robot, world) {
         return world.getBalls(1, 1) == 24 &&
            robot.getAvenue() == 1 &&
            robot.getStreet() == 1;
      },
   }

.. reveal:: Karel_for_fetch_24_from_matrix_reveal
   :showtitle: Solution
   :hidetitle: Hide solution

   .. activecode:: Karel_for_fetch_24_from_matrix_solution
      :passivecode: true
      
      from karel import *
      for i_column in range(2):   # repeat emptying one column four times
          move()                      # enter the next column
          turn_left()                 # turn north
          for i_row in range(3):      # go to the top edge, picking the balls along
              move()                   
              for i_ball in range(4): 
                  pick_ball()                  

          turn_right(); turn_right()  # turn south
          for i_row in range(3):      # go to the bottom edge
              move()                   

          turn_left()                 # turn east

      turn_left()                 # turn west
      turn_left()                           
      for i_column in range(2):   # come back to the starting square
          move()

      for i_ball in range(24):    # drop all the balls
          drop_ball()


Изкачване и слизане
'''''''''''''''''''

.. questionnote::

  Карел трябва да се изкачи по първия стълб, след това да слезе по останалите и да завърши в долния десен ъгъл.

Сега имаме нужда от два цикъла един след друг. В първия Карел трябва да се изкачи до първото стълбище и да слезе по второто стълбище във втория. Във всеки Karel трябва да извърши 4 действия, които представляват една стъпка нагоре или надолу по стълбите.

.. karel:: Karel_for_stairs_constant
   :blockly:

   {
      setup:function() {

         var Y = 4;
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
                     "turn_left()                  # northwards",
                     "for i_stair in range(3):         # repeat 3 times",
                     "    # tell Karel to climb up one stair",
                     "",
                     "turn_right(); turn_right()   # southwards",
                     "",
                     "# tell Karel to go down the stairs",
                     ""];
    
         return {robot:robot, world:world, code:code};
      },
    
      isSuccess: function(robot, world) {
         return robot.getAvenue() == world.getAvenues() &&
            robot.getStreet() == 1;
      },
   }

.. reveal:: Karel_for_stairs_constant_reveal
   :showtitle: Solution
   :hidetitle: Hide solution

   .. activecode:: Karel_for_stairs_constant_solution
      :passivecode: true
      
      from karel import *
      turn_left()                # northwards
      for i_stair in range(3):   # repeat 3 times
          move(); turn_right()       # climb up one stair
          move(); turn_left() 

      turn_right(); turn_right() # southwards
      
      for i_stair in range(3):   # repeat 3 times
          move(); turn_left()        # go one stair down
          move(); turn_right() 

Съберете топките на стълбите
'''''''''''''''''''''''''''''''

.. questionnote::

  Карел трябва да завърши отново в долния десен ъгъл, а по пътя трябва да вземе всички топчета.

Добър начин за решаване на тази задача е да се започне от решението на предишната задача. Съвет: копирайте решението на предишната задача тук и след това поставете циклите за вземане на топките.

.. karel:: Karel_for_stairs_and_balls_constant
   :blockly:

   {
      setup:function() {

         var Y = 4;
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
         
         // Balls
         for (let y = 2; y <= Y; y++) {
            world.putBalls(y - 1, y, 3);
            world.putBalls(y, y, 4);
         }
         for (let y = 1; y < Y; y++) {
            world.putBalls(X - y, y, 2);
            world.putBalls(X + 1 - y, y, 3);
         }

         var robot = new Robot();
         
         var code = ["from karel import *",
                     "# write a program",
                     ""];
    
         return {robot:robot, world:world, code:code};
      },
    
      isSuccess: function(robot, world) {
         return robot.getBalls() == 36 &&
            robot.getAvenue() == world.getAvenues() &&
            robot.getStreet() == 1;
      },
   }

.. reveal:: Karel_for_stairs_and_balls_constant_reveal
   :showtitle: Solution
   :hidetitle: Hide solution

   .. activecode:: Karel_for_stairs_and_balls_constant_solution
      :passivecode: true
      
      from karel import *
      turn_left()                     # northwards
      for i_stair in range(3):        # repeat 3 times
          move(); turn_right()            # climb up one stair
          for i_ball in range(3):
              pick_ball()
          move(); turn_left() 
          for i_ball in range(4):
              pick_ball()

      turn_right(); turn_right()      # southwards
      
      for i_stair in range(3):        # repeat 3 times
          move(); turn_left()             # go one stair down
          for i_ball in range(2):
              pick_ball()
          move(); turn_right() 
          for i_ball in range(3):
              pick_ball()
