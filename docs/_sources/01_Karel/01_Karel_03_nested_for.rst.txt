Нека съкратим още програмите
============================

Да се върнем към последната програма от предишния урок. Карел трябваше да вземе по пет топки от всеки от трите квадрати в него.

.. image:: ../../_images/Karel/nested_for_3x5.png
    :width: 300px
    :align: center

Програмата, която решава задачата, може да изглежда така:

.. activecode:: Karel_nested_for__intro_1
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
        
Виждаме, че в тази програма следната група оператори се повтаря три пъти:

.. activecode:: Karel_nested_for__intro_2
   :passivecode: true

    move()
    for i in range(5):
        pick_ball()

Това ни позволява да съкратим програмата допълнително. В обясняването на оператора за изказване споменахме, че в тялото на цикъла могат да се намерят други цикли. Сега имаме възможност да го използваме.

Nested *for* цикли
------------------

Когато в тялото на един цикъл има втори цикъл, тогава първият цикъл се нарича външен цикъл, а другият се нарича вътрешен цикъл. Заедно ги наричаме вложени или вмъкнати цикли. В следващия пример ще видим как се пишат вложени for цикли.

Вземете пет топки три пъти
''''''''''''''''''''''''''''''

.. questionnote::

  Пред Карел има три полета, а на всеки от тях има 5 топки. Карел трябва да вземе всичките топки.

Задачата се повтаря, но сега ще я решим по различен начин.

.. infonote::
    Споменахме, че i в предходните примери служи брояч на повторения. Сега за първи път трябва да броим други неща (топки) по време на броенето на едно нещо (полета). Това означава например, че ще трябва да знаем точно кога сме на третото поле, като вземем втората топка. Следователно не можем да използваме едно и също име и за двата брояча, затова сме въвели нови имена за броячи вместо предишните i. В следната програма наричаме брояча на полетата  i_square, а името на брояча на топката е i_ball.
   
.. karel:: Karel_for_TakeMxN
   :blockly:

   {
        setup:function() {
           var numAvenues = 4;
           var numBalls = 5;
           var world = new World(numAvenues, 1);
           world.setRobotStartAvenue(1);
           world.setRobotStartStreet(1);
           world.setRobotStartDirection("E");
           
           for (var k = 2; k <= numAvenues; k++)
              world.putBalls(k, 1, numBalls);
           
           var robot = new Robot();

           var code = ["from karel import *",
                       "for i_square in range(3):",
                       "    move()",
                       "    for i_ball in range(5):",
                       "        pick_ball()",
                       ""];
           return {robot:robot, world:world, code:code};
        },
    
        isSuccess: function(robot, world) {
           return robot.getBalls() == 15; // 3 x 5 balls
        },
   }

В даденото решение, операторът pick_ball () е допълнително отразен, тъй като се изпълнява такива за всеки i_ball от диапазона [0, 1, 2, 3, 4]. В допълнение, целия statement за i_ball в диапазон (5): (заедно с неговото тяло и оператора се движат () над него), се повтаря 3 пъти, по един за всеки i_square от обхвата [0, 1, 2]. Това означава, че командата pick_ball () изпълнява общо 3 х 5 = 15 пъти (на всеки от трите полета пет пъти).
.. infonote::
С вложени цикли е необходимо да се обърне допълнително внимание на правилното отстъпване на операторите, защото става малко по-сложно. Неправилното отстъпване на някои команди може да доведе до грешен резултат или до програма, която изобщо не работи.   

Задачи за упражнения
--------------------

Skip
''''

.. questionnote::

  Пред Карел има по една топка на всяко трето поле и Карел трябва да ги вземе и двете.
  
Карел трябва да повтори група действия „Движете се три пъти и след това вземете топката“ 2 пъти.

.. karel:: Karel_for_every_nth_square
    :blockly:

    {
        setup:function() {
            var everyNth = 3;
            var numRepetitions = 2;
            var numBalls = 1;
            var numAvenues = 1 + numRepetitions * everyNth;
            var world = new World(numAvenues, 1);
            world.setRobotStartAvenue(1);
            world.setRobotStartStreet(1);
            world.setRobotStartDirection("E");
           
            for (var k = 1; k <= numRepetitions; k++)
                world.putBalls(1+k*everyNth, 1, numBalls);
            
            var robot = new Robot();
         
            var code = ["from karel import *",
                        "for i_rep in range(2):  # repeat twice everything that follows",
                        "    # use for statement to tell Karel to go 3 squares forward",
                        "    pick_ball()             # take the ball",
                        ""];
    
            return {robot:robot, world:world, code:code};
        },
    
        isSuccess: function(robot, world) {
            return robot.getBalls() == 2; // number of repetitions
        },
    }

.. commented out
   .. reveal:: Karel_for_every_nth_square_reveal
       :showtitle: Решење
       :hidetitle: Сакриј решење
   
       .. activecode:: Karel_for_every_nth_square_solution
           :passivecode: true
         
           from karel import *
           for i_pon in range(2):     # repeat twice everything that follows
               for i_polje in range(3):   # go 3 squares forward
                   move()
               pick_ball()            # take the ball

5 топки на всяко трето поле
'''''''''''''''''''''''''''''

.. questionnote::

  На всяко трето поле пред Карел има пет топки и той трябва да събере всички.
  
Задачата е подобна на предишната, просто трябва да повторите вдигането на топката. Уверете се, че цикълът за вземане на топките е под цикъла за придвижване напред, а не в него.


.. karel:: Karel_for_every_nth_square_5
    :blockly:

    {
        setup:function() {
            var everyNth = 3;
            var numRepetitions = 2;
            var numBalls = 5;
            var numAvenues = 1 + numRepetitions * everyNth;
            var world = new World(numAvenues, 1);
            world.setRobotStartAvenue(1);
            world.setRobotStartStreet(1);
            world.setRobotStartDirection("E");
           
            for (var k = 1; k <= numRepetitions; k++)
                world.putBalls(1+k*everyNth, 1, numBalls);
            
            var robot = new Robot();
         
            var code = ["from karel import *",
                        "for i_rep in range(2):      # repeat twice everything that follows",
                        "    # use for statement to tell Karel to go 3 squares forward",
                        "    # use a new for statement to tell Karel to take 5 balls",
                        ""];
    
            return {robot:robot, world:world, code:code};
        },
    
        isSuccess: function(robot, world) {
            return robot.getBalls() == 10; // numRepetitions x numBalls
        },
    }

.. commented out
   .. reveal:: Karel_for_every_nth_square_5_reveal
       :showtitle: Решење
       :hidetitle: Сакриј решење
   
       .. activecode:: Karel_for_every_nth_square_5_solution
           :passivecode: true
         
           from karel import *
           for i_pon in range(2):     # repeat twice everything that follows
               for i_polje in range(3):   # go 3 squares forward
                   move()
               for i_loptica in range(5): # to take 5 balls
                   pick_ball()


Мини напред
'''''''''''

.. questionnote::

  Карл още веднъж трябва да вземе всички топки.
  
Външният цикъл трябва да бъде изпълнен 3 пъти, а в него Karel трябва да направи следното:

- Повторете два пъти двете действия: „движете се напред“ и „вземете топката“
- Завийте наляво

.. karel:: Karel_for_ring
    :blockly:

    {
        setup:function() {
            var w = [
               '███████',
               '█1.1.1█',
               '█.███.█',
               '█0.0█1█',
               '█████.█',
               '█E.1.1█',
               '███████'
            ];

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
                        "... # complete the program",
                        ""];
                     
            return {robot:robot, world:world, code:code};
        },
      
        isSuccess: function(robot, world) {
           return robot.getBalls() == 6;
        }
    }

.. reveal:: Karel_for_ring_reveal_1
    :showtitle: Hint
    :hidetitle: Hide hint

    We've made verbal instructions a little more similar to the program, try converting them into statements. If you still want to see the program itself, click the "Solution" button.
    
    .. activecode:: Karel_for_ring_solution_1
        :passivecode: true
      
        for each of the 3 sides:
            for each of the 2 squares:
                move forward
                pick the ball
            turn left

    .. reveal:: Karel_for_ring_reveal_2
       :showtitle: Solution
       :hidetitle: Hide solution
   
       .. activecode:: Karel_for_ring_solution_2
           :passivecode: true
         
           from karel import *
           for i_side in range(3):     # repeat three times everything that follows
               for i_square in range(2):     # two times do "move" and "pick ball"
                   move()
                   pick_ball()
               turn_left()                   # turn along the next side



Върви и вземи по 3 топки всеки път
'''''''''''''''''''''''''''''''''''

.. questionnote::

  Напишете програма, чрез която Карел ще вземе всичките 18 топки.
  
Тази задача се различава от предходната само в едно: сега вдигането на топките трябва да бъде в допълнителен цикъл. Това означава, че ще имаме три внедрени цикъла: един, който брои страните на лабиринта, един, който брои квадратите по едната страна, и трети, който брои топките на едно поле.

.. karel:: Karel_for_ring_3
    :blockly:

    {
        setup:function() {
            var w = [
               '███████',
               '█3.3.3█',
               '█.███.█',
               '█0.0█3█',
               '█████.█',
               '█E.3.3█',
               '███████'
            ];

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
                        "... # complete the program",
                        ""];
                     
            return {robot:robot, world:world, code:code};
        },
      
        isSuccess: function(robot, world) {
           return robot.getBalls() == 18;
        }
    }

.. reveal:: Karel_for_ring_3_reveal
    :showtitle: Hint
    :hidetitle: Hide hint

    Again, we give instructions which look like a program (this time without the program itself).
    
    .. activecode:: Karel_for_ring_3_solution
        :passivecode: true
      
        for each of the 3 sides:
            for each of the 2 squares:
                move forward
                for each of the 3 balls:
                    pick the ball
            turn left

.. commented out
   .. reveal:: Karel_for_ring_3_reveal
       :showtitle: Solution
       :hidetitle: Hide solution
   
       .. activecode:: Karel_for_ring_3_solution
           :passivecode: true
         
           from karel import *
           for i_side in range(3):     # three times repeat everything that follows
               for i_square in range(2):   # repeat twice "move forward" and "take 3 balls"
                   move()
                   for i_ball in range(3):
                       pick_ball()
               turn_left()             # turn along the next side
