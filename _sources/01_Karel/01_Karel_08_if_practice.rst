If оператор – упражнения
========================

В този раздел ще практикуваме само с помощта на оператора if и комбинирането му с цикли.

Задачи за упражнения
--------------------

Отидете до края на пътеката и вземете само една топка
'''''''''''''''''''''''''''''''''''''''''''''''''''''

.. questionnote::

   Карел трябва да пристигне в края на коридора и да вземе само първата топка по пътя. Началният квадрат никога няма топка върху него, а Карел първоначално не носи топки.

.. karel:: Karel_if__take_first_ball_only
   :blockly:

   {
      setup:function() {
         function random(n) {
            return Math.floor(n * Math.random());
         }
         
         var ww = [
            [
               '█████████████',
               '█E.0.1.0.3.0█',
               '█████████████'
            ],
            [
               '█████████',
               '█E.0.2.2█',
               '█████████'
            ],
            [
               '███████',
               '█E.1.0█',
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
                     "# write the program",
                     ""];
                     
         return {robot:robot, world:world, code:code};
      },
      
      isSuccess: function(robot, world) {
         return robot.getBalls() > 0;
      }
   }

.. reveal:: Karel_if__take_first_ball_only_reveal
    :showtitle: Hint
    :hidetitle: Hide hint
    
    We have started one solution here. You are expected to complete the *if* statements with appropriate conditions.
    
    Karel should take the ball only if two conditions are met:
    
    - the first condition is the one that we check whenever Karel tries to take the ball (without this condition the program could be terminated due to an undoable operation).
    - the second condition is imposed by the requirements of this task, which is that Karel takes the ball only if he has not already taken one before.
    
    The order of checking these two conditions is not important, since both of them should be fulfilled in order to take the ball anyway.
    
    .. activecode:: Karel_if__take_first_ball_only_solution
        :passivecode: true
      
        from karel import *
        while front_is_clear():  # while there are squares in front of Karel
            move()                    
            if ???
                if ???
                    pick_ball()

Вземете топката на съседния площад
'''''''''''''''''''''''''''''''''''

.. questionnote::

   На дъската има само една топка. Карел и топката са разположени на два съседни квадрата без стена между тях (Карел е само на една стъпка от топката, ако първо се обърне към топката). Между другите площади може да има или да не съществува стена. Карел трябва да вземе топката и в крайна сметка може да завърши на всеки квадрат.

   Както обикновено, стартирайте програмата няколко пъти, за да я тествате на различни примери.

Една възможна идея е, че във всяка от четирите посоки се опитваме да накараме Карел да върви една крачка напред и да вземем топката. Във всеки от четирите опита могат да възникнат различни сценарии:

 - възможно е да няма квадрат пред Карел в тази посока
 - възможно е да има квадрат пред Карел, но върху него няма топки
 - възможно е да има квадрат и да има топка върху него

Когато опитвате следващата посока, е много по-просто, ако не е нужно да вземаме предвид дали Карел е намерил квадрат без топка в предишната посока, която е опитал, или изобщо не е намерил квадрат. За да опрости следващия опит, за нас е удобно, че Карел завършва предишния опит, когато е бил на празен квадрат в същото състояние, както когато не е имало квадрат. Когато няма квадрат в опитаната посока, Карел ще остане на началния квадрат, обърнат към опитаната посока. За да улесним продължаването на търсенето, можем да оставим Карел на същия площад, обърнат към същата посока, когато той се върне от празен съседен квадрат. Всъщност няма да навреди, ако го направим и когато Карел вземе топката (възможно е Карел излишно да търси, но това няма да причини грешки). 
Тъй като доведохмеКарел в същото състояние (позиция и ориентация) след всеки от трите случая по-горе, ние знаем точно новото си изходно състояние за всеки следващ опит. След всеки опит за направление, просто трябва да завием Карел към следващата посока, в която ще се опитаме да намерим топката (или вляво, или вдясно).

.. karel:: Karel_if__take_neighboring_ball
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
                     "for i in range(4):",
                     "    if front_is_clear():",
                     "        move()",
                     "        # tell Karel to try to take the ball",
                     "        # tell Karel to go back to the starting square...",
                     "        # ... and turn towards the square at which he just tried",
                     "        # (as if he had not gone to that square at all)",
                     "    # tell Karel to prepare for the next attempt",
                     ""];
                     
         return {robot:robot, world:world, code:code};
      },
      
      isSuccess: function(robot, world) {
         return robot.getBalls() > 0;
      }
   }

.. commented out
   .. reveal:: Karel_if__take_neighboring_ball_reveal
       :showtitle: Solution
       :hidetitle: Hide solution
       
       Solution can look like this:
       
       .. activecode:: Karel_if__take_neighboring_ball_solution
           :passivecode: true
         
           from karel import *
           for i in range(4):          # in each of the 4 directions
               if front_is_clear():        # look for a square in that direction
                   move()                    
                   if is_ball_on_square():
                       pick_ball()
                   turn_left()                 # go back to starting square
                   turn_left()
                   move()
                   turn_left()                 # face the square you just tried
                   turn_left()
               turn_left()                 # next direction

Следвайте пътеката
''''''''''''''''''

.. questionnote::

  На масата има само една топка и Карел трябва да я вземе. Пътят до топката не е само направо и  няма пресечки (винаги има само един начин да продължите да се движите, дори от стартовия квадрат).

.. karel:: Karel_if__take_ball_no_branches
   :blockly:

   {
      setup:function() {
         function random(n) {
            return Math.floor(n * Math.random());
         }
         
         var ww = [
            [
               '███████████',
               '█N█0.0.0.0█',
               '█.█.█████.█',
               '█0█0█0.1█0█',
               '█.█.█.███.█',
               '█0.0█0.0.0█',
               '███████████'
            ],
            [
               '█████████',
               '█0.0.0.0█',
               '█.█████.█',
               '█0█0.0.0█',
               '█.█.█████',
               '█0█E█0.0█',
               '█.███.█.█',
               '█0.0.0█1█',
               '█████████'
            ],
            [
               '█████████████',
               '█W.0.0█0.0.0█',
               '█████.█.███.█',
               '█0.0.0█0█0.0█',
               '█.█████.█.███',
               '█0.0.0.0█0.1█',
               '█████████████'
            ],
            [
               '███████████',
               '█0.0█0.0█S█',
               '█.█.█.█.█.█',
               '█0█0.0█0.0█',
               '█.█████████',
               '█0█0.0█0.0█',
               '█.█.█.█.█.█',
               '█0.0█0.0█1█',
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
                     "... # write the program",
                     ""];
                     
         return {robot:robot, world:world, code:code};
      },
      
      isSuccess: function(robot, world) {
         return robot.getBalls() > 0;
      }
   }

.. reveal:: Karel_if__take_ball_no_branches_reveal
    :showtitle: Hint
    :hidetitle: Hide hint
    
    We give a program-like instructions for one possible solution:

    .. activecode:: Karel_if__take_ball_no_branches_solution
        :passivecode: true
      
        # First, turn towards the (only) free square
        
        while you can't move forward: 
            turn left
            
        while you can go forward:
            move forward
            if there is no free square in front of you: # if there is no straight path
                turn left
                if there is no free square in front of you: # if no path to the left either
                    turn right twice
        
        take the ball

.. commented out
   .. reveal:: Karel_if__take_ball_no_branches_reveal
       :showtitle: Solution
       :hidetitle: Hide solution
       
       One possible solution is:
   
       .. activecode:: Karel_if__take_ball_no_branches_solution
           :passivecode: true
         
           from karel import *
           while not front_is_clear(): # turn towards the (only) free square
               turn_left()
               
           while front_is_clear():
               move()
               
               # turn towards the next free square
               if not front_is_clear():   # if there is no straight path,
                   turn_left()                # try left
               if not front_is_clear():   # if there is no path to the left
                   turn_right(); turn_right() # try right
           
           if is_ball_on_square():
               pick_ball()

Отклоняване от целта
'''''''''''''''''''''

.. questionnote::

  На масата има само една топка и Карел трябва да я вземе. За да стигне до топката, Карел трябва да тръгне право, само когато не може да завие наляво или надясно (няма да има двусмислено кръстовище, където има път и вляво, и вдясно).

.. karel:: Karel_if__p1_left_p2_right_p3_forward
   :blockly:

   {
      setup:function() {
         function random(n) {
            return Math.floor(n * Math.random());
         }
         
         var ww = [
            [
               '███████████',
               '█1.0█0.0.0█',
               '███.█.█████',
               '█0.0.0█0.0█',
               '█████.███.█',
               '█S.0.0.0.0█',
               '███████████'
            ],
            [
               '███████████',
               '█0.0.0█0.0█',
               '█████.█.███',
               '█0.0.0█0.0█',
               '█.█.█.█.█.█',
               '█0█0█E█0█1█',
               '█.█.███.███',
               '█0█0.0.0.0█',
               '███████████'
            ],
            [
               '█████████████',
               '█E.0.0█0.0.0█',
               '███.█.█.█████',
               '█0.0█0█0.0.0█',
               '█.█.███.███.█',
               '█0█0█0.0.0█0█',
               '█.███.█████.█',
               '█0.0.0.0.0█1█',
               '█████████████'
            ],
            [
               '█████████',
               '█0.0.0█S█',
               '█.█████.█',
               '█0.0.0.0█',
               '███.███.█',
               '█0█0.0█0█',
               '█.█.█.███',
               '█0.0█0.1█',
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
                     world.setRobotStartDirection("SWEN".charAt(pos));
                 }
                 let d = w[wy].charCodeAt(wx);
                 if (d >= 48 && d < 58) world.putBalls(x, y, d - 48);
             }
         }
         
         var robot = new Robot();
         
         var code = ["from karel import *",
                     "... # write the program",
                     ""];
                     
         return {robot:robot, world:world, code:code};
      },
      
      isSuccess: function(robot, world) {
         return robot.getBalls() > 0;
      }
   }
   
.. reveal:: Karel_if__p1_left_p2_right_p3_forward_reveal
    :showtitle: Hint
    :hidetitle: Hide hint

    Instructions for one possible solution:
    
    .. activecode:: Karel_if__p1_left_p2_right_p3_forward_solution
        :passivecode: true
      
        # turn towards the only free square
        
        while you can move forward:
            move forward
            # try going left (turn left and try going forward)
            # if you can't go left:
                # try going right
                # if you can't go right either
                    # prepare to try going straight in the next iteration
        
        take the ball

.. commented out
    .. reveal:: Karel_if__p1_left_p2_right_p3_forward_reveal
        :showtitle: Solution
        :hidetitle: Hide solution

        .. activecode:: Karel_if__p1_left_p2_right_p3_forward_solution
            :passivecode: true
          
            from karel import *
            for i in range(3):        # turn towards the only fre square
                if not front_is_clear():
                    turn_left()
            
            while front_is_clear():
                move()
                turn_left()                # try going left
                if not front_is_clear():   # if you can't go left
                    turn_right(); turn_right()     # try going right
                if not front_is_clear():   # if you can't go right either
                    turn_left() # prepare to try going straight in the next iteration
            
            pick_ball()

Завийте наляво, където е възможно
'''''''''''''''''''''''''''''''''

.. questionnote::

  На масата има само една топка и Карел трябва да я вземе. Карел винаги ще достигне топката, като завива наляво, когато може, и ще тръгне направо, когато не може да отиде наляво (когато не може да отиде нито наляво, нито направо, това означава, че е пристигнал). Първоначално Карел е обърнат така, както трябва, а първата му стъпка винаги е напред.
  
.. karel:: Karel_if_p1_left_p2_forward
   :blockly:

   {
      setup:function() {
         function random(n) {
            return Math.floor(n * Math.random());
         }
         
         var ww = [
            [
               '█████████████',
               '█0.0.0.0.0.0█',
               '█.███████.█.█',
               '█0.0.0.1█0█0█',
               '█████.███...█',
               '█0.0.0.0█0.0█',
               '█████████.███',
               '█E.0.0.0.0.0█',
               '█████████████'
            ],
            [
               '█████████████',
               '█0.0.0.0.0█0█',
               '█..██████.█.█',
               '█0.0█0.0.0█0█',
               '█████..██.█.█',
               '█0.0.0.1█0█0█',
               '█████████..██',
               '█E.0.0.0.0.0█',
               '█████████████'
            ],
            [
               '█████████████',
               '█0.0.0.0.0█0█',
               '█.█.........█',
               '█0█0.0.0.0.0█',
               '█.█.███████.█',
               '█0█0.0.1█0█0█',
               '█.█.█████.█.█',
               '█0.0.0.0.0█N█',
               '█████████████'
            ],
            [
               '█████████████',
               '█S█0.0.0.0█0█',
               '█.███.███...█',
               '█0█0.1█0█..0█',
               '█.███████.█.█',
               '█0.0.0.0.0█0█',
               '█.███████████',
               '█0.0.0.0.0.0█',
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
                  world.setRobotStartDirection("SWEN".charAt(pos));
               }
               let d = w[wy].charCodeAt(wx);
               if (d >= 48 && d < 58) world.putBalls(x, y, d - 48);
            }
         }
         
         var robot = new Robot();
         
         var code = ["from karel import *",
                     "... # write the program",
                     ""];
                     
         return {robot:robot, world:world, code:code};
      },
      
      isSuccess: function(robot, world) {
         return robot.getBalls() > 0;
      }
   }

.. reveal:: Karel_if_p1_left_p2_forward_reveal
    :showtitle: Hint
    :hidetitle: Hide hint

    Instructions for one possible solution:
    
    .. activecode:: Karel_if_p1_left_p2_forward_solution
        :passivecode: true
      
        while you can go forward:
            move forward
            # if there is no path to the left
                # stay turned straight

        take the ball

.. commented out
    .. reveal:: Karel_if_p1_left_p2_forward_reveal
        :showtitle: Solution
        :hidetitle: Hide solution

        .. activecode:: Karel_if_p1_left_p2_forward_solution
            :passivecode: true
          
            from karel import *
            while front_is_clear():
                move()
                turn_left()
                if not front_is_clear():
                    turn_right()

            if is_ball_on_square():
                pick_ball()
