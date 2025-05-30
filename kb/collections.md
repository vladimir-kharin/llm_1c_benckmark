### Коллекции-контейнеры 1С

---

## Массив

```1c
// Создание
М = Новый Массив;              // пустой
// Добавление в начало
М.Вставить(0,"А"); М.Вставить(0,"Б"); // (Б, А)

// Последний индекс (-1, если пуст)
Конец = М.ВГраница();          // 1

// Доступ
Первый = М[0];                 // "Б"

// Поиск / удаление
Инд = М.Найти("А");            // 1
Если Инд <> Неопределено Тогда
    М.Удалить(Инд);            // (Б)
КонецЕсли;

// Перебор
Для Инд = 0 По М.ВГраница() Цикл
    Сообщить(М[Инд]);
КонецЦикла;

// Очистка
М.Очистить();
```

---

## Соответствие

*ассоциативный массив «ключ-значение»*

```1c
// Создание и наполнение
Параметры = Новый Соответствие;
Параметры.Вставить("Фонд", 5000);
Параметры.Вставить("ДатаРег", '19990417');

// Чтение
Фонд = Параметры.Получить("Фонд"); // 5000

// Проверка существования
Если Параметры.Получить("ДатаРеорг") = Неопределено Тогда
    Сообщить("Реорганизации не было");
КонецЕсли;

// Изменение / добавление
Параметры.Вставить("Проверка", '20031104');

// Цикл по парам
Для каждого Эл Из Параметры Цикл
    Сообщить(Эл.Ключ + " / " + Эл.Значение);
КонецЦикла;

// Служебные операции
ЧислоЭл = Параметры.Количество(); // 3
Параметры.Удалить("Проверка");
Параметры.Очистить();
```

---

## Структура

*фиксированные именованные поля (JSON-look-alike)*

```1c
// Способ 1: строка имён + значения
Клиент = Новый Структура(
    "Имя,ДатаРег,Сотрудники",
    "ОАО ""Савушкин продукт""", '19961230', 3120);

// Способ 2: пустая + Вставить
Клиент = Новый Структура;
Клиент.Вставить("Имя","ОАО ""Савушкин продукт""");
Клиент.Вставить("Сайт","savushkin.by");

// Доступ как к полям объекта
Клиент.Сотрудники = 3584;
Телефон = Клиент.НомерТелефона;

// Итерация
Для каждого Пара Из Клиент Цикл
    Сообщить(Пара.Ключ + ": " + Пара.Значение);
КонецЦикла;

// Служебные
Всего = Клиент.Количество();
Клиент.Удалить("Сайт");
Клиент.Очистить();
```

---

## ТаблицаЗначений

*двумерная «in-memory» таблица, близка к SQL‐таблице*

```1c
// --- Создание таблицы и колонок
ТЗ = Новый ТаблицаЗначений;
ТЗ.Колонки.Добавить("Название");
ТЗ.Колонки.Добавить("Автор");
ТЗ.Колонки.Добавить("Жанр");

// --- Добавление строк (2 равнозначных способа)
Стр = ТЗ.Добавить();                 // способ 1
Стр.Название = "Война и мир";  Стр.Автор = "Толстой";  Стр.Жанр = "Роман";

Стр = ТЗ.Добавить();                 // способ 2
Стр["Название"] = "Преступление и наказание";
Стр["Автор"] = "Достоевский";
Стр["Жанр"] = "Драма";

// --- Работа с колонками
КолНазваний = ТЗ.ВыгрузитьКолонку("Название"); // → Массив
ТЗ.ЗагрузитьКолонку(КолНазваний,"Название");   // idempotent

// --- Массовая запись
ТЗ.ЗаполнитьЗначения("","Жанр");          // очистили жанр

// --- Поиск
СтрНайдено = ТЗ.Найти("Преступление и наказание");        // по первой колонке
Если СтрНайдено <> Неопределено Тогда
    Сообщить(СтрНайдено.Автор);           // Достоевский
КонецЕсли;

// поиск по нескольким колонкам
Фильтр = Новый Структура("Автор","Достоевский");
КнигиАвтора = ТЗ.НайтиСтроки(Фильтр);  // → Массив строк таблицы

// --- Итоги, сортировка, свёртка
КолСтраниц = ТЗ.Итог("Страниц");              // сумма
ТЗ.Сортировать("Автор, Название");           // множественный сорт
ТЗ.Свернуть("Автор","Страниц");         // групп. + агрег.

// --- Сдвиг строк
ТЗ.Сдвинуть(0,1);  // строка 0 → позиция 1

// --- Копии
КопияПолная   = ТЗ.Скопировать();
КопияКолонок  = ТЗ.СкопироватьКолонки("Название, Автор");  // пустая таблица с теми же колонками
КопияОтбора   = ТЗ.Скопировать(Фильтр);

// --- Удаление
ТЗ.Удалить(0);     // по индексу
ТЗ.Очистить();     // все строки
```