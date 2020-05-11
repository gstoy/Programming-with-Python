Управление на Карел
===================

.. infonote::

    За да видите как изглежда програмирането, ще ви представим Karel. Karel е анимиран робот, който се движи по таблица, подобна на лабиринт, като следва нашите инструкции под формата на програма. Чрез управлението на Karel ние ще възприемем логика, която е много важна за писането на всяка програма, а също така можем да се забавляваме по пътя.

Идеята за изучаване на програмиране чрез управление на робот датира от 70-те години на миналия век, когато Ричард Е. Патис, като аспирант в Станфордския университет, създава първата такава среда с език за програмиране, специално създаден за тази цел. Езикът, подобно на робота, е кръстен Карел, на името на Карел Чапек, чешкият писател, който пръв започва да използва думата робот. Книгата на Патис Карел, Роботът: Въведение в изкуството на програмирането, е публикувана през 1981 г. и бързо се превръща в най-продаваната уводна книга в курсовете по програмиране. 
    
За да управляваме Karel можем да използваме следните функции:

- ``move()`` - преместване с един квадрат напред,
- ``turn_left()`` - завийте 90 градуса наляво (обратно на часовниковата стрелка),
- ``turn_right()`` - завийте 90 градуса надясно (по посока на часовниковата стрелка),
- ``pick_ball()`` - вземете топка от полето, на което се намирате,
- ``drop_ball()`` - пуснете топка върху полето, на което се намирате.

Използвайки тези пет функции, ние заявяваме какво искаме да направи Karel, така че ще ги наречем „команди за Karel“ или „оператори“. Карел разбира още пет различни функции, които ще видим скоро. В допълнение към тези команди, директно адресирани до Karel, можем да използваме и всички команди на езика за програмиране Python, които ще научим по време на курса.

Нека да разгледаме примерите как гореспоменатите команди могат да се използват за насочване на Карел през неговия свят:

Примери
--------

Преместете се с един квадрат напред и вземете топката
''''''''''''''''''''''''''''''''''''''''''''''''''''''

.. questionnote::

    Напишете програма, за да преместите Карел на поле (2, 1) и да го накарате да вземе топката.

Тази програма се състои само от две команди. Първата казва на Карел да се  придвижи едно поле напред, а другата да вземе топката.
   
.. karel:: Karel_intro_two_squares_one_ball
   :blockly:

   {
        setup:function() {
            var world = new World(2, 1);
            world.setRobotStartAvenue(1);
            world.setRobotStartStreet(1);
            world.setRobotStartDirection("E");
            world.putBall(2, 1);

        var robot = new Robot();

        var code = ["from karel import *",
                    "move()",
                    "pick_ball()"];
            return {robot:robot, world:world, code:code};
        },
    
        isSuccess: function(robot, world) {
           return robot.getBalls() === 1;
        },
   }

**Including** *karel* **library**
'''''''''''''''''''''''''''''''''

.. infonote::

    Функциите, които използваме за управление на Karel, са дефинирани в библиотеката karel. Следователно в началото на всяка програма трябва да кажем на компютъра (по-точно програмата, който изпълнява нашата програма) първо да прикачи определенията на тези функции за управление на Karel. Това се постига чрез първия ред на програмата: *from karel import*. Всяка програма, занимаваща се с Karel, която пишем, трябва да започва по този начин.
   
    Имайте предвид, че засега библиотеката на karel може да се използва в тази среда. Можете да стартирате другите си програми по други начини, но ние ще ви напомним за това, когато дойде времето.

На едно поле може да има повече от една топка и нашата задача може да е да кажем на Карел да вземе няколко или всичките.

Движение с едно поле напред и събиране на три топки
'''''''''''''''''''''''''''''''''''''''''''''''''''

.. questionnote::

    Напишете програма, която казва на Карел да се премести на поле (2, 1) и да вземе три от петте топки, които са там.
    
В тази програма след командата move (), командата pick_ball () трябва да бъде написана три пъти, за да вземе Карел 3 топки. Обърнете внимание на номера, който се появява на топката. Показва колко топки има на това поле. В допълнение към това, числото вляво от главата на Карел (което може би сте забелязали и в предишния пример) показва колко топки има Карел с него.
   
.. karel:: Karel_intro_two_squares_five_balls
   :blockly:

   {
        setup:function() {
            var world = new World(2, 1);
            world.setRobotStartAvenue(1);
            world.setRobotStartStreet(1);
            world.setRobotStartDirection("E");
            world.putBalls(2, 1, 5);

        var robot = new Robot();

        var code = ["from karel import *",
                    "move()",
                    "pick_ball()",
                    "pick_ball()",
                    "pick_ball()"];
            return {robot:robot, world:world, code:code};
        },
    
        isSuccess: function(robot, world) {
           return robot.getBalls() === 3;
        },
   }
   

Следващата задача е подобна, но малко по-трудна.
   
Стигнете до топката и я вземете
'''''''''''''''''''''''''''''''

.. questionnote::

   Напишете програма, която казва на Карел да дойде на поле (4, 1) и да вземе топката.

Задачата по същество не се различава от предишната. Все още е необходимо да изведете Карел на целевия площад и да му кажете да вземе топката. Разликата е, че сега пътят до целевия квадрат е по-дълъг и такава е нашата програма:

.. karel:: Karel_intro_take_ball_on_square_4_1
   :blockly:

   {
        setup:function() {
            var world = new World(5,5);
            world.setRobotStartAvenue(1);
            world.setRobotStartStreet(1);
            world.setRobotStartDirection("E");
            world.putBall(4, 1);
            world.addEWWall(1, 1, 2);
            world.addNSWall(2, 2, 2);
            world.addEWWall(2, 3, 3);
            world.addNSWall(3, 1, 2);
            world.addNSWall(3, 4, 1);
            world.addNSWall(1, 5, 1);
            world.addEWWall(4, 1, 1);
            
        var robot = new Robot();

        var code = ["from karel import *",
                    "move()       # go to (2, 1)",
                    "move()       # go to (3, 1)",
                    "turn_left()  # turn north (^)",
                    "move()       # go to (3, 2)",
                    "move()       # go to (3, 3)",
                    "turn_right() # turn east (>)",
                    "move()       # go to (4, 3)",
                    "move()       # go to (5, 3)",
                    "turn_right() # turn south (v)",
                    "move()       # go to (5, 2)",
                    "move()       # go to (5, 1)",
                    "turn_right() # turn west (<)",
                    "move()       # go to (4, 1)",
                    "pick_ball()  # take the ball at (4, 1)"];
            return {robot:robot, world:world, code:code};
        },
    
        isSuccess: function(robot, world) {
           return robot.getBalls() === 1;
        },
   }

Четейки тази програма, става трудно да следвате коя команда води Карел до кoe поле. Това не е така само за начинаещи, за всеки е трудно, защото всяко move () изглежда едно и също. За да си помогнем след всяка команда добавихме знака # и текст, който ни помага да следваме до къде сме довели Карел.

**Коментари**
'''''''''''''

.. infonote::

    Частта от всяка програма на Python от символа # до края на реда се нарича коментар(comment). Коментарите не засягат изпълнението на програмата, програмата прави същото със или без тях. Коментарите са предназначени само за хора, които четат и пишат програми, за да им помогнат да разберат по-добре тези програми и да се справят по-лесно с тях.
    
    Когато обмисляме да пишем коментари в нашите програми, трябва да ги пишем както за себе си, така и за други хора, които ще четат нашите програми. От друга страна, коментарите, които другите хора пишат в своите програми, ще ни помогнат да разберем техните програми.
    
    Няма точни правила за писане на коментари. В коментарите си трябва да запишете всичко, за което вярвате, че помага на другите (и на себе си) да разберат по-добре вашата програма.
   
Вземете всички топчета
''''''''''''''''''''''

В този пример топките са на различни полета и трябва да докараме Карел до всяка от тези топки.

.. questionnote::

   Напишете програма, за да кажете на Карел да вземе всичките четири топки.

Можем да изберем пътя за Карел по много начини, но колкото по-кратък е пътят, който избираме, толкова по-къса (и по-бърза) ще бъде нашата програма. Така че, например, първо можем да вземем топката на поле (5, 2), след това двете топчета при (5, 5) и накрая топката при (4, 4)

.. karel:: Karel_intro_collect_three_balls
   :blockly:

   {
        setup:function() {
            var world = new World(5,5);
            world.setRobotStartAvenue(1);
            world.setRobotStartStreet(1);
            world.setRobotStartDirection("E");
            world.putBall(5, 2);
            world.putBalls(5, 5, 2);
            world.putBall(4, 4);
            world.addEWWall(1, 1, 2);
            world.addNSWall(2, 2, 2);
            world.addEWWall(2, 3, 3);
            world.addNSWall(3, 1, 2);
            world.addNSWall(3, 4, 1);
            world.addNSWall(1, 5, 1);
            world.addEWWall(4, 1, 1);
            
        var robot = new Robot();

        var code = ["from karel import *",
                    "move(); move(); turn_left()  # go to square (3, 1) and turn north",
                    "move(); move(); turn_right() # go to square (3, 3) and turn east",
                    "move(); move(); turn_right() # go to square (5, 3) and turn south",
                    "move(); pick_ball()          # come to square (5, 2) and take the ball",
                    "turn_left(); turn_left()     # turn north",
                    "move(); move(); move()       # come to square (5, 5)",
                    "pick_ball(); pick_ball()     # take two balls",
                    "turn_left(); move();         # go to square (4, 5)",
                    "turn_left(); move();         # go to square (4, 4)",
                    "pick_ball()                  # take the last ball at (4, 4)"];
            return {robot:robot, world:world, code:code};
        },
    
        isSuccess: function(robot, world) {
           return robot.getBalls() === 4;
        },
   }

**Групиране на команди**
''''''''''''''''''''''''

Тъй като тази програма е дори по-дълга от предишната, за да улесним навигацията в програмата и да проследим позицията на Карел, направихме групи команди, които съставляват един етап от пътуването и поставихме всяка група в един ред от програма. В края на всеки ред има коментар, който обяснява групата команди в този ред.

Обърнете внимание, че когато пишете програма по този начин, знакът ; между командите трябва да присъства.

Командите могат да бъдат групирани по различен начин, например чрез разделяне на група от команди (написани една под друга) от следващата група в празен ред. Този метод за групиране се използва много по-често, тъй като командите обикновено не са толкова кратки, колкото контролите на Karel. Ето как би изглеждало:

.. code::

    from karel import *
    
    # go to square (3, 1) and turn north"
    move()
    move()
    turn_left()
    
    # go to square (3, 3) and turn east
    move()
    move()
    turn_right()
    
    # go to square (5, 3) and turn south
    move()
    move()
    turn_right()
    
    # come to square (5, 2) and take the ball
    move()
    pick_ball()
    
    # turn north
    turn_left()
    turn_left()
    
    # come to square (5, 5)
    move()
    move()
    move()
    
    # take two balls
    pick_ball()
    pick_ball()
    
    # go to square (4, 4)
    turn_left()
    move()
    turn_left()
    move()
    
    # take the last ball at (4, 4)
    pick_ball()
    
~~~~

Карел също може да поставя топчета в полетата. Ето как го прави.

Преместете топката
''''''''''''''''''

.. questionnote::

   Напишете програма, която кара Карел да премести топката на поле (2, 2) (обърнете внимание, че в началото Карел не е ориентиран правилно).
   

.. karel:: Karel_intro_move_ball_in_2x2
   :blockly:

   {
        setup:function() {
            var world = new World(2, 2);
            world.setRobotStartAvenue(1);
            world.setRobotStartStreet(1);
            world.setRobotStartDirection("S");
            world.putBall(2, 1);
            world.addEWWall(2, 1, 1);

        var robot = new Robot();

        var code = ["from karel import *",
                    "turn_left(); move(); pick_ball();  # take the ball at (2, 1)",
                    "turn_right(); turn_right(); move() # go back to (1, 1)",
                    "turn_right(); move()               # go to (1, 2)",
                    "turn_right(); move()               # go to (2, 2)",
                    "drop_ball()                        # place the ball at (2, 2)"];
            return {robot:robot, world:world, code:code};
        },
    
        isSuccess: function(robot, world) {
           return world.getBalls(2, 2) === 1;
        },
   }

**Грешки в изпълнението**
'''''''''''''''''''''''''

.. infonote::

    Моля, обърнете внимание, че Karel не може да изпълни всякаква команда по всяко време. По-специално, Карел не може да продължи напред, ако е пред стена, не може да вземе топка, където няма топка, и не може да играе топка, ако няма топки със себе си.
    
    Опитайте да изтриете първата команда turn_left () в предишната програма и след това стартирайте програмата, за да видите какво ще се случи.
    
    Когато програмата, изпълняваща нашата програма, стигне до команда, която не може да бъде изпълнена, изпълнението на програмата ни се прекъсва и получаваме съобщение за грешка. Такива съобщения са нормални и ще ги виждаме винаги, когато Карел не е в състояние да направи това, което му казваме или когато изказването ни не е ясно (по-точно, когато не е написано правилно). В такива ситуации трябва да се опитаме да разберем какъв е проблемът, да го решим и рестартираме програмата.
    
По-долу са някои задачи за самоубочение. Всяка задача идва с решение, което можете да видите, като кликнете върху бутона „solution“. Можете да копирате показаното решение във вашата работна зона и да го тествате, като стартирате програмата. Обърнете внимание, че вашето решение може да е различно от нашето и все пак да бъде доста добро.

Задачи за упражнение
--------------------

Ела на поле (3, 3)
'''''''''''''''''''''

.. questionnote::

   В тази задача няма топки, просто oтведете Карел на поле (3, 3).
   
.. karel:: Karel_intro_task_go_to_3_3
   :blockly:

   {
        setup:function() {
            var world = new World(3, 3);
            world.setRobotStartAvenue(1);
            world.setRobotStartStreet(1);
            world.setRobotStartDirection("N");
            world.addNSWall(1, 1, 2);
            world.addNSWall(2, 2, 2);

        var robot = new Robot();

        var code = ["from karel import *",
                    "# Add missing commands"];
            return {robot:robot, world:world, code:code};
        },
    
        isSuccess: function(robot, world) {
           return robot.getStreet() === 3 &&
           robot.getAvenue() === 3;
        },
   }
   
.. reveal:: Karel_intro_task_go_to_3_3_reveal
   :showtitle: Solution
   :hidetitle: Hide solution

   .. activecode:: Karel_intro_task_go_to_3_3_solution
      :passivecode: true
      
      from karel import *
      move(); move()               # to square (1, 3)
      turn_right(); move()         # to square (2, 3)
      turn_right(); move(); move() # to square (2, 1)
      turn_left(); move()          # to square (3, 1)
      turn_left(); move(); move()  # to square (3, 3)

Вземете топките
'''''''''''''''''

.. questionnote::

   Напишете програма, за да вземе Карел топките.
   
.. karel:: Karel_intro_task_collect_balls_in_2x2
   :blockly:

   {
        setup:function() {
            var world = new World(2, 2);
            world.setRobotStartAvenue(1);
            world.setRobotStartStreet(1);
            world.setRobotStartDirection("E");
            world.putBall(2, 1);
            world.putBall(2, 2);
            world.putBall(1, 2);
            world.addEWWall(2, 1, 1);

        var robot = new Robot();

        var code = ["from karel import *",
                    "# Add missing commands",
                    "pick_ball()"];
            return {robot:robot, world:world, code:code};
        },
    
        isSuccess: function(robot, world) {
           return robot.getBalls() === 3;
        },
   }
   
.. reveal:: Karel_intro_task_collect_balls_in_2x2_reveal
   :showtitle: Solution
   :hidetitle: Hide solution
  
   .. activecode:: Karel_intro_task_collect_balls_in_2x2_solution
      :passivecode: true
       
      from karel import *
      move(); pick_ball()                 # take the ball at square (2, 1)
      turn_right(); turn_right(); move()  # go back to square (1, 1)
      turn_right(); move(); pick_ball()   # pick the ball at square (1, 2)
      turn_right(); move(); pick_ball()   # pick the ball at square (2, 2)

Зиг-заг
'''''''

.. questionnote::

  Карел трябва да стигне до поле(5, 1).

.. karel:: Karel_intro_task_stairs_fixed
   :blockly:

   {
      setup:function() {

         var Y = 3;
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
                     "# Add missing commands ",
                     ""];
    
         return {robot:robot, world:world, code:code};
      },
    
      isSuccess: function(robot, world) {
         return robot.getAvenue() == world.getAvenues() &&
            robot.getStreet() == 1;
      },
   }

.. reveal:: Karel_intro_task_stairs_fixed_reveal
   :showtitle: Solution
   :hidetitle: Hide solution

   .. activecode:: Karel_intro_task_stairs_fixed_solution
      :passivecode: true
      
      from karel import *
      turn_left(); move()     # to (1, 2)
      turn_right(); move()    # to (2, 2)
      turn_left(); move()     # to (2, 3)
      turn_right(); move()    # to (3, 3)
      turn_right(); move()    # to (3, 2)
      turn_left(); move()     # to (4, 2)
      turn_right(); move()    # to (4, 1)
      turn_left(); move()     # to (5, 1)


Напред, след това наляво и после пак
''''''''''''''''''''''''''''''''''''

.. questionnote::

  Карел трябва да стигне до поле(2, 3).
   

.. karel:: Karel_intro_task_spiral_left_fixed
   :blockly:

   {
      setup:function() {

         var N = 4;
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
                     "# Add missing commands",
                     ""];
      
         return {robot:robot, world:world, code:code};
      },
 
      isSuccess: function(robot, world) {
         var N = world.getAvenues();
         return robot.getStreet() === Math.floor((N+2)/2) &&
           robot.getAvenue() === Math.floor((N+1)/2);
      },
   }

.. reveal:: Karel_intro_task_spiral_left_fixed_reveal
   :showtitle: Solution
   :hidetitle: Hide solution

   .. activecode:: Karel_intro_task_spiral_left_fixed_solution
      :passivecode: true
      
      from karel import *
      move(); move(); move(); turn_left() # to (4, 1)
      move(); move(); move(); turn_left() # to (4, 4)
      move(); move(); move(); turn_left() # to (1, 4)
      move(); move(); turn_left()         # to (1, 2)
      move(); move(); turn_left()         # to (3, 2)
      move(); turn_left()                 # to (3, 3)
      move();                             # to (2, 3)
