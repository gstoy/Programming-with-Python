Събиране на данни
=================

В предишния урок използвахме комплект, за да изпълняваме някои команди (изчисляване и печат) над всяка стойност от комплекта, използвайки for цикъл.

Комплектите също са тип данни в Python, като числа, низове или логически стойности. Типовете int (integer), float (реално число), str (string) и bool (логическа стойност) са основни типове. Разликата между комплектите и основните типове е, че стойността на комплект се състои от множество стойности от по-опростен тип.

Всяка стойност, която се състои от множество стойности от по-опростен тип, ще се нарича колекция. Данните, от които се събира колекцията, се наричат елементи за събиране.

Можем да кажем, че комплектът е вид колекция и това е първият вид колекция, който срещаме.



Комплект (Tuple) и неговите елементи
------------------------------------

Опаковане и разопаковане на комплектите
'''''''''''''''''''''''''''''''''''''''

Можем да поставим целия комплект в променлива, както правим със стойности от по-прост тип. В следващия пример, променливата на температурата съдържа целия комплект като неговата стойност.

.. activecode:: console__collections_tuple1
    
    temperatures = (25, 24, 25, 23, 25, 25)
    for t in temperatures:
        print(t)
        
Този вид присвояване на стойност (както в първия ред на програмата) е известен като пакетиране на комплект. Възможно е и обратното присвояване: когато знаем колко елемента има в комплект, можем да присвоим елементите на комплекта на съответния брой променливи:

.. activecode:: console__collections_tuple2
    
    full_name = ("Arthur", "Conan", "Doyle")  
    first_name, middle_name, last_name = full_name
    print(first_name)
    print(middle_name)
    print(last_name)
    
Твърдения като ``first_name, middle_name, last_name = full name`` се наричат отваряне на комплекта

Същият ефект се постига чрез свързано твърдение

.. code::
    
    first_name, middle_name, last_name = "Arthur", "Conan", "Doyle"
    
Комплектите не се появяват в това изявление, което се нарича присвояване на множество стойности.

Елементи и индекси
''''''''''''''''''

Можем да получим и елементите на комплект, като напишем името на комплекта, а зад него в квадратни скоби поредният номер на елемента, който искаме. Тук трябва да се отбележи, че преброяването на елементите на всяка колекция започва от нула. Например:

.. activecode:: console__collections_index

    basic_colors = ("Red", "Green", "Blue")
    print(basic_colors[0])
    print(basic_colors[1])
    print(basic_colors[2])

Поредният номер на елемент се нарича също *индекс* на елемента. ако комплектът има *n* елемента, можем да използваме числата 0, 1, 2, ... n-1 като индекси. В горния пример n = 3, така че са разрешени индекси 0, 1 и 2. Опитът да използвате индекс извън тези граници причинява грешка (опитайте).

Дължина на комплектите
''''''''''''''''''''''

Броят на елементите на комплека може да се получи с помощта на функцията *len*.

.. activecode:: console__collections_len1
    
    basic_colors = ("Red", "Green", "Blue")
    n = len(basic_colors)
    print(n)
    
или по-кратко:

.. activecode:: console__collections_len2
    
    print(len(("Red", "Green", "Blue")))
    
Обърнете внимание на двойните скоби (едната за функция, а другата за комплект).

Чрез тези примери видяхме, че комплектните елементи могат да бъдат числа или низове. Всъщност елементите на комплекта могат да бъдат от всякакъв тип, основни или сложни.

Например, възможно е да се създаде пакет от комплекти:

.. activecode:: console__collections_len3
    
    t = ((11, 12, 13), (21, 22, 23))
    print(len(t))


.. commented out

    t2 = ((1, 2, 3), ) # last comma matters
    print(len(t2))
    
Комплекта t съдържа два по-прости комплекта, следователно броят на неговите елементи е 2.

В Python елементите на един комплект могат да бъдат от различни типове и такива примери ще видим последни.


Обхват
------

Обхватът е друг вид колекция. За разлика от комплекта, елементите тук винаги са цели числа.

Обхватът може да бъде определен по няколко начина.


Обхват с един аргумент
''''''''''''''''''''''

Най-простата форма за определяне на диапазон е  *range(n)*, където *n* е положително цяло число. Диапазонът *range(n)* съдържа цели числа от 0 до n, без да включва n. Например, range(5) съдържа стойности 0, 1, 2, 3, 4.

.. activecode:: console__collections_range_n_i
    
    for i in range(5):
        print(i)
        
Виждаме, че в оператора *for* можем да използваме диапазона по същия начин като комплекта. Всъщност, всяка колекция може да бъде на мястото на комплекта или гамата.

Тъй като range(n) съдържа общо n стойности, този диапазон често се използва, когато командата трябва да се повтаря n пъти по същия начин:

.. activecode:: console__collections_range_n
    
    for i in range(5):
        print("Hello!")

Функцията за печат беше изпълнена за всяка стойност i от последователност 0, 1, 2, 3, 4, но в този пример тези стойности не се използват в тялото на цикъла. Така постигнахме, че функцията за печат се изпълнява 5 пъти по абсолютно същия начин, тоест тя се повтаря 5 пъти.

Друго често срещано използване на този тип гама е да преминете през всички елементи на комплект. В такъв случай променливата на цикъла служи като индекс. Този начин на преминаване през стойностите на комплекта е подходящ, когато освен тези стойности на комплекта в цикъла имаме нужда и от техните последователни номера (този начин на преминаване през колекцията е по-често срещан в други езици за програмиране от Python).


.. activecode:: console__collections_for_range_len
    
    colors = ["Red", "Green", "Blue", "Yellow", "Magenta"]
    n = len(colors)
    for i in range(n):
        print('Color #', i, 'is', colors[i])
    

Обхват с два аргумента
''''''''''''''''''''''''

Когато се нуждаем от последователност от последователни цели числа, които не започват от нула, задаваме диапазона като range(a, b), където a и b са цели числа, така че a <b. Тогава последователността е съставена от цели числа от a до b, без да се включва b. Например диапазонът на range(1, b) дава последователността от числа 1, 2, 3, 4, 5:

.. activecode:: console__collections_range_a_b
    
    for i in range(1, 6):
        print(i)

Обхват с три аргумента
''''''''''''''''''''''

Третата форма за определяне на диапазон има три аргумента:

.. activecode:: console__collections_range_a_b_c
    
    for i in range(2, 12, 2):
        print(i)

Стойностите на диапазона, дадени от диапазон (a, b, c), включва от a до b (без да се включва b) със стъпка c, т.е. стойностите се променят с c. Стъпка c също може да бъде отрицателна:

.. activecode:: console__collections_range_a_b_cneg
    
    for i in range(12, 2, -2):
        print(i)


Можем да преобразуваме диапазон в комплект (обратното не е възможно, нито някога е необходимо):

.. activecode:: console__collections_range_to_tuple
    
    a = tuple(range(2, 12, 2))
    print(len(a))

Низовете(strings) като колекция
-------------------------------

Досега сме използвали низове като основен тип, но низовете могат да се използват и като колекции от отделни знаци. Можем да преместваме низови символи с помощта на цикъл и да извличаме отделни символи, използвайки индекси:

.. activecode:: console__collections_str_as_collection
    
    s = 'text'
    print(s[1], s[2])
    for c in s:
        print(c)

Функции на колекциите
---------------------

В Python има много функции, които приемат колекция като аргумент. Една от тях е функцията len, която вече срещнахме. Някои други често използвани функции, които се прилагат за колекциите, са:

- *min*, функция, която дава най-малкия елемент от колекция
- *max*, функция, която дава най-големия елемент от колекция
- *sum*, функция, която дава сумата от елементите на колекция

.. activecode:: console__collections_aggregation
    
    print('Tuple:')
    t = (2, 8, 4, 15, 3)
    print('len(t) =', len(t))
    print('min(t) =', min(t))
    print('max(t) =', max(t))
    print('sum(t) =', sum(t))

    print('Range:')
    r = range(1, 10, 2)
    print('len(r) =', len(r))
    print('min(r) =', min(r))
    print('max(r) =', max(r))
    print('sum(r) =', sum(r))

    print('String:')
    s = 'Python'
    print('len(s) =', len(s))
    print('min(s) =', min(s))
    print('max(s) =', max(s))
    # elements of s are not numbers, so uncommenting the next statement would cause an error
    # print('sum(s) =', sum(s)) 

Стойностите на функциите len, sum, min, max за диапазона също могат да бъдат определени от параметрите на диапазона, но тук искахме да отбележим, че всички тези функции приемат различни колекции като свой аргумент (включително диапазон).

Въпроси
'''''''

.. mchoice:: console__collections_quiz_tuple_unpack
   :answer_a: a program error occurs
   :answer_b: 2
   :answer_c: 20
   :answer_d: 3
   :feedback_a: Try again
   :correct: c
   :feedback_b: Try again
   :feedback_c: Correct
   :feedback_d: Try again

   Какво отпечатва следната програма?
   
   .. code::
   
       t = (32, 41, 20, 17)
       a, b, c, d = t
       print(c)

.. mchoice:: console__collections_quiz_tuple_index
   :answer_a: 1
   :answer_b: 2
   :answer_c: a program error occurs
   :answer_d: 3
   :correct: b
   :feedback_a: Try again
   :feedback_b: Correct
   :feedback_c: Try again
   :feedback_d: Try again

   Какво отпечатва следната програма?
   
   .. code::
   
       a = (1, 2, 3)
       print(a[1])


.. mchoice:: console__collections_quiz_range1
   :answer_a: range(4)
   :answer_b: range(1, 4)
   :answer_c: range(3)
   :answer_d: range(1, 3)
   :correct: b
   :feedback_a: Try again
   :feedback_b: Correct
   :feedback_c: Try again
   :feedback_d: Try again

   Кой диапазон съдържа само стойности 1, 2, 3?

.. mchoice:: console__collections_quiz_range2
   :answer_a: 5
   :answer_b: 6
   :answer_c: 9
   :answer_d: 10
   :correct: a
   :feedback_a: Correct
   :feedback_b: Try again
   :feedback_c: Try again
   :feedback_d: Try again

   Колко стойности съдържа диапазонът (1, 10, 2)?

.. dragndrop:: console__collections_quiz_range_len
    :feedback: Try again!
    :match_1: 5|||range(5)
    :match_2: 0|||range(3, 3)
    :match_3: 3|||range(1, 4)
    :match_4: 1|||range(3, 6, 3)

    Свържете обхватите с броя елементи


.. dragndrop:: console__collections_quiz_range_values
    :feedback: Try again!
    :match_1: 3, 4, 5|||range(3, 6)
    :match_2: 0, 1, 2|||range(3)
    :match_3: 3, 1|||range(3, -1, -2)
    :match_4: 3, 2, 1, 0, -1|||range(3, -2, -1)
    :match_5: 3|||range(3, 6, 3)

    Свържете обхватите със стойностите
