Допълнителни инструкции към функция
===================================

Споменахме, че има няколко начина за писане на функции в Python и че функциите, които сме написали и използвали досега, имат най-простата форма. Такива функции са, например, движение (), turn_left (), turn_right (), pick_ball () и drop_ball () от библиотеката Karel, както и функциите back (), take_at_neighboring_square () и go_to_neighboring_nonempty_square (), което ние написахме сами. Всички тези функции изпълняват конкретна работа, винаги по един и същи начин.

Функциите могат да бъдат написани така, че при различни екзекуции не винаги вършат точно едно и също нещо, но изпълняват малко по-обща задача. Когато наричаме такива функции, им казваме точно как искаме те да си вършат задачата. Например функция, която ще премести Карел за определен брой квадратчета напред или назад, често може да бъде много полезна. За тази функция искаме да уточним заявката, когато я извикваме - колко квадрата трябва да се движи и от коя страна.

Функции с параметри
-------------------

.. infonote::
    Допълнителна информация, която даваме на функция, се записва между скобите след името на функцията в първия ред на нейното определение. Между скобите можем да посочим една стойност или няколко стойности, разделени със запетаи. Тези стойности се наричат аргументи или параметри на функция. Думите „аргументи“ и „параметри“ са синоними в програмирането и ще ги използваме еднакво.

.. activecode:: Karel_functions__function_with_args_def
    :passivecode: true

    def function_name(parameter1, ... parameterN):
        statement_1
        ...
        statement_k

Функцията, която движи Karel определен брой квадратчета напред или назад, може да бъде наречена go и може да има един цяло число параметър. Ако този параметър е положителен, Karel ще премести толкова много квадратчета напред, а ако е отрицателен, Karel ще върне съответно (противоположно) число квадратчета назад. Например, обаждането go (5) ще означава "отидете 5 квадрата напред", докато go (-2) ще означава "върнете 2 квадрата назад". Ето как можем да напишем такава функция:

.. activecode:: Karel_functions__function_go_def
    :passivecode: true

    def go(n):
        if n > 0:
            for i in range(n):
                move()
        else:
            turn_left();turn_left()
            for i in range(-n):
                move()
            turn_left();turn_left()
 
Тази функция може да опрости много програми, които трябва да кажат на Karel да се движи няколко пъти по един път в двете посоки. Ето един пример.

Извършване на определени премествания
'''''''''''''''''''''''''''''''''''''

.. questionnote::

    Karel е разположен на началния квадрат на пътека с достатъчна дължина и трябва да извършва следните измествания на топки:

    - 3 топки от квадрат 3 до квадрат 4
    - 4 топки от квадрат 5 до квадрат 1

При решаването на тази задача ще използваме описаната функция go. За да опростим допълнително решението, можем също да въведем функцията displace, която измества определения брой топки за определен брой квадратчета напред или назад. Това описание показва, че функцията displaceтрябва да има два аргумента.

За да направим по-ясна целта на всеки параметър, ще им дадем имена, които описват тяхната роля:

.. activecode:: Karel_functions__function_displace_def
    :passivecode: true

    def displace(num_balls, num_squares):
        for i in range(num_balls):
            pick_ball()
        go(num_squares)
        for i in range(num_balls):
            drop_ball()

Функцията displace използва предварително написаната функция go. Извикването на функция от друга функция като тази може да отиде в дълбочина, доколкото ни е необходимо. Важно е само всяка функция да бъде дефинирана преди да бъде извикана за изпълнение.

Сега, когато имаме на разположение тези две функции, решаването на стартовата задача е много лесно:

.. karel:: Karel_functions__displace_balls
    :blockly:

    {
        setup:function() {
            function random(n) {
                return Math.floor(n * Math.random());
        }
         
        var ww = [
            [
               '███████████',
               '█E.0.4.0.6█',
               '███████████'
            ],
            [
               '█████████████',
               '█E.1.3.0.4.0█',
               '█████████████'
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
                  world.setRobotStartDirection(c);
               }
               let d = w[wy].charCodeAt(wx);
               if (d >= 48 && d < 58) world.putBalls(x, y, d - 48);
            }
         }
         
            var robot = new Robot();
         
            var code = ["from karel import *",
                     "# replace each word 'pass' with an appropriate function body",
                     "",
                     "def go(n):",
                     "    pass",
                     "",
                     "def displace(num_balls, num_squares):",
                     "    pass",
                     "",
                     "go(2) # to square 3",
                     "displace(3, 1) # displace 3 balls one square forward",
                     "go(1) # to the square 5",
                     "displace(4, -4) # displace 4 balls 4 squares back",
                     ""];
                     
            return {robot:robot, world:world, code:code};
        },
      
        isSuccess: function(robot, world) {
            var X = world.getAvenues();
            if (X == 5) {var tagret_layout = [4,0,1,3,2]}
            if (X == 6) {var tagret_layout = [4,1,0,3,0,0]}
           
            for (let x = 1; x <= X; x++)
                if (world.getBalls(x, 1) != tagret_layout[x-1]) return false;
           
            if (robot.getBalls() > 0)
                return false;
                 
            return true;
        }
    }

Задачи за упражнения
--------------------

Вземете определен брой топки
''''''''''''''''''''''''''''

.. questionnote::
    Напишете функцията *take_up_to(n)*, която казва на Карел да вземе максимум n топки от квадрата, на който стои. По-точно, ако на площада има n или повече топки, Карел взема n от тях, а ако има по-малко топки, Карел взема колкото може.

    Карел, който е на първия квадрат, трябва да вземе до 4 топки от втория квадрат, след това до 2 топки от третия квадрат и до 3 топки от четвъртия квадрат, а след това да донесе всички събрани топки до първия квадрат. Разбира се, функцията take_up_to (n), написана в първата част на задачата, трябва да се използва за тази цел.

.. karel:: Karel_functions__take_balls_up_to
    :blockly:

    {
        setup:function() {
            function random(n) {
                return Math.floor(n * Math.random());
        }
         
        var ww = [
            [
               '███████████',
               '█E.3.4.1.2█',
               '███████████'
            ],
            [
               '█████████',
               '█E.2.5.3█',
               '█████████'
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
                  world.setRobotStartDirection(c);
               }
               let d = w[wy].charCodeAt(wx);
               if (d >= 48 && d < 58) world.putBalls(x, y, d - 48);
            }
         }
         
            var robot = new Robot();
         
            var code = ["from karel import *",
                     "def take_up_to(n):",
                     "    pass # write the function",
                     "",
                     "move(); take_up_to(4)",
                     "# complete collecting the balls as specified",
                     "",
                     "turn_left(); turn_left() # come back",
                     "# complete Karel's return to the starting square and the dropping of the balls",
                     ""];
                     
            // from karel import *
            // def take_up_to(n):
            //     for i in range(n):
            //         if is_ball_on_square():
            //             pick_ball()
            // 
            // move(); take_up_to(4)
            // move(); take_up_to(2)
            // move(); take_up_to(3)
            //
            // turn_left(); turn_left()
            // move();move();move()
            // while any_balls_with_karel():
            //     drop_ball()
                     
            return {robot:robot, world:world, code:code};
        },
      
        isSuccess: function(robot, world) {
            var X = world.getAvenues();
            if (X == 5) {var tagret_layout = [6,0,2,0,2]} // = 0,3,4,1,2 - *,4,2,3
            if (X == 4) {var tagret_layout = [7,0,3,0]}   // = 0,2,5,3   - *,4,2,3
           
            for (let x = 1; x <= X; x++)
                if (world.getBalls(x, 1) != tagret_layout[x-1]) return false;
           
            if (robot.getBalls() > 0)
                return false;
                 
            return true;
        }
    }
    

Шофиране според инструкциите
''''''''''''''''''''''''''''

.. questionnote::
    Дадени са функции *face_left_at_intersection()* и *go_left (n)*.
    
    - Функция *face_left_at_intersection()* позиционира Karel да се изправи срещу първата улица, на която се натъква от лявата страна. При изпълнението на тази функция Карел върви напред, докато не срещне площад, където може да отиде наляво, но всъщност не отива наляво, вместо това остава на кръстовището, обърнат наляво. Ако Карел може да отиде наляво преди повикването на функцията, той няма да се движи от неговия квадрат по време на изпълнението на тази функция, а ще се обърне само вляво;
    - Функцията *go_left(n)* премества Karel по един квадрат до n-та улица вляво. Ако Карел вече е на кръстопът, улицата вляво от него се отчита като първа;

    Напишете подобни функции, използвайки дадените функции като модел.
    
    Напишете програма, която (използвайки дадени и писмени функции) води Карел до третата улица вляво, след това втората отдясно, а в края, втората отляво. Карел трябва да стигне до края на тази улица и да вземе единствената топка на масата.
    
.. karel:: Karel_functions__travel_instructions_1
   :blockly:

   {
      setup:function() {
         function random(n) {
            return Math.floor(n * Math.random());
         }
         
         var ww = [
            [
               '█████████████',
               '█0.0.0█0█1█0█',
               '█████.█.█.█.█',
               '█0.0█0.0.0.0█',
               '███.█.███████',
               '█0█0█0.0.0.0█',
               '█.█.█.█████.█',
               '█E.0.0.0.0.0█',
               '█████████████'
            ],
            [
               '███████████████',
               '█0.0.0.0.0.0█1█',
               '███████.█████.█',
               '█0.0.0.0.0.0█0█',
               '███████.███.█.█',
               '█0.0█0.0.0.0.0█',
               '███.███.███████',
               '█0█0█0.0.0.0█0█',
               '█.█.███.█████.█',
               '█E.0.0.0.0.0.0█',
               '███████████████'
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
                     "def face_left_at_intersection():",
                     "    turn_left()",
                     "    while not front_is_clear():",
                     "        turn_right()",
                     "        move()",
                     "        turn_left()",
                     "    ",
                     "def go_left(n):",
                     "    for i in range(n-1):",
                     "        face_left_at_intersection()",
                     "        turn_right()",
                     "        move()",
                     "    face_left_at_intersection()",
                     "    move()",
                     "",
                     "def face_right_at_intersection():",
                     "    # ...",
                     "    ",
                     "def go_right(n):",
                     "    # ...",
                     "",
                     
                     "go_left(3) # third street to the left",
                     "# second to the right",
                     "# second to the left",
                     "# go until end of the street",
                     "# take the ball",
                     ""];
                     
         //var code = ["from karel import *",
         //            "def face_left_at_intersection():",
         //            "    turn_left()",
         //            "    while not front_is_clear():",
         //            "        turn_right()",
         //            "        move()",
         //            "        turn_left()",
         //            "    ",
         //            "def go_left(n):",
         //            "    for i in range(n-1):",
         //            "        face_left_at_intersection()",
         //            "        turn_right()",
         //            "        move()",
         //            "    face_left_at_intersection()",
         //            "    move()",
         //            "",
         //            "def face_right_at_intersection():",
         //            "    turn_right()",
         //            "    while not front_is_clear():",
         //            "        turn_left()",
         //            "        move()",
         //            "        turn_right()",
         //            "    ",
         //            "def go_right(n):",
         //            "    for i in range(n-1):",
         //            "        face_right_at_intersection()",
         //            "        turn_left()",
         //            "        move()",
         //            "    face_right_at_intersection()",
         //            "    move()",
         //            "",
         //            
         //            "go_left(3)",
         //            "go_right(2)",
         //            "go_left(2)",
         //            "while front_is_clear():",
         //            "    move()",
         //            "if is_ball_on_square():",
         //            "    pick_ball()",
         //            ""];
                     
         return {robot:robot, world:world, code:code};
      },
      
      isSuccess: function(robot, world) {
         return robot.getBalls() > 0;
      }
   }
