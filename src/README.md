## Соревнование агентов

### Правила
1. Соревнование проводится в виде турнира. Каждый играет с каждым N партий за белых и черных.
2. За победу начисляется 3 балла, ничья стоит 1 балл.
3. В случае ошибки времени исполнения игроку засчитывается поражение.
4. Время на ход ограничено сверху T.
5. Игра не может длиться более M ходов.
6. Для определения победителя могут проводиться дополнительные партии.

N = 3 партии, T = 10 секунд, M = 60 ходов


### Подготовка среды
Агенты будут запускаться в virtualenv, созданной с помощью [anaconda](https://www.continuum.io/DOWNLOADS).
Поэтому необходимо указать зависимости в файле requirements.txt.
```
python=3.5.0
numpy=1.12.1
tensorflow=1.0.1
keras
```
Если версия указана явно, то используется самая свежая. Возможно использовать конкретный интерпретатор.
Лучше всего поставить себе пакет anaconda. И убедиться в работоспособности вашего кода.
```
conda create --copy --file requirements.txt --mkdir --prefix /home/dasimagin/envs/TEST 
```

Если для запуска агента вам нужны какие-то дополнительне шаги, 
то их исполнение должно запускаться простой командой make. Для сборки будет предоставлен компилятора gcc 4.8.4.

### Устройство агента
Агент будет запускаться в виде отдельного python процесса.
Комуникация со средой будет вестись через потоки sys.stdout и sys.stdin, которые через pipe подключены к мастер-процессу.
Как следствие, ваша программа не должна делать какой-либо стандартный ввод вывод.
Для логирования используйте запись в файл.

Вся работа проходит всего через две функции,
```
backend.wait_for_game_update()
backend.move(m)
```
первая делает блокирующий вызов и возвращает объект игры. Вторая делает ход, где m - строка в формате 'h10'.

Пример агента, который делает случайные ходы можно найти [здесь](https://github.com/dasimagin/renju/blob/master/src/dummy.py).


