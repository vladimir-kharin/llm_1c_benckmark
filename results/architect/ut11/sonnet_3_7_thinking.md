# Архитектура расширения для учета задач специалистов 1С в ИТ-отделе (УТ 11)

## 1. Использование типовых объектов УТ 11

### Бизнес-процесс "Задание"
Бизнес-процесс "Задание" станет основой для учета задач специалистов 1С:
* Задания будут использоваться для постановки, назначения и контроля выполнения задач
* Позволит отслеживать сроки выполнения работ
* Обеспечит маршрутизацию согласно ролевой модели ИТ-отдела

### Справочник "Пользователи"
* Для учета специалистов 1С, выполняющих задачи
* Привязка пользователей к задачам для контроля выполнения

### Справочник "ГруппыИсполнителейЗадач"
* Для организации структуры ИТ-отдела (разработчики, консультанты и т.д.)
* Позволит распределять задачи по группам специалистов

### Справочник "РолиИсполнителей"
* Определение ролей сотрудников в процессе выполнения задач (исполнитель, проверяющий, постановщик)

### Задача "ЗадачаИсполнителя"
* Для создания задач исполнителям и контроля их выполнения

### Документ "Встреча"
* Может использоваться для планирования и учета совещаний по проектам
* Удобно для фиксации совещаний команды разработки

### Информационный регистр "ИсполнителиЗадач"
* Определяет связь между исполнителями и задачами

## 2. Дополнительные объекты для расширения

### Справочники

#### Справочник "ИТ_ТипыЗадач"
* **Реквизиты:**
  * Наименование
  * Описание
  * НормативноеВремя (Число)
  * ТребуетТестирования (Булево)
  * КатегорияСложности (ПеречислениеСсылка.ИТ_КатегорииСложности)

#### Справочник "ИТ_Проекты"
* **Реквизиты:**
  * Наименование
  * Описание
  * ДатаНачала (Дата)
  * ПлановаяДатаЗавершения (Дата)
  * ФактическаяДатаЗавершения (Дата)
  * Статус (ПеречислениеСсылка.ИТ_СтатусыПроектов)
  * Заказчик (СправочникСсылка.Контрагенты)
  * Руководитель (СправочникСсылка.Пользователи)
* **Табличная часть "Этапы":**
  * Наименование
  * ДатаНачала (Дата)
  * ДатаОкончания (Дата)
  * Ответственный (СправочникСсылка.Пользователи)
  * Статус (ПеречислениеСсылка.ИТ_СтатусыЭтаповПроектов)

#### Справочник "ИТ_ПриоритетыЗадач"
* **Реквизиты:**
  * Наименование
  * Описание
  * Вес (Число)
  * ЦветПриоритета (ХранилищеЗначения)

### Документы

#### Документ "ИТ_УчетВремени"
* **Реквизиты:**
  * Дата (Дата, время)
  * Номер
  * Специалист (СправочникСсылка.Пользователи)
  * Проект (СправочникСсылка.ИТ_Проекты)
  * Комментарий
* **Табличная часть "Работы":**
  * Задача (БизнесПроцессСсылка.Задание)
  * ТипРаботы (СправочникСсылка.ИТ_ТипыЗадач)
  * ВремяНачала (Дата, время)
  * ВремяОкончания (Дата, время)
  * ЗатраченноеВремя (Число)
  * Результат (Строка)

### Регистры

#### Регистр накопления "ИТ_ЗатратыВремени"
* **Измерения:**
  * Период (Дата)
  * Специалист (СправочникСсылка.Пользователи)
  * Задача (БизнесПроцессСсылка.Задание)
  * Проект (СправочникСсылка.ИТ_Проекты)
  * ТипРаботы (СправочникСсылка.ИТ_ТипыЗадач)
* **Ресурсы:**
  * ЗатраченноеВремя (Число)
  * ПлановоеВремя (Число)

#### Регистр сведений "ИТ_СостоянияЗадач"
* **Измерения:**
  * Период (Дата, время)
  * Задача (БизнесПроцессСсылка.Задание)
* **Ресурсы:**
  * Состояние (ПеречислениеСсылка.ИТ_СостоянияЗадач)
  * Исполнитель (СправочникСсылка.Пользователи)
  * Комментарий (Строка)

### Перечисления

#### Перечисление "ИТ_СостоянияЗадач"
* Зарегистрирована
* Назначена
* ВРаботе
* ОжиданиеДанных
* Приостановлена
* НаПроверке
* Выполнена
* Отменена

#### Перечисление "ИТ_СтатусыПроектов"
* Планирование
* ВРазработке
* Тестирование
* Внедрение
* Завершен
* Отменен

#### Перечисление "ИТ_КатегорииСложности"
* Легкая
* Средняя
* Сложная
* Критичная

## 3. Использование типового бизнес-процесса "Задание"

### Расширение бизнес-процесса "Задание"
В расширении для бизнес-процесса "Задание" добавляются следующие реквизиты:

* **ИТ_ТипЗадачи** (СправочникСсылка.ИТ_ТипыЗадач)
* **ИТ_Приоритет** (СправочникСсылка.ИТ_ПриоритетыЗадач)
* **ИТ_Проект** (СправочникСсылка.ИТ_Проекты)
* **ИТ_ЭтапПроекта** (Строка)
* **ИТ_ПлановаяДлительность** (Число)
* **ИТ_ФактическаяДлительность** (Число)
* **ИТ_Статус** (ПеречислениеСсылка.ИТ_СостоянияЗадач)
* **ИТ_ДатаНачалаРабот** (Дата, время)
* **ИТ_ДатаЗавершенияРабот** (Дата, время)

### Точки маршрута бизнес-процесса "Задание"

В типовом бизнес-процессе "Задание" имеется следующий маршрут:
1. **Выполнить** - начальная точка маршрута
2. **Проверить** - точка проверки выполнения
3. **Исправить** - точка доработки (при необходимости)

Для ИТ-отдела дополним этот процесс:
1. **ИТ_Зарегистрировать** - регистрация задачи
2. **ИТ_Назначить** - назначение исполнителя
3. **ИТ_Выполнить** - выполнение задачи
4. **ИТ_Проверить** - проверка результатов
5. **ИТ_Исправить** - доработка (при необходимости)
6. **ИТ_Завершить** - завершение задачи

### Особенности использования
* При создании задачи автоматически заполняются поля ИТ_ПлановаяДлительность на основе типа задачи
* На каждом этапе выполнения задачи меняется значение ИТ_Статус
* При взятии в работу фиксируется ИТ_ДатаНачалаРабот
* При завершении фиксируется ИТ_ДатаЗавершенияРабот и ИТ_ФактическаяДлительность
* Реализуется механизм оповещений при нарушении сроков или изменении статуса задачи

## 4. Необходимые отчеты

### Отчет "ИТ_ТекущиеЗадачи"
* **Назначение:** мониторинг текущих задач ИТ-отдела
* **Параметры:**
  * Период
  * Исполнитель
  * Проект
  * Статус
  * Приоритет
* **Формирование:**
  * На основе данных бизнес-процесса "Задание" с фильтрацией по статусам
  * Группировка по исполнителям, проектам, приоритетам
* **Выводимые данные:**
  * Список задач с указанием исполнителя, проекта, срока
  * Статус выполнения
  * Процент завершения

### Отчет "ИТ_АнализЗагруженностиСпециалистов"
* **Назначение:** анализ рабочего времени и загруженности специалистов
* **Параметры:**
  * Период
  * Специалист(ы)
  * Проект(ы)
* **Формирование:**
  * На основе регистра накопления "ИТ_ЗатратыВремени"
  * Группировка по специалистам, проектам, дням/неделям
* **Выводимые данные:**
  * Затраченное время по специалистам
  * Распределение времени по типам задач и проектам
  * Графики загруженности
  * Сравнение с нормативами

### Отчет "ИТ_ПрогрессПроектов"
* **Назначение:** контроль выполнения проектов
* **Параметры:**
  * Период
  * Проект(ы)
* **Формирование:**
  * На основе данных по задачам, сгруппированным по проектам
  * Учет статусов и фактического времени выполнения
* **Выводимые данные:**
  * Процент выполнения проекта
  * Соотношение план/факт по времени
  * Прогноз даты завершения
  * Диаграмма Ганта по этапам проекта

### Отчет "ИТ_ЭффективностьРаботы"
* **Назначение:** анализ эффективности работы специалистов
* **Параметры:**
  * Период
  * Специалист(ы)
  * Тип задач
* **Формирование:**
  * Сопоставление плановой и фактической длительности выполнения задач
  * Анализ своевременности выполнения
* **Выводимые данные:**
  * Показатель эффективности (соотношение план/факт)
  * Процент задач, выполненных в срок
  * Динамика эффективности по периодам

### Отчет "ИТ_ПросроченныеЗадачи"
* **Назначение:** контроль просроченных задач
* **Параметры:**
  * На дату
  * Исполнитель
  * Проект
* **Формирование:**
  * Выборка задач с просроченным сроком выполнения
  * Расчет длительности просрочки
* **Выводимые данные:**
  * Список просроченных задач с указанием приоритета
  * Длительность просрочки
  * Ответственный исполнитель
  * Критичность (оценка на основе приоритета и длительности просрочки)

Данная архитектура расширения для УТ 11 позволит эффективно организовать учет задач специалистов 1С в ИТ-отделе компании, обеспечит планирование, учет времени и контроль выполнения задач.