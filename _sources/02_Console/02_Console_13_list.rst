Списъци
=======

Досега споменахме низовете и диапазона като видове колекции и видяхме, че низът може да се използва и като колекция. Друг много важен и често използван тип колекции са списъците.

Списъци и низове
----------------

Списъците, както и низовете, могат да бъдат зададени чрез изброяване на елементите, с изключение на това, че елементите на списъка са написани между квадратни скоби:

.. activecode:: console__collections_list1

    for x in [2, 5, 8, 3]:
        print(x)
        
Списъците са в много отношения подобни на низовете. Всички характеристики низовете, споменати в главата на колекциите, се прилагат и за списъци:

- Списък може да бъде поставен и в променлива и обратно - елементите на списъка могат да бъдат присвоени на подходящ брой променливи. 
- Елементите на списъка могат да бъдат достъпни чрез името на списъка и поредния номер (индекс) на елемента, изписан в квадратни скоби
- дължината на списъка се получава от функцията *len*

.. activecode:: console__collections_list2

    names = ["Tom", "Polly", "Filip", "Mary"]
    t, p, f, m = names
    print("p =", p)
    print("names[0] =", names[0])
    print("len(names) =", len(names))

Списъците също имат някои функции, които ги отличават от низовете. Например списъците могат да бъдат разширени с помощта на функцията за добавяне:

.. activecode:: console__collections_list_append

    a = []
    a.append(3)
    a.append(7)
    a.append(2)
    
    for x in a:
        print(x)
    
Също така елементите на списъка могат да променят стойностите си и могат да бъдат изтрити от списъка: 

.. activecode:: console__collections_list_mutable

    a = [3, 7, 2]
    print("Initial list:")
    for x in a:
        print(x)
        
    a[0] = 5
    print("Changed list:")
    for x in a:
        print(x)

    del a[1]
    print("Shorter list:")
    for x in a:
        print(x)

Такива операции с низове не са възможни. Веднъж направен, низът остава такъв, какъвто е. Не може да бъде променен - той не може да променя дължината или стойностите на отделните елементи. Променлива, съдържаща низ, може само да получи изцяло нов низ като стойност, но по този начин предишният низ не е модифициран, а е престанал да съществува. Ето защо се казва, че низовете са неизменни.

Tuples могат да се използват за събиране на данни, които не възнамеряваме да променяме при изпълнение на програма (въпреки че можем да ги променим ръчно преди да изпълним програма). Използвайки низове, ние гарантираме, че данните няма да се променят случайно и програмата ще работи малко по-ефективно с низа, отколкото би направила със списъка.

Комплект *t* може да се преобразува в списък *a* по време на изпълнението на програмата и обратно: ''a = list(t)'' или ''t = tuple(a)'', но такива преобразувания рядко са необходими и по-добре да ги избягвате (ако често се прилагат за големи колекции, реализации като това може да забави значително програмата).

Съставяне на списък
-------------------

Както вече видяхме, можем постепенно да изграждаме списъци в програма. Например, ако ни се даде набор от числа, от които искаме да копираме тези, които са по-големи от нула (и изпълним някаква допълнителна задача с тези числа последни), можем да направим това:

.. activecode:: console__collections_list_create

    numbers  = (2, 5, -2, 1, -3, 4, -7, 3)
    positive_numbers = []
    for x in numbers:
        if x > 0:
            positive_numbers.append(x)
            
    for x in positive_numbers:
        print(x)

В началото имаме празен списък, а след това в цикъла използваме функцията за добавяне, за да добавим към списъка елементите, които искаме.


Зареждане на списък
-------------------

По същия начин можем да заредим данни в списък: 

.. activecode:: console__collections_list_read1

    a = []
    n = int(input("How many elements to load: "))
    for i in range(n):
        x = float(input("Please enter an element: "))
        a.append(x)

    print("The elements of the list are:")
    for x in a:
        print(x)


Друг начин за зареждане на списък е първо да формирате списък с необходимата дължина и след това да присвоите заредените стойности директно на елементите на списъка в цикъла.

.. activecode:: console__collections_list_read2

    n = int(input("How many elements to load: "))
    a = [0] * n
    for i in range(n):
        a[i] = float(input("Please enter an element: "))

    print("The elements of the list are:")
    for x in a:
        print(x)

Използвахме израза ''a = [0] * n'', за да формираме списък от *n* елемента. Операцията ''[0] * n'' се нарича умножение на списъка. Резултатът от умножаването на списъка е сплотяване на n повторения на дадения списък. Например [0]*5 е списъкът [0, 0, 0, 0, 0], а [2, 7] * 3 е списъкът [2, 7, 2, 7, 2, 7].

Ако потребителят въведе всички елементи от списъка в един ред, разделен с интервали, ние пишем програмата така:

.. activecode:: console__collections_list_read_line

    a_str = input("Enter all the elements: ")
    a = []
    for s in a_str.split():
        a.append(float(s))

    print("The elements of the list are:")
    for x in a:
        print(x)

Използвахме функцията *split()*, за да разделим въведения текст на по-къси низове, съдържащи отделни числа.


.. infonote::

    *split()* **функция**:
    
    Функцията split() е символ или текст, които искаме да използваме като разделител. Ако разделителят не е посочен, като интервал '' се приема по подразбиране.
    
    :code:`"1234 56".split() -> ["1234", "56"]`
    
    :code:`"1234,56".split(',') -> ["1234", "56"]`
    
    Резултатът от функцията split() е списък с низове. Броят на по-късите низове, които получаваме в резултат зависи от броя и разположението на разделителните знаци в началния низ. Например, ако текстът съдържа само един разделител някъде по средата, ще получим два по-къси низа. Всеки нов вид на символа за разделяне може да произведе един низ повече в получения списък (ако той наистина отделя част от началния низ от останалата част от текста).

    :code:`"1;23;456;7".split(';') -> ["1", "23", "456", "7"]`
    
    :code:`" 1  234    56 7 ".split() -> ["1", "234", "56", "7"]`
    

Примери и задачи
''''''''''''''''

.. questionnote::

    **Пример - продажби**
    
    В началото на скрипта са дадени стойностите на няколко продажби в един магазин. Извадете продажбите със стойност по-голяма от 1000 и по-малка или равна на 4000 в списък, след което разпечатайте елементите от списъка.

.. activecode:: console__collections_list_sales

    sales = (241, 5372, 1278, 9335, 2438, 127, 529, 6027)
    lower_bound = 1000
    upper_bound = 4000
    # complete the program

Задачата се решава по следния начин:

.. activecode:: console__collections_list_sales_sol

    sales = (241, 5372, 1278, 9335, 2438, 127, 529, 6027)
    lower_bound = 1000
    upper_bound = 4000

    requested_sales = []
    for value in sales:
        if value > lower_bound and value <= upper_bound:
            requested_sales.append(value)

    print('Requested sales:')
    for value in requested_sales:
        print(value)


.. questionnote::

    **Пример - скок-промени**
    
    Даден е набор от числа. Извадете числа, които се различават от предшествениците си поне с 10, след което ги разпечатайте.

.. activecode:: console__collections_list_increasing

    numbers = (5, 7, 9, 11, 22, 18, 15, 13, 36, 31, 27, 14, 13, 20)
    # complete the program

Едно възможно решение е:

.. activecode:: console__collections_list_increasing_sol

    numbers = (5, 7, 9, 11, 22, 18, 15, 13, 36, 31, 27, 14, 13, 20)
    leap_changes = []
    
    for i in range(1, len(numbers)):
        if abs(numbers[i] - numbers[i-1]) >= 10:
            leap_changes.append(numbers[i])

    print('Leap changes:')
    for x in leap_changes:
        print(x)





.. questionnote::

    **Задача - четни числа**
    
    Даден е набор от числа. Извадете числата, които са равномерни, и след това ги разпечатайте.
    
    Спомнете си, че числото *x* е четно ако :math:`x \% 2 == 0`

.. activecode:: console__collections_list_even

    a = (35, 12, 32, 17, 64, 98, 77, 46, 9)
    even = []
    
.. commented out

    for x in a:
        if x % 2 == 0:
            even.append(x)

    print('Even numbers:')
    for x in even:
        print(x)




.. questionnote::

    **Задача - всяка трета дума**
    
    Даден е набор от низове. Извадете низовете, чиито индекси се делят на 3, след което ги отпечатайте.
    
.. activecode:: console__collections_list_every_third

    words = ('All', 'the', 'other', 'words', 'and', 'phrases', 'are', 'not', 'so', 'important')
    every_third = []
    
.. commented out

    for i in range(len(words)):
        if i % 3 == 0:
            every_third.append(words[i])

    print('Every third word:')
    for rec in every_third:
        print(rec)




.. questionnote::

    **Задача - под нулата**
    
    Даден е набор от числа. Извадете числата, които са отрицателни, а техните предшественици са положителни, след което отпечатайте извлечените числа.
    

.. activecode:: console__collections_list_neg_after_pos

    a = (1, -2, 3, 5, -4, -1, -3, 2, -7)
    extracted = []
    
.. commented out

    for i in range(1, len(a)):
        if a[i] < 0 and a[i - 1] > 0:
            extracted.append(a[i])

    for x in extracted:
        print(x)
