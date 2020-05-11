Вижте и решете
==============

Операторът while се оказа много полезeн, защото с него успяхме да разрешим по-разнообразни задачи. Следващият пример обаче показва, че има прости задачи, които не можем да решим с наученото досега.

Нека да кажем, че в някаква ситуация трябва да преместите Карел само с едно поле, ако е възможно (ако не е възможно, Карел трябва да остане там, където е).

- Ако напишем само командата *move()* , рискуваме съобщение за грешка в случай, че Карел е пред стената.
- Ако поставим командата *move()* под оператора *while front_is_clear():* рискуваме Karel да отиде по-далеч, отколкото искаме.
- Ако не използваме командата *move()*, рискуваме да не се преместим, дори ако е възможно (и е необходимо).

Очевидно се нуждаем от нов оператор, който ще каже на Карел „ако можете да продължите напред, преместете едно място“.

Операторът *if* 
---------------

Твърдението, от което се нуждаем в описания случай, е операторът if, който също съществува в почти всички езици за програмиране. В Python той (в по-простата си форма) е написан така:

.. activecode:: Karel_if__syntax
   :passivecode: true

   if condition:
       statement_1
       ...
       statement_k


.. infonote::

   Виждаме, че писането на оператора if е много подобно на писането на oператора while. Под if можем да поставим и един или повече оператора, които съставляват тялото на оператора if. Същите правила се прилагат за писане на двоеточие: след условието и за изречения отстъпи, които се изпълняват, ако условието е изпълнено. Разликата е, че операторите, които съставят  if няма да се повторят - ако условието е изпълнено, те ще бъдат направени само веднъж.

   if понякога се нарича операция за разклоняване, защото изпълнението на програмата се разклонява при този елемент: следващият оператор, който трябва да бъде изпълнен, зависи от отговора на въпроса от условието.

В горния пример трябва да напишем:

.. activecode:: Karel_if__example
   :passivecode: true

   if front_is_clear():
       move()


Да видим някои задачи, в които (освен вече известните ни оператори) се използва операторът if.

Вземете една топка, ако има такава
''''''''''''''''''''''''''''''''''

.. questionnote::

   Има едно поле пред Карел, с нула или повече топки. Напишете програма, която казва на Карел да се придвижи на това поле и след това вземете точно една топка, ако има поне една топка в полето.
   
   Стартирайте програмата няколко пъти, за да я тествате на различни примери.

В нашия случай условието ще бъде is_ball_on_square(), а командата, която условно се изпълнява, е pick_ball().

.. karel:: Karel_if__take_one_if_any
   :blockly:

   {
      setup:function() {
          var world = new World(2, 1);
          world.setRobotStartAvenue(1);
          world.setRobotStartStreet(1);
          world.setRobotStartDirection("E");
          if (Math.random() > 0.5)
             world.putBalls(2, 1, 1 + Math.floor(7 *  Math.random()));
      
      var robot = new Robot();
      
      var code = ["from karel import *",
                  "move()",
                  "if ...         # complete the statement",
                  "    pick_ball()",
                  ""];
          return {robot:robot, world:world, code:code};
      },
      
      isSuccess: function(robot, world) {
         return world.getBalls(1, 1) === 0 &&
            (robot.getBalls() === 1 ||
            (robot.getBalls() === 0 && world.getBalls(2, 1) === 0));
      }
   }

.. commented out
   .. reveal:: Karel_if__take_one_if_any_reveal
       :showtitle: Solution
       :hidetitle: Hide solution
       
       Solution:
   
       .. activecode:: Karel_if__take_one_if_any_solution
           :passivecode: true
         
           from karel import *
           move()
           if is_ball_on_square():
               pick_ball()


Отидете до края на пътеката и изберете една топка, където е възможно
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

.. questionnote::

  Има поне един квадрат пред Карел и може да има произволен брой от тях. Всеки квадрат има нула или повече топки. Карел трябва да вземе точно една топка от всеки квадрат, на който има топка.
  
  Стартирайте програмата няколко пъти, за да я тествате на различни примери.

Тук е необходимо да се използва, операторът while за движение и като част от тялото на цикъл while, след всяка стъпка напред, трябва да се използва оператор if, за да се провери дали Карел стои на квадрат с топка или не.

.. karel:: Karel_if__many_squares_take_one_if_any
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
             if (Math.random() > 0.5)
                world.putBalls(k, 1, 2 + random(3)); // need initial world to replace '2'->'1'
      
         var robot = new Robot();
      
         var code = ["from karel import *",
                     "while front_is_clear():",
                     "    move()",
                     "    if ... # add the condition",
                     "       ... # add the conditional statement",
                     ""];
                     
         return {robot:robot, world:world, code:code};
      },
      
      isSuccess: function(robot, world) {
         var N = world.getAvenues();
         var nonEmpty = 0;
         for (var k = 1; k <= N; k++)
            if (world.getBalls(k, 1) > 0)
               nonEmpty++;
               
         return robot.getBalls() === nonEmpty;
      }
   }

.. commented out
   .. reveal:: Karel_if__many_squares_take_one_if_any_reveal
       :showtitle: Solution
       :hidetitle: Hide solution
       
       Solution:
   
       .. activecode:: Karel_if__many_squares_take_one_if_any_solution
           :passivecode: true
         
           from karel import *
           while front_is_clear():
               move()
               if is_ball_on_square():
                   pick_ball()


Ако не направите така, направете това (if-else)
-----------------------------------------------

При някои задачи трябва да се направи едно нещо, ако е изпълнено определено условие, а друго - ако не е изпълнено. В такъв случай можем да използваме разширената форма на оператор if, който изглежда така:

.. activecode:: Karel_if__else_syntax
    :passivecode: true

    if condition:
        statement_a1
        ...
        statement_ak
    else:
        statement_b1
        ...
        statement_bm


.. infonote::

   В разширената форма на if, първата част (преди else) има същия вид и значение като преди. Под тази част се изписва  else, насъщото място в реда, където бихме изписали if`, последвана от двоеточие:. В следващите редове пишем един или повече други оператори, които съставляват тялото на else. Тази втора група отоператори се изписва едно поле по-навътре от else и се изпълнява, ако условието, посочено в оператора if, не е изпълнено.

Пример - вземане и пускане на топки
'''''''''''''''''''''''''''''''''''

.. questionnote::

   Пред Карел има 3 квадрата и на всеки от тях може да има или една топка, или николко. Карел трябва да вземе топки от квадратите, на които има топки и да постави по една топка на всеки квадрат, който първоначално е бил празен. Карел има достатъчно топки с него в началото.

Използвайки новата, разширена форма на израза if, можем да кажем на Карел: „Ако има топка на квадрата, тогава вземете тази топка, иначе пуснете една топка“, така че задачата да бъде лесно разрешена:

.. karel:: Karel_if__take_else_put
    :blockly:
   
    {
      setup: function() {
       var world = new World(4, 1);
           world.setRobotStartAvenue(1);
           world.setRobotStartStreet(1);
           world.setRobotStartDirection("E");
       world.balls = [];
       for (var k = 2; k <= world.getAvenues(); k++) {
          var ball = Math.random() > 0.5;
          world.balls.push(ball);
          if (ball)
                  world.putBall(k, 1);
           }
           var robot = new Robot();
       robot.setInfiniteBalls(true);
       var code = ["from karel import *",
        "for i in range(3):",
        "    move()",
        "    if is_ball_on_square():",
        "        pick_ball()",
        "    else:",
        "        drop_ball()"
       ]
       return {world: world, robot: robot, code: code};
      },

      isSuccess: function(robot, world) {
       for (var k = 2; k <= world.getAvenues(); k++)
              if (world.getBalls(k, 1) == world.balls[k-2])
             return false;
       return true;
      }
    }


Вземете топките, до които можете да стигнете
''''''''''''''''''''''''''''''''''''''''''''


.. questionnote::

   Лабиринтът се състои от два реда. Карел е в горния ред, който е напълно празен и проходим. В долния ред може да има препятствия или квадратчета с една топка. Задачата на Карел е да вземе всички топки.

.. karel:: Karel_if__take_all_from_lower_row
    :blockly:
   
    {
      setup: function() {

         function random(n) {
             return Math.floor(n * Math.random());
         }

         var world = new World(4 + random(4), 2);
         world.setRobotStartAvenue(1);
         world.setRobotStartStreet(2);
         world.setRobotStartDirection("E");

         world.addEWWall(1, 1, 1);
         var balls = 0;
         var prevBall = false;
         for (var i = 2; i <= world.getAvenues(); i++) {
             if (random(2) == 0 || (balls == 0 && i == world.getAvenues() - 1)) {
                 balls++;
                 if (!prevBall)
                    world.addNSWall(i-1, 1, 1);
                 world.putBall(i, 1);
                 prevBall = true;
             } else {
                 if (prevBall)
                    world.addNSWall(i-1, 1, 1);
                 world.addEWWall(i, 1, 1);
                 prevBall = false;
             }
         }

         var robot = new Robot();
         var code = ["from karel import *",
            "while front_is_clear():",
            "    move() # next square in upper row",
            "",
            "    # check the lower row",
            "    turn_right()           # southwards",
            "    if front_is_clear():   # if there is a square in the lower row",
            "        # tell Karel to go get the ball, ",
            "        # to come back to the upper row and turn east",
            "    # tell Karel, if he could not go to the lower row,",
            "    # to turn back to east, to be able to continue properly",
         ]
         return {world: world, robot: robot, code: code};
      },

      isSuccess: function(robot, world) {
           for (var i = 1; i <= world.getAvenues(); i++)
              for (var j = 1; j <= world.getStreets(); j++)
                 if (world.getBalls(i, j) != 0)
                    return false;
          return true;
      }
    }
   
.. commented out
   .. reveal:: Karel_if__take_all_from_lower_row_reveal
       :showtitle: Show solution
       :hidetitle: Hide solution
   
       One possible solution (not the only one) is the following:
   
       .. activecode:: Karel_if__take_all_from_lower_row_solution
           :passivecode: true
                       
           from karel import *
           while front_is_clear():
               move() # next square
               
               # check the lower row
               turn_right()  # southwards
               if front_is_clear(): # if there is a square in the lower row
                   move(); pick_ball() # go get the ball
                   
                   # go back to the upper row, and turn east
                   turn_left(); turn_left()
                   move(); turn_right() 
               else:
                   turn_left() # just turn back east


Действайте само, когато нещо не е изпълнено
-------------------------------------------

Нека кажем, че Карел трябва да завие наляво, ако не може да продължи напред (ако може да продължи напред, не трябва да прави нищо).

Според правилата за писане на *if*, след условието (в тялото на първия branch) трябва да има поне един оператор, според логиката на задачата не се нуждаем от оператор на това място. В такива ситуации можем да пишем:

.. activecode:: Karel_if__else_only
    :passivecode: true

    if front_is_clear():
        pass
    else:
        turn_left()

или

.. activecode:: Karel_if__not
    :passivecode: true

    if not front_is_clear():
        turn_left()

В първия случай използваме pass, който не прави нищо. Правейки това, удовлетворяваме синтаксиса (правила за писане) и получаваме програма, която работи така, както искаме.

Във втория случай, използвайки думата not, правим обратното условие, което означава, че условието на  if е изпълнено, когато Karel не може да продължи напред. В този случай клоните променят ролите, така че else частта вече не е необходима.

В малкото предстоящи задачи има какво да се направи само когато условието не е изпълнено.

Обърнете се към празно поле
'''''''''''''''''''''''''''


.. questionnote::

   Първоначално Карел може да се изправи от двете страни, но може да започне да се движи само в една посока. Карел трябва да се обърне към свободния квадрат и да направи една стъпка.

.. karel:: Karel_if__turn_to_free_square
   :blockly:

   {
      setup:function() {
         function random(n) {
            return Math.floor(n * Math.random());
         }
         
         var ww = [
            [
               '█████',
               '█N.0█',
               '█████'
            ],
            [
               '█████',
               '█S.0█',
               '█████'
            ],
            [
               '█████',
               '█E.0█',
               '█████'
            ],
            [
               '█████',
               '█W.0█',
               '█████'
            ],
            [
               '███',
               '█0█',
               '█.█',
               '█E█',
               '███'
            ],
            [
               '███',
               '█0█',
               '█.█',
               '█W█',
               '███'
            ],
            [
               '███',
               '█0█',
               '█.█',
               '█S█',
               '███'
            ],
            [
               '███',
               '█0█',
               '█.█',
               '█N█',
               '███'
            ],
            [
               '███████',
               '█0.0.N█',
               '███████'
            ],
            [
               '███████',
               '█0.0.S█',
               '███████'
            ],
            [
               '███████',
               '█0.0.W█',
               '███████'
            ],
            [
               '███████',
               '█0.0.E█',
               '███████'
            ],
            [
               '█████',
               '█0█N█',
               '█.█.█',
               '█0.0█',
               '█████'
            ],
            [
               '█████',
               '█0█S█',
               '█.█.█',
               '█0.0█',
               '█████'
            ],
            [
               '█████',
               '█0█W█',
               '█.█.█',
               '█0.0█',
               '█████'
            ],
            [
               '█████',
               '█0█E█',
               '█.█.█',
               '█0.0█',
               '█████'
            ]
         ];
         let choice = random(ww.length);
         var w = ww[choice];
         var ny = Math.floor(w.length / 2);
         var nx = Math.floor(w[0].length / 2);
         var world = new World(nx, ny);
         
         for (let y = 1; y <= ny; y++) {
            let wy = 2*(ny-y) + 1;
            for (let x = 1; x <= nx; x++) {
               let wx = 2*x - 1;
               if (y < ny && w[wy - 1].charAt(wx) == "█") world.addEWWall(x, y, 1);
               if (x < nx && w[wy].charAt(wx + 1) == "█") world.addNSWall(x, y, 1);
               let c = w[wy].charAt(wx);
               let pos = "SWEN".indexOf(c);
               if (pos > -1) {
                  world.setRobotStartAvenue(x);
                  world.setRobotStartStreet(y);
                  world.setRobotStartDirection("SWEN".charAt(pos));
               }
               let d = w[wy].charCodeAt(wx);
               if (d >= 48 && d < 58) world.putBalls(x, y, d - 48);
            }
         }
         
         var robot = new Robot();
         
         var code = ["from karel import *",
                     "# write the program",
                     ""];
                     
         return {robot:robot, world:world, code:code};
      },
      
      isSuccess: function(robot, world) {
         var X = world.getAvenues();
         var Y = world.getStreets();
         if (X == 2 && Y == 1) return robot.getAvenue() == 2 && robot.getStreet() == 1 && robot.getDirection() == "E";
         if (X == 1 && Y == 2) return robot.getAvenue() == 1 && robot.getStreet() == 2 && robot.getDirection() == "N";
         if (X == 3 && Y == 1) return robot.getAvenue() == 2 && robot.getStreet() == 1 && robot.getDirection() == "W";
         if (X == 2 && Y == 2) return robot.getAvenue() == 2 && robot.getStreet() == 1 && robot.getDirection() == "S";
         return false;
      }
   }

.. reveal:: Karel_if__turn_to_free_square_reveal
    :showtitle: Solution
    :hidetitle: Hide solution

    We offer you two short solutions:
   
    .. activecode:: Karel_if__turn_to_free_square_solution1
        :passivecode: true
      
        from karel import *
        while not front_is_clear():
            turn_left()
        move()

    .. activecode:: Karel_if__turn_to_free_square_solution2
        :passivecode: true
      
        from karel import *
        for i in range(3):
            if not front_is_clear():
                turn_left()
        move()
                
Където няма топки, добавете ги
'''''''''''''''''''''''''''''''

.. questionnote::

   Пред Карел има неизвестен брой квадратчета и всеки от тях може да съдържа една топка или никакви топки. Карел има достатъчно топки със себе си и той трябва да сложи по една топка на всеки празен квадрат.

.. karel:: Karel_if__fill_the_empty_squares
    :blockly:
   
    {
        setup: function() {
            function random(n) {
                return Math.floor(n * Math.random());
            }
            var N = 2 + random(5);
            var world = new World(N, 1);
            world.setRobotStartAvenue(1);
            world.setRobotStartStreet(1);
            world.setRobotStartDirection("E");
            world.balls = [];
            world.putBall(1, 1);
            for (var k = 2; k <= world.getAvenues(); k++) {
                var ball = Math.random() > 0.5;
                world.balls.push(ball);
                if (ball)
                    world.putBall(k, 1);
            }
            var robot = new Robot();
            robot.setInfiniteBalls(true);
            var code = ["from karel import *",
                        "# write the program"
                        ]
            return {world: world, robot: robot, code: code};
        },

        isSuccess: function(robot, world) {
            for (var k = 1; k <= world.getAvenues(); k++)
                if (world.getBalls(k, 1) != 1)
                    return false;
            return true;
        }
    }
