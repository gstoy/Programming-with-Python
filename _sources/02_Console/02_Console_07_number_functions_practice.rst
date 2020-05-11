Математически функции - упражнения
==================================

Нека да практикуваме, използвайки математическите функции, които сме научили.

.. questionnote::
    
    **Задача - реклама:** 
    
    Томас разпространява рекламни пакети, съдържащи един календар, ключодържател и химикалка. Напишете програма, която зарежда колко календари, ключодържатели и химикалки, които Томас има и след това отпечатва колко рекламни пакета може да направи.

За да завършите програмата, поставете една от математическите функции, които сте научили.

.. activecode:: console__mathfunc_promo_material

    num_calendars = int(input("How many calendars are there?"))
    num_keychains = int(input("How many keychains are there?"))
    num_pens = int(input("How many pens are there?"))
    num_packages = 0 # complete the statement
    print(num_packages, "packages can be made.")


.. questionnote::

    **Задача - лимонада:** 
    
    Група хора тръгнаха на пътешествие и Зоуи направи лимонада за всички. Напишете програма, която зарежда колко литра лимонада е направила Zoe (като реално число), след което пише колко половин литрови бутилки могат да бъдат напълнени с тази лимонада и колко бутилки отнема за цялата лимонада (двете числа могат да варират най-много от един).

    
  
.. activecode:: console__mathfunc_lemonade

.. reveal:: console__mathfunc_lemonade_reveal
   :showtitle: Help
   :hidetitle: Hide help
   
   To complete the following program, use some of the rounding functions.
   
   .. activecode:: console__mathfunc_lemonade_solution
   
        liters = float(input())
        num_full_bottles = 0 # complete the statement
        total_bottles = 0 # complete the statement
        print(num_full_bottles, "bottles can be filled.")
        print("A total of", total_bottles, "bottles are required.") 

    
.. questionnote::

    **Задача - играта:**
    
    Шестимата приятели се съгласиха да се качат на определеното време и да играят игра. Напишете програма, която зарежда времето за закъснение на всеки играч в минути (като цели числа) и отпечатва с колко минути закъснение може да започне мачът.
    
.. activecode:: console__mathfunc_late_game

.. reveal:: console__mathfunc_late_game_reveal
   :showtitle: Help
   :hidetitle: Hide help
   
   One possible solution is partially written below. Try to complete it.
   
   .. activecode:: console__mathfunc_late_game_help

        t1 = int(input("How many minutes late was the first: "))
        # load the remaining data the same way
        game_delay = 0 # fix this statement
        print("The match could have started with a", game_delay, "minute delay.")

.. commented out

   .. activecode:: console__mathfunc_late_game_solution

        t1 = int(input("How many minutes late was the first: "))
        t2 = int(input("How many minutes late was the second: "))
        t3 = int(input("How many minutes late was the third: "))
        t4 = int(input("How many minutes late was the fourth: "))
        t5 = int(input("How many minutes late was the fifth: "))
        t6 = int(input("How many minutes late was the sixth: "))
        game_delay = 0 # complete this statement
        print("The match could have started with a", game_delay, "minute delay.")



.. questionnote::

    **Задача - два автобуса:** 
    
    Мая и Лола пътуват по една и съща магистрала в два различни автобуса и разговарят по телефона. Единият от тях току-що е забелязал основната точка x, а другият y. Напишете програма, която зарежда цели числа: x и y и отпечатва колко мили Мая и Лола са на разстояние една от друга.
    
.. activecode:: console__mathfunc_buses

.. commented out
    
    .. reveal:: console__mathfunc_buses_reveal
       :showtitle: Help
       :hidetitle: Hide help
       
       To complete the following program, use one of the math functions you have learned.
       
       .. activecode:: console__mathfunc_buses_solution

            x = int(input("Enter x: "))
            y = int(input("Enter y: "))
            distance = 0 # complete thes statement
            print("Distance is", distance)



.. questionnote::

    **Задача - Видео уроци**

    Курсът се състои от няколко видео урока, които всички продължават еднакво. Решихте да отделяте 90 минути на този курс всеки ден и искате да знаете колко дни ще отнеме за целия курс. Напишете програма, която зарежда броя на уроците и продължителността на един урок в минути и отпечатва необходимия брой дни, закръглени до най-близкото цяло число.
        
.. activecode:: console__mathfunc_videolessons
