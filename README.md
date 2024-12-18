# STM Bank

Задание включает в себя следующие исходные файлы:

* [`src/Bank.kt`](src/Bank.kt) содержит интерфейс для гипотетического банка.
* [`src/BankImpl.kt`](src/BankImpl.kt) содержит простую реализации операций банка используя STM.
* [`src/STM.kt`](src/STM.kt) содержит незаконченную реализацию obstruction-free STM. 
 
## Задание

Необходимо закончить реализацию STM, написав реализацию метода `TxVar.openIn` вместо написанного там кода-заглушки,
который должен открывать перменную в указанной транзакции и применять к ней функцию `update`. 
Алгоритм такого STM без блокировок описан в учебнике
"The Art of Multiprocessor Programming" by Maurice Herlihy and Nir Shavit 
и был рассказан на лекции.  

В качестве алгоритма разрешения конфликтов между транзакциями необходимо отменять незаконченную транзакцию,
которая в данный момент работает над транзакционной переменной, что обеспечивает работу данного алгоритма
без блокировок, а точнее obstruction-free образом.  
  
Весь код должен содержаться в файле [`STM.kt`](src/STM.kt).
**В заголовке файла, в строке `@author` впишите вашу фамилию и имя**.

## Сборка и тестирование

Для проверки вашего решения запустите из корня репозитория:
* `./gradlew test` на Linux или MacOS
* `gradlew test` на Windows

При этом автоматически будут запущены следующие тесты:

* [`FunctionalTest`](test/FunctionalTest.kt) проверяет базовую корректность работы операций банка.
* [`MTStressTest`](test/MTStressTest.kt) проверяет основные аспекты корректности работы банка при множестве одновременно работающих потоков исполнения.
* [`LinearizabilityTest`](test/LinearizabilityTest.kt) проверяет все аспекты корректности работы банка и линеаризуемость операций, сравнивая различные варианты одновременного выполнения операций с различными вариантами их перестановки на модельной однопоточной реализации.

Обратите внимание, что исходная реализация проходит только `FunctionalTest`, но не проходит многопоточные тесты.

## Сделайте наблюдения

При запуске `MTStressTest` происходит замер пропускной способности реализации банка и выдается среднее количество 
операций в секунду, которе выполняет реализация банка при этом профиле нагрузки. 

* Сравните пропускную способность реализации `BankImpl` в этом задании "STM Bank" и в предыдущем задании "Lock-Free Bank". 
  Какая реализация работает быстрей и почему?
* Что можно сказать о простоте реализации (количестве кода) в реализации `BankImpl` в этих двух заданиях?

