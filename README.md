# Учебный проект: игра Blackjack (aka Rubyjack)

## TODO
—

## Done
1. Продумать объектную модель игры и связи между объектами
1. Написать классы карты и колоды
1. Написать класс игрока
1. Написать класс игры
1. Написать класс интерфейса: запрос ввода игрока и вывод хода игры
1. Написать класс управления игрой
1. Перенести вывод игры в модуль интерфейса
1. Провести рефакторинг всех классов
1. Исправить замечания наставника

## Объектная модель игры
__1. Game__<br/>
  Основной цикл игры. Задаёт игроков, банк, ставку

__2. Round__<br/>
  Один раунд игры, принимает игроков, делает ходы, определяет победителя

__3. Player__<br/>
  Определяет параметры игрока: имя, банк. Запрашивает решение игрока.

__4. Dealer__<br/>
  Подкласс Player, автоматическое принятие решения на основе игровой логики

__5. Hand__<br/>
  Работа с картами игрока: карты, подсчёт очков, сброс

__6. Deck__<br/>
  Создаёт колоду карт, перетасовывает карты и сдаёт по одной

__7. Card__<br/>
  Определяет параметры карты: название и количество очков

__8. Интерфейс__<br/>
  Модуль для консольного ввод-вывода

## Механика и правила игры:

Есть игрок (пользователь) и дилер (управляется программой).
Вначале запрашиваем у пользователя имя, после чего начинается игра.
При начале игры у пользователя и дилера в банке находится по 100 долларов
Пользователю выдаются случайные 2 карты, которые он видит (карты указываем условными обозначениями, например, «К+» - король крестей, «К<3» - король черв, «К^» - король пик, «К<>» - король бубен и т.д. При желании, можете использовать символы юникода для мастей.)
Также 2 случайные карты выдаются «дилеру», против которого играет пользователь. Пользователь не видит карты дилера, вместо них показываются звездочки.
Пользователь видит сумму своих очков. Сумма считается так: от 2 до 10 - по номиналу карты, все «картинки» - по 10, **туз - 1 или 11, в зависимости от того, какое значение будет ближе к 21 и что не ведет к проигрышу (сумме более 21).**
После раздачи, автоматически делается ставка в банк игры в размере 10 долларов от игрока и диллера. (У игрока и дилера вычитается 10 из банка)
После этого ход переходит пользователю. У пользователя есть на выбор 3 варианта:
- __*Пропустить.*__ В этом случае, ход переходит к дилеру (см. ниже)
- __*Добавить карту.*__ (только если у пользователя на руках 2 карты). В этом случае игроку добавляется еще одна случайная карта, сумма очков пересчитывается, ход переходит дилеру. **Может быть добавлена только одна карта.**
- __*Открыть карты.*__ Открываются карты дилера и игрока, игрок видит сумму очков дилера, идет подсчет результатов игры (см. ниже).

Ход дилера (управляется программой, цель - выиграть, то есть набрать сумму очков, максимально близкую к 21). Дилер может:
- __*Пропустить ход* (если очков у дилера 17 или более)__. Ход переходит игроку.
- __*Добавить карту* (если очков менее 17)__. У дилера появляется новая карта (для пользователя закрыта). После этого ход переходит игроку. Может быть добавлена только одна карта.

Игроки вскрывают карты либо по достижению у них по 3 карты (автоматически), либо когда пользователь выберет вариант «Открыть карты». После этого пользователь видит карты дилера и сумму его очков, а также результат игры (кто выиграл и кто проиграл).
Подсчет результатов:

- Выигрывает игрок, у которого сумма очков ближе к 21
- Если у игрока сумма очков больше 21, то он проиграл
- Если сумма очков у игрока и дилера одинаковая, то объявляется ничья и деньги из банка возвращаются игрокам
- Сумма из банка игры переходит к выигравшему

После окончания игры, спрашиваем у пользователя, хочет ли он сыграть еще раз. Если да, то игра начинается заново с раздачи карт, если нет - то завершаем работу.
