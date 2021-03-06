Библиотеки PyGame 
=================

Предполагаме, че вече сте запознати с Python като език и че знаете за изрази (константи, променливи, оператори), оператори (ако, ако-друго, ако-елиф-друго, за), функции (тези вградени, като min или abs и тези, които сами определяте, като използвате ключова дума def), низове ("Hello" или "Hello"), списъци (като [1, 2, 3]), кортежи (като (3, 4)) и други подобни.

Сега ще продължим да практикуваме писането на Python програми, използвайки графичната библиотека PyGame. Избрахме тази библиотека, защото тя предлага възможността да произвежда интересни резултати със сравнително малко програмиране, които включват рисуване, анимация и взаимодействие с потребител. Следователно целта на представянето на библиотеката PyGame е да продължите да практикувате уменията си по програмиране по забавен начин. Читателите, които стават по-заинтересовани от програмирането, ще получат много възможности за модифициране на дадени програми и вдъхновение за различни свои собствени проекти.

За библиотеката PyGame
----------------------

`PyGame <http://pygame.org>`__ библиотеката се развива от началото на 2000-тa годинa. Самите автори казаха, че това не е най-добрата библиотека за програмиране на игри (дори и втората, нито третата по качество), но основното й предимство е, че е по-проста за използване от другите библиотеки и е подходяща за учене на програмиране чрез интересният свят на компютърната графика и компютърните игри.


Онлайн употреба
---------------

За да ви помогнем да започнете, ние ви предоставихме среда, в която можете да пишете и тествате прости PyGame програми в работната книга, която четете. Също така сме подготвили шепа примери и задачи, в които, както в предишните глави, обикновено трябва да завършите или модифицирате стартирани програми, за да ги накарате да работят напълно. Не е необходимо да инсталирате нищо допълнително на вашия компютър, за да използвате тази среда. Ако обаче искате да направите някои по-сериозни програми (например искате да направите своя собствена игра), препоръчваме да инсталирате библиотеката на вашия компютър и да я използвате от среда за разработка на Python (като IDLE), независима от уеб браузъра и тази работна книга. Наред с други предимства, програмирането в действителна среда за разработка е по-удобно и по-ефективно, по-лесно за тестване, отстраняване на грешки и т.н.

Инсталация
----------

За да стартирате програми, написани с помощта на PyGame, в средата ви за разработка на приложения, първо трябва да инсталирате тази библиотека. Предпоставка, разбира се, е да имате инсталиран Python на вашия компютър (за предпочитане версия 3.6 или по-нова). Ако вече не сте го направили, посетете 'сайта <https://www.python.org>' и изтеглете най-новата версия на Python и работната му среда (обикновено се намира в секцията за изтегляния, подраздел, посветен на операционната система, която използвате).

Когато Python е инсталиран на вашия компютър, можем да преминем към инсталацията на библиотеката PyGame. Наистина е много просто. Просто въведете pip3 инсталирате pygame в командния ред. Най-лесният начин да стартирате командния ред е като задържите клавиша Windows и натиснете клавиша r, а след това въведете cmd в прозорецa. Ако получите съобщението, че командата pip3 не съществува, опитайте py -3 -m pip инсталирате pygame.

Когато завършите инсталацията, най-добре е незабавно да проверите дали всичко мина добре:

* стартиране на IDLE Python среда за разработка, като Windows приложение

* отваряне на нов проект в средата за разработка на IDLE  (option File/New)

* въведете програмата, показана по-долу в редактора (можете просто да я копирате и поставите в редактора IDLE)

* запазване на програмата във файл, преди да я стартирате (опция File/ Save as...)

* стартиране на програмата (опция Run / Run Module в менюто или клавиша F5)

След стартиране на програмата трябва да се появи прозорец, в който се очертава квадрат и се показва в продължение на три секунди.

.. activecode:: PyGame__check_install
   :nocodelens:
   :modaloutput: 
   :enablecopy:

   import pygame
   pygame.init()
   prozor = pygame.display.set_mode((200, 200))
   prozor.fill(pygame.Color("white"))
   pygame.draw.rect(prozor, pygame.Color("black"), (20, 20, 160, 160), 5)
   pygame.display.update()
   pygame.time.wait(3000)
   pygame.quit()

Можете също да стартирате други примери от това ръководство на вашия компютър, което ви препоръчваме да правите поне понякога.

