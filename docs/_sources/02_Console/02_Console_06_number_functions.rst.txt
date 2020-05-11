Математически функции
=====================

Ние използваме функции в програмирането през цялото време. Например print (), input (), int (), float () и str () са функции на езика Python, който използвахме досега. В Python има много други функции и много от тях се използват в математиката. По-долу ще видим някои от по-простите математически функции.

Функции *abs()*, *min()* и *max()*
----------------------------------

Функциите abs (), min () и max () често се използват при изчислителни задачи. Вероятно вече сте ги използвали някъде, така че нека просто ги обясним накратко:

- -*abs()* връща абсолютната стойност на числовия израз, който му се предава като аргумент (абсолютната стойност на число се получава чрез игнориране на знака на числото, вижте пример по-долу);
- -*min()* може да има два или повече числови аргумента и връща стойността на най-малкия от тях;
- -*max()* може да има два или повече числови аргумента и връща стойността на най-големия от тях;

Ето как да използвате тези функции в програма:

.. activecode:: console__numberfunc_absminmax_example

    print("abs(3) =", abs(3))
    print("abs(-7) =", abs(-7))
    print("abs(-5 - -2) =", abs(-5 - -2))
    print("min(5, 2, 7, 3) =", min(5, 2, 7, 3))
    print("max(5, 2, 7, 3) =", max(5, 2, 7, 3))

Функциите *abs()*, *min()* и *max()* - въпроси
----------------------------------------------

Проверете разбирането си за горните функции:

.. mchoice:: console__numberfunc_min
   :answer_a: 10
   :answer_b: 20
   :answer_c: 30
   :correct: a
   :feedback_a: Correct!
   :feedback_b: The min function returns the smallest of the values passed to it as arguments.
   :feedback_c: The min function returns the smallest of the values passed to it as arguments.
		
   Каква е стойността на израза ``min(10, 20, 30)``?

.. mchoice:: console__numberfunc_max
   :answer_a: 10
   :answer_b: 20
   :answer_c: 30
   :correct: c
   :feedback_a: The max function returns the largest of the values passed to it as arguments.
   :feedback_b: The max function returns the largest of the values passed to it as arguments.
   :feedback_c: Correct!
		
   Каква е стойността на израза ``max(10, 20, 30)``?

.. dragndrop:: console__numberfunc_max_0x100
    :feedback: Try again!
    :match_1: the value of the expression is 0 ||| if x is less than zero
    :match_2: the value of the expression is x ||| if x is between 0 and 100
    :match_3: the value of the expression is 100 ||| if x is greater than 100
    
    Съпоставете стойностите на израза ``min(100, max(0, x))`` с условията за x.

.. dragndrop:: console__numberfunc_max_0x
    :feedback: Try again!
    :match_1: abs(x)||| x if x is positive, and the opposite number otherwise
    :match_2: max(0, x)||| x if x is positive and zero otherwise
    :match_3: min(0, x)||| x if x is negative and zero otherwise
    :match_4: min(0, abs(x))||| always zero
		
    Съпоставете изразите със стойностите им.

Функции за закръгляване на стойността
-------------------------------------

Закръгляването на реалната стойност до цяло число е операция, от която също често се нуждаем. Вече видяхме, че преобразувайки реално число в цяло число, го закръгляме към нула. Има още няколко функции, които можем да използваме в Python, за да закръглим истинско число по различни начини:

- *round()* връща целочислено най-близко до аргумента (типът на резултата е int);
- *floor()* връща най-близкото цяло число по-малко или равно на стойността на аргумента (типът на резултата е float);
- *ceil()* връща най-близкото цяло число, по-голямо или равно на стойността на аргумента (типът на резултата е float);

Изпълнете следната програма, за да видите как работят тези функции и да ги сравните.

.. activecode:: console__numberfunc_rounding_example

    import math
    
    print("round(56.234) =", round(56.234))
    print("round(56.789) =", round(56.789))

    print("math.floor(56.234) =", math.floor(56.234))
    print("math.floor(56.789) =", math.floor(56.789))

    print("math.ceil(56.234) =", math.ceil(56.234))
    print("math.ceil(56.789) =", math.ceil(56.789))


Обърнете внимание, че функциите на пода и тавана са малко по-различни от функцията за кръгла форма и всички предишни функции - тя казва математиката. пред името им в програмата. Това е така, защото тези функции са дефинирани в модул, наречен математика. Модулите са програмни единици, които съдържат различни функции, константи и други части от кода, които можем да използваме в нашите програми. Математическият модул съдържа много други функции в допълнение към пода и таваните. Например, известната константа pi може да се използва като math.pi, а функционалният корен като math.sqrt (тук няма да ги използваме).

За да използваме функциите на математическия модул, трябва да прикачим този модул към нашата програма. Направихме това, като написахме математика за импортиране в началото на програмата. Това, разбира се, ни позволява да използваме и всички други математически функции и всичко останало, дефинирано в този модул.

За функцита round и всички предишни функции не е необходим специален модул, тъй като тези функции са вградени в самия Python, така че те винаги са пряко достъпни за нас.

Функции за закръгляване на стойността - Въпроси
-----------------------------------------------

Проверете разбирането си за функциите, обяснени в този урок:

.. mchoice:: console__numberfunc_abs_round
   :answer_a: -2
   :answer_b: 2
   :answer_c: -3
   :answer_d: 3
   :correct: d
   :feedback_a: Read the explanations about abs and round functions again.
   :feedback_b: The round function returns the closest integer.
   :feedback_c: The abs function returns the absolute value of a number, which is always greater than or equal to zero.
   :feedback_d: Correct!
		
   Каква е стойността на израза  ``abs(round(-2.7))``?
   
.. mchoice:: console__numberfunc_max_abs
   :answer_a: max(x, round(x))
   :answer_b: max(x)
   :answer_c: round(x)
   :answer_d: abs(x)
   :correct: a
   :feedback_a: Correct!
   :feedback_b: The max function should have at least two arguments.
   :feedback_c: In this way, the amount can also be reduced.
   :feedback_d: The amount is already positive, nothing is achieved here with the abs function.
		
   Един касиер закръгля сметката до най-близкото цяло число, само ако сумата се увеличи чрез закръгляне, в противен случай отчита сумата такава, каквато е. Каква формула прилага тази каса (x е началната стойност на сметката)?

.. dragndrop:: console__numberfunc_rounding
    :feedback: Try again!
    :match_1: towards zero|||int()
    :match_2: to a closer whole number|||round()
    :match_3: to a smaller whole number|||floor()
    :match_4: to a greater whole number|||ceil()

    Съпоставете функциите на закръгляване с начина на закръгляване.

.. questionnote::

    **Задачата за любопитните**
    
    Round функция може да бъде извикана и с два аргумента (няма да я използваме по този начин), където вторият аргумент обикновено е малко цяло число. Проверете например стойностите на round(123.23456,2) round(123.23456,2), round(123.23456,3)round(123.23456,3 и round(123.23456,−1) round(123.23456,−1). Можете да използвате полето по-долу, за да изпробвате нещата бързо.
    
    Опитайте да обясните за какво е вторият аргумент round, когато се извиква функция с два аргумента.
    
.. activecode:: console__givenfunc_round

