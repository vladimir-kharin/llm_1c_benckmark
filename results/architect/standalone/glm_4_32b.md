# Архитектура самостоятельной конфигурации 1С для учета задач разработчиков 1С

## Состав объектов

### 1. Номенклатура (Тип задачи)
- **Реквизиты**:
  - Наименование (Строка)
  - Код (Строка)
  - Описание (Строка)
  - Время выполнения (Число)
  - Стоимость (Число)
- **Характеристики**:
  - Тип задачи (Репетиционный, Производственный, Обучение)

### 2. Контрагенты
- **Реквизиты**:
  - Наименование (Строка)
  - ИНН (Строка)
  - КПП (Строка)
  - Адрес (Строка)

### 3. Планировщик задач
- **Реквизиты**:
  - Номенклатура (Тип задачи)
  - Пользователь (Сотрудник)
  - Период выполнения (Дата)
  - Статус (Новые, В работе, Выполненные, Отклоненные)
  - Причина отклонения (Строка)
- **Характеристики**:
  - Плановое время выполнения (Число)
  - Фактическое время выполнения (Число)

### 4. Учет времени
- **Реквизиты**:
  - Планировщик задач (Название задачи)
  - Пользователь (Сотрудник)
  - Время начала (Дата и время)
  - Время окончания (Дата и время)
  - Итоговое время (Число)

### 5. Учет стоимости
- **Реквизиты**:
  - Контрагент (Клиент)
  - Планировщик задач (Название задачи)
  - Стоимость задачи (Число)
  - Датаinvoices (Дата)

### 6. Сотрудники
- **Реквизиты**:
  - Наименование (Строка)
  - Должность (Строка)
  - Контактные данные (Строка)

## Взаимосвязи

- **Планировщик задач** связан с **Номенклатурой** (Тип задачи) через реквизит "Номенклатура".
- **Планировщик задач** связан с **Сотрудниками** через реквизит "Пользователь".
- **Учет времени** связан с **Планировщиком задач** через реквизит "Планировщик задач".
- **Учет стоимости** связан с **Планировщиком задач** через реквизит "Планировщик задач".
- **Учет стоимости** связан с **Контрагентами** через реквизит "Контрагент".

## Отчеты

### 1. Отчет о выполненных задачах
**Формирование**:
- Использовать данные из **Планировщика задач** с фильтром по статусу "Выполненные".
- Включить данные о **Сотрудниках**, **Номенклатуре**, плановом и фактическом времени выполнения.

### 2. Отчет о не выполненных задачах
**Формирование**:
- Использовать данные из **Планировщика задач** с фильтром по статусу "Отклоненные".
- Включить данные о причине отклонения и **Сотрудниках**.

### 3. Отчет о времени выполнения задач
**Формирование**:
- Использовать данные из **Учета времени**.
- Включить информацию о начале и конце выполнения задачи, итоговое время и **Сотрудниках**.

### 4. Отчет о стоимости выполненных задач
**Формирование**:
- Использовать данные из **Учета стоимости**.
- Включить информацию о **Контрагентах**, **Планировщике задач**, стоимости задачи и датеinvoices.

### 5. Отчет о загруженности сотрудников
**Формирование**:
- Использовать данные из **Планировщика задач** и **Учета времени**.
- Включить информацию о задачах, поставленных **Сотрудникам**, плановом и фактическом времени выполнения, а также статусе задач.

### 6. Отчет о финансовых показателях
**Формирование**:
- Использовать данные из **Учета стоимости**.
- Включить общую сумму по всем клиентам, общую сумму по каждому клиенту, и детализацию по задачам.

## Заключение
Данная архитектура позволяет организовать планирование, учет времени, стоимости задач для клиента и контроль выполнения задач разработчиками 1С. Она предоставит руководителю и сотрудникам инструменты для эффективного управления проектами и ресурсов.
