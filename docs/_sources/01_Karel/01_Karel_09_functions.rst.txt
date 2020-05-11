Създайте серия от оператори
============================

Нека си припомним задачата Вземете топката на съседното поле. Задачата беше, че във всяка посока Карел трябваше да се опита да отиде до съседното поле и (ако можеше да отиде до съседния площад), за да опита да вземе топката там. За да улесним пробването на следващата посока, избрахме да връщаме Карел на началния квадрат след всеки опит.

Една програма, която решава тази задача, е:

.. activecode:: Karel_functions__take_neighboring_ball_1
    :passivecode: true

    from karel import *
    for i in range(4):   # in each of the 4 directions
        if front_is_clear(): # search the square in that direction
            move()
            if is_ball_on_square():
                pick_ball()
            turn_left()          # come back to the starting square
            turn_left()
            move()
            turn_left()          # turn towards the square you just tried
            turn_left()
        turn_left()          # next direction

TЧастта от програмата от седмия до единадесетия ред изглежда малко по-трудна за следване. В тази част може да се наложи да си представите какво ще направи Карел, за да разберете напълно какво се случва там.

Коментарите донякъде помагат за по-лесното разбиране на тази част от програмата. В допълнение към коментарите, ще бъде още по-добре, ако има функция back(), която ще премести Карел крачка назад. Тогава програмата ще бъде по-кратка и по-разбираема:

.. activecode:: Karel_functions__take_neighboring_ball_2
    :passivecode: true

    from karel import *
    for i in range(4):          # in each of the 4 directions
        if front_is_clear():       # seek a free square in that direction
            move()
            if is_ball_on_square():
                pick_ball()
            back()                     # come back to starting square
        turn_left()                # next direction
        
Функцията back () не е част от библиотеката на Karel, но много лесно можем сами да напишем тази функция. Когато приключите, ще можем да използваме функцията back () еднакво с другите функции на библиотеката Karel, като например move () или turn_right ().

Как се пишат функции
--------------------

Засега ще научим само най-простия начин за писане на функция в Python, а други, по-сложни форми ще видим по-късно.

.. activecode:: Karel_functions__function_def
    :passivecode: true

    def function_name():
        statement_1
        ...
        statement_k

.. infonote::
      
   WКогато пишете някоя функция в Python, думата def в началото, скобите () и двоеточие: в края на първия ред са задължителни. За име на функция можем да използваме всяко правилно написано име, което сме избрали. Следващите оператори се пишат по-навътре и те формират тялото на функцията (ако повече от една команда е написана на ред, тогава тези команди са разделени с точка и запетая;). Операторите във функционалното тяло ще се изпълняват всеки път, когато името на функцията се срещне при изпълнение на програмата, тоест когато се извиква тази функция.

В съответствие с тези правила, функцията back () може да бъде написана, както следва:

.. activecode:: Karel_functions__backwards_def
    :passivecode: true

    def back():
        turn_left(); turn_left()
        move()
        turn_left(); turn_left()

Тогава цялата програма ще изглежда така:
   
.. karel:: Karel_functions__take_neighboring_ball_final
   :blockly:

   {
      setup:function() {
         function random(n) {
            return Math.floor(n * Math.random());
         }
         
         var ww = [
            [
               '█████',
               '█0.0█',
               '███.█',
               '█1.N█',
               '███.█',
               '█0.0█',
               '█████'
            ],
            [
               '█████',
               '█1.0█',
               '█...█',
               '█E.0█',
               '█████'
            ],
            [
               '███████',
               '█0█0█0█',
               '█.█.█.█',
               '█0.W.0█',
               '█.█.█.█',
               '█0█1█0█',
               '███████'
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
                     "def back():",
                     "    turn_left(); turn_left()",
                     "    move()",
                     "    turn_left(); turn_left()",
                     "",    
                     "for i in range(4):",
                     "    if front_is_clear():",
                     "        move()",
                     "        if is_ball_on_square():",
                     "            pick_ball()",
                     "        back()",
                     "    turn_left()  # next direction",
                     ""];
                     
         return {robot:robot, world:world, code:code};
      },
      
      isSuccess: function(robot, world) {
         return robot.getBalls() > 0;
      }
   }

.. infonote::
    Когато извлечем някои оператори (които имат значение като група) във функция, можем да напишем програми, които са по-кратки и ясни, защото сме разделили проблема на по-малко сложни части.

    Друго предимство на функциите за писане е, че лесно можем да ги използваме в други програми (тук понякога ще копираме предварително написани функции, но в реалното програмиране има по-добър и по-прост начин за повторно използване на веднъж написани функции).


Излизане от функцията или цикъла преди края
-------------------------------------------

В задачата да търсим топката на съседно поле, в името на простотата на програмата, решихме, че дори когато Карел намери топка, той продължава да търси в останалите посоки. Има начин да се избегне това ненужно изпълнение на останалите оператори.

.. infonote::
    Когато искаме да прекъснем изпълнението на цикъла, пишем специален оператор break за прекъсване. Ефектът е да изскочите от цикъла и да продължите изпълнението на програмата от първия оператор след цикъла.

    Използвайки break, ще изскочим от най-близкия (най-тесен) for или while цикъл, съдържащ декларацията за почивка. Ако операторът за прекъсване е разположен в две или повече вложени цикли, изпълнението продължава с оператора, който следва най-вътрешния (най-тесен) цикъл.

Използвайки break, бихме могли да модифицираме основната част на програмата:

.. activecode:: Karel_functions__break_intro_1
    :passivecode: true

    for i in range(4):
        if front_is_clear():
            move()
            if is_ball_on_square():
                pick_ball()
            back()
        turn_left()  # next direction

във:

.. activecode:: Karel_functions__break_intro_2
    :passivecode: true

    for i in range(4):
        if front_is_clear():
            move()
            if is_ball_on_square():
                pick_ball()
                break
            back()
        turn_left()  # next direction

По този начин цикълът завършва веднага щом топката бъде намерена и взета. Тъй като няма други операции след този цикъл, в този случай чрез изпълнение на break, работата на програмата завършва.

~~~~

Подобно на излизането от цикъла, ние също можем да излезем от функцията, преди да се изпълнят всички нейни оператори.

.. infonote::
    Когато искаме да прекъснем изпълнението на функция, пишем специален оператор return. Ефектът на оператора return е да излезете от функцията и да продължите изпълнението на програмата от първият оператор след мястото, от което е извикана функцията. 

    С return излизаме от функцията, без значение колко цикъла има около оператора за връщане вътре във функцията.

Можем да превърнем програмата за вземане на топката от съседното поле във функция. В този случай можем да напишем:

.. activecode:: Karel_functions__return_intro
    :passivecode: true

    def take_at_neighboring_square():
        for i in range(4):
            if front_is_clear():
                move()
                if is_ball_on_square():
                    pick_ball()
                    return # exit the function
                back()
            turn_left()  # next direction
            
    take_at_neighboring_square()
    
Задачи за упражнение
--------------------

Оставяйте топките, докато има, както топки, така и квадратчета
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

.. questionnote::

    Първоначално Карел има няколко топки и трябва да ги подреди по пътеката по една за всяко поле (започвайки от това, на което стои), доколкото е възможно. Карел спира да поставя топки, когато удари препятствие или когато му свършат топките (каето се случи първо). Няма значение дали Карел ще спре на последния запълнен квадрат или на първия празен квадрат.

Съвет: Поставете едно от тези две условия в while цикъл, така цикълът приключва, когато условието вече не е изпълнено. Освен това, използвайте оператора break за излизане от цикъла, ако другото условие не е изпълнено.

.. karel:: Karel_functions__put_balls_until_wall_or_no_more_balls
   :blockly:

    {
        setup:function() {
            function random(n) {
                return Math.floor(n * Math.random());
            }
            var choice = random(3); // need initial world to get rid of 'choice'
            var N = [3, 4, 5];
            var world = new World(N[choice], 1);
            world.setRobotStartAvenue(1);
            world.setRobotStartStreet(1);
            world.setRobotStartDirection("E");
            
            var robot = new Robot();
            if (choice == 0) robot.setBalls(3);
            if (choice == 1) robot.setBalls(6);
            if (choice == 2) robot.setBalls(2);
           
            var code = ["from karel import *",
                        " # write the program",
                        ""];
                        
            //var code = ["from karel import *",
            //            "while any_balls_with_karel():",
            //            "    drop_ball()",
            //            "    if not front_is_clear():",
            //            "        break",
            //            "    move()",
            //            ""];
                        
            return {robot:robot, world:world, code:code};
        },
    
        isSuccess: function(robot, world) {
            var X = world.getAvenues();
            var zeroBallsFound = false;
            for (var x = 1; x <= X; x++) {
                var b = world.getBalls(x, 1);
                if (b > 1) return false;
                if (b == 1 && zeroBallsFound) return false;
                if (b == 0) zeroBallsFound = true;
            }
           
           if (robot.getBalls() > 0 && zeroBallsFound)
               return false;
                 
           return true;
        },
    }

Преместете всички топки един квадрат назад
''''''''''''''''''''''''''''''''''''''''''

.. questionnote::

    Пред Карел има пътека с неизвестна дължина. В стартовия квадрат няма топки. Карел трябва да измести всяка топка по един квадрат на запад.

Можете да разрешите тази задача, като повторите следните стъпки, стига да има квадратчета пред Карел:

- отидете на следващия квадрат
- вземете всички топчета от този квадрат
- отидете крачка назад (тоест, обърнете се и отидете една стъпка напред)
- пуснете всички топчета
- върнете се на квадрата, от който сте взели топките

По този начин можете да използвате написаната по-рано функцията, която разгледахме по-рано, за да се върнете към квадрата, към който Карел движи топките. Просто трябва да го копирате (или да го въведете отново) в областта за вашето решение.

.. karel:: Karel_functions__all_balls_one_square_back
   :blockly:

    {
        setup:function() {
           function random(n) {
              return Math.floor(n * Math.random());
           }
           var choice = random(3); // need initial world to get rid of 'choice'
           var N = [3, 4, 5];
           var world = new World(N[choice], 1);
           world.setRobotStartAvenue(1);
           world.setRobotStartStreet(1);
           world.setRobotStartDirection("E");
           
           var B = 0;
           if (Math.random() > 0.8) B = random(3);
           if (choice == 0) {
              world.putBalls(2, 1, B);
              world.putBalls(3, 1, B + 2);
           }
           if (choice == 1) {
              world.putBalls(2, 1, B);
              world.putBalls(3, 1, B + 3);
              world.putBalls(4, 1, B + 1);
           }
           if (choice == 2) {
              world.putBalls(2, 1, B);
              world.putBalls(3, 1, B + 2);
              world.putBalls(4, 1, B + 1);
              world.putBalls(5, 1, B + 0);
           }

           var robot = new Robot();

           var code = ["from karel import *",
                       "",
                       "# copy the function 'back()'",
                       "",
                       "while front_is_clear():  # while there are squares in fornt of Karel, repeat",
                       "    move();                  # go forward",
                       "    # complete the line      # pick up all the balls from this square",
                       "    # complete the line      # go one step back",
                       "    # complete the line      # drop all the balls",
                       "    # complete the line      # go forward once more to the emptied square",
                       ""];
                       
           return {robot:robot, world:world, code:code};
        },
    
        isSuccess: function(robot, world) {
           var N = world.getAvenues();
           var B = world.getBalls(1, 1);
           if (N == 3) {
              if (world.getBalls(2, 1) != B + 2)
                return false;              
           }
           if (N == 4) {
              if (world.getBalls(2, 1) != B + 3)
                return false;
              if (world.getBalls(3, 1) != B + 1)
                return false;              
           }
           if (N == 5) {
              if (world.getBalls(2, 1) != B + 2)
                return false;
              if (world.getBalls(3, 1) != B + 1)
                return false;
              if (world.getBalls(4, 1) != B + 0)
                return false;
           }
           
           if (world.getBalls(N, 1) != 0) 
              return false;

           if (robot.getBalls() > 0)
                 return false;
                 
           return true;
        },
    }
   
.. reveal:: Karel_functions__all_balls_one_square_back_reveal
    :showtitle: Solution
    :hidetitle: Hide solution

    .. activecode:: Karel_functions__all_balls_one_square_back_solution
        :passivecode: true
      
        from karel import *
        def back():      # go one step back, and maintain the same orientation
            turn_left(); turn_left();
            move(); 
            turn_left(); turn_left();

        while front_is_clear():       # while there are squares in fornt of Karel, repeat
            move();                       # go to a new square
            while is_ball_on_square():    # take all the balls from this square
                pick_ball()            
            back()                        # step back
            while any_balls_with_karel(): # drop all the balls
                drop_ball()
            move()                        # go to the emptied square


Следвайте топките
'''''''''''''''''

.. questionnote::

    Всеки квадрат съдържа една топка или нито една. Квадратите с топките върху тях образуват пътека, която започва на площада до Карел. Карел трябва да следва този път и да вземе всички топки.

Съвет: За да решите тази задача, можете да напишете функцията go_to_neighboring_nonempty_square (), която трябва само да премести Karell до съседния квадрат, който има топка върху него (return би бил полезен там). Функцията go_to_neighboring_nonempty_square () трябва да се различава от написаната по-рано функция take_at_neighboring_square () само в смисъл, че не взема топката.

Когато Карел събере всички топки, следващият призив на тази функция ще го постави на празен квадрат (между другото, това ще бъде квадратът, където Карел взе последната топка). Когато на площада, на който е Карел, няма топка, това ще означава, че Карел вече е взел всички топчета.

.. karel:: Karel_functions__follow_the_balls
   :blockly:

    {
        setup:function() {
            function random(n) {
                return Math.floor(n * Math.random());
            }
         
            var ww = [
                [
                   '███████████',
                   '█0.0.1.1.0█',
                   '█.........█',
                   '█0.N.0.1.0█',
                   '█.........█',
                   '█0.1.1.1.0█',
                   '███████████'
                ],
                [
                   '███████████',
                   '█1.1.1.1.1█',
                   '█.........█',
                   '█1.0.0.0.1█',
                   '██........█',
                   '█S.1.1.1.1█',
                   '███████████'
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
                        "def back():",
                        "    turn_left(); turn_left()",
                        "    move()",
                        "    turn_left(); turn_left()",
                        "",    
                        "def go_to_neighboring_nonempty_square():", 
                        "    # write the function",
                        "",
                        "go_to_neighboring_nonempty_square()",
                        "while ??? # add the condition",
                        "    pick_ball()",
                        "    ??? # complete the program",
                        ""];
                     
            //var code = ["from karel import *",
            //            "def back():",
            //            "    turn_left(); turn_left()",
            //            "    move()",
            //            "    turn_left(); turn_left()",
            //            "",
            //            "def go_to_neighboring_nonempty_square():",
            //            "    for i in range(4):",
            //            "        if front_is_clear():",
            //            "            move()",
            //            "            if is_ball_on_square():",
            //            "                return",
            //            "            back()",
            //            "        turn_left()  # next direction",
            //            "",
            //            "go_to_neighboring_nonempty_square()",
            //            "while is_ball_on_square():",
            //            "    pick_ball()",
            //            "    go_to_neighboring_nonempty_square()",
            //            ""];
            
            return {robot:robot, world:world, code:code};
        },
      
        isSuccess: function(robot, world) {
            var X = world.getAvenues();
            var Y = world.getStreets();
            for (var y = 1; y <= Y; y++)
                for (var x = 1; x <= X; x++)
                    if (world.getBalls(x, y) > 0)
                        return false;
               
            return true;
        },
    }

Вземете всички топчета от цялата маса
'''''''''''''''''''''''''''''''''''''

.. questionnote::

  Карел първоначално е обърнат на север (нагоре) и е разположен в долния ляв ъгъл на правоъгълна маса с неизвестни размери, без вътрешни стени. На всеки квадрат може да има произволен брой топки. Карел трябва да вземе всички топчета от всички квадратчета на дъската.

Съвет: Напишете функция *empty_one_row()*, която кара Karel да:

- завийте наляво (на изток), като погледнете по реда, в който се намира
- преминете през целия ред и вземете всички топки от всеки квадрат в този ред, включително квадрата, на който е започнал
- обърнете се към началото на реда (т.е. на запад)
- върнете се в началото на реда и завийте на север (нагоре), както той застана преди повикването на функцията

Програмата, която решава задачата с помощта на тази функция, не е дълга. Трябва да направи следното:

- изпразнете първия ред
- докато има редове пред Карел, отидете на следващия и го изпразнете

.. karel:: Karel_functions_take_all_balls_2D
   :blockly:

   {
      setup:function() {
         function random(n) {
            return Math.floor(n * Math.random());
         }

         var sizes = [1, 2, 3, 3, 4, 4, 4];
         var numBalls = [0, 0, 1, 1, 1, 3];
         var X = sizes[random(sizes.length)];
         var Y = sizes[random(sizes.length)];
         var world = new World(X, Y);
         world.setRobotStartAvenue(1);
         world.setRobotStartStreet(1);
         world.setRobotStartDirection("N");
         
         for (var col = 1; col <= X; col++) {
             for (var row = 1; row <= Y; row++) {
                 let B = numBalls[random(numBalls.length)];
                 world.putBalls(col, row, B);
             }
         }
      
         var robot = new Robot();
         
         var code = ["from karel import *",
                     "# write the program",
                     ""];
        //var code = ["from karel import *
        //            "def empty_one_row():",
        //            "    turn_right()                # turn towards end of the row (eastwards)",
        //            "    while is_ball_on_square():  # empty first square in the row",
        //            "        pick_ball()",
        //            "    while front_is_clear():     # while there are unvisited squares",
        //            "        move()                      # go to a new square",
        //            "        while is_ball_on_square():  # emtpy the new square",
        //            "            pick_ball()",
        //            "        ",
        //            "    turn_right(); turn_right()  # turn towards beginning of the row (westwards)",
        //            "    while front_is_clear():     # come back to the first square in that row",
        //            "        move()",
        //            "    turn_right()                # turn towards next row (northwards)",
        //            "",
        //            "empty_one_row()             # pick up the balls from the first row",
        //            "while front_is_clear():     # while there are new rows",
        //            "    move(); empty_one_row()     # go to the next row and empty it",
        //            ""];

         return {robot:robot, world:world, code:code};
        },

        isSuccess: function(robot, world) {
           var X = world.getAvenues();
           var Y = world.getStreets();
           for (var col = 1; col <= X; col++) {
              for (var row = 1; row <= Y; row++) {
                 if (world.getBalls(col, row) > 0)   
                    return false;
              }
           }
                 
           return true;
      },
   }
