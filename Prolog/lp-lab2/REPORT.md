#№ Отчет по лабораторной работе №2
## по курсу "Логическое программирование"

## Решение логических задач

### студент: Хисамутдинов Д.С. М80-208б-18

## Результат проверки

| Преподаватель     | Дата         |  Оценка       |
|-------------------|--------------|---------------|
| Сошников Д.В. |              |               |
| Левинская М.А.|              |               |

## Введение

<!-- Опишите своими словами, какие подходы существуют к решению логических задач. Почему Prolog оказывается удобным языком для написания решателей таких задач? -->

Часто в решении логических задач используется перебор, частые ошибки, сложные условия, язык Prolog позволяет манипулировать выссказываниями, задавая финальное условие, язык умным перебором находит подходящие решения.

## Задание

Вариант 4.

Левин, Митерев и Набатов работают в банке в качестве бухгалтера, кассира и счетовода. Если Набатов  кассир, то Митерев  счетовод. Если Набатов  счетовод, то Митерев  бухгалтер. Если Митерев  не кассир, то Левин  не счетовод. Если Левин  бухгалтер, то Набатов  счетовод. Кто какую должность занимает?

## Принцип решения

<!-- Опишите своими словами принцип решения задачи, приведите важные фрагменты кода. -->

Самая сложная часть решения заключалась в написании правильных предикатов и зависимостей. jobs() принимал имена и профессии, а предикат ! позволял отсекать сразу неверные варианты, не позволяя языку пытаться найти другие решения по умолчанию. Коим является последний предикат в списке, с пустыми именами, где условием выполнения являтся различие профессий.

```prolog
jobs("Митерев", V1, "Набатов", V3):-
    V3 = "Кассир", !,
    V1 = "Счетовод".
```

Данный предикат говорит нам о том, что если Набатов будет счетоводом тогда и только тогда когда Митереев Кассир. По такому принципу создаем предикаты описывающие все данные условия.

```prolog
res():-
    job(V1),
    job(V2),
    job(V3),
    V1 \= V2,
    V1 \= V3,
    V2 \= V3,
    jobs("Митерев", V1, "Левин", V2),
    jobs("Левин", V2,  "Набатов", V3),
    jobs("Митерев", V1, "Набатов", V3), !,
    write("Митерев"), tab(1), write(V1), nl,
    write("Левин"), tab(1), write(V2), nl,
    write("Набатов"), tab(1), write(V3), nl.
```

Функция распределяет по переменным различные профессии, дальше они отправляются на проверку каждый с каждым, если есть какое то особое условие, оно обрабатывается, если отсутствует, то последний предикат jobs проверяет на различие и выдает ответ. Дальше идет печать результата, каждой фамилии соответвутет его профессия.

## Выводы

Очень важно придумать систему предикатов, достаточную для решения задачи, нагромождение кода не делает решение лучше. Предикат !, как отсечение решений, очень помогает, без его использования программа уходит в страшные циклы и дает неоднозначный ответ. Но опять таки его надо использовать с умом. Как и в предыдущей лабораторной помогает режим trace на swipl, где я работаю, очень часто программа проваливалась на странных услових, выдавая неожиданные результаты, приходилось подставлять вручную условия.

Перед тем как начать решать эту задачу на машине, я на листочке проработал сетку вариантов, чтобы потом сравнивать ответ машины на задачу, и когда я спустя время получил ответ как на листке, я задумался, как легче стало мыслить в логичском ключе, возможно, дальше будет легче и веселее, особенно когда начинаешь понимать язык.

<!-- Сформулируйте *содержательные* выводы по лабораторной работе. Чему она вас научила? Над чем заставила задуматься? Помните, что несодержательные выводы -
самая частая причина снижения оценки за лабораторную. -->