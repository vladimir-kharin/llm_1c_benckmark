# Архитектура расширения УТ 11 для учета задач ИТ-отдела

## 1. Типовые объекты и их использование

### Каталоги:
- **ГруппыИсполнителейЗадач**:
  - Для группировки сотрудников ИТ-отдела (например: "Разработчики", "Администраторы").
- **ЗадачиПроектов**:
  - Базовый объект для создания задач. Добавить реквизиты:
    - `ТипЗадачи` (ссылка на новый справочник "ТипыЗадачИТ"),
    - `Трудозатраты` (план/факт),
    - `СрокИсполнения`.

### Документы:
- **Задание** (бизнес-процесс):
  - Использовать для постановки задач с этапами: "Назначение", "В работе", "Проверка", "Завершено".

### Регистры:
- **Календари**:
  - Для планирования сроков задач и визуализации в виде диаграммы Ганта.
- **Накопительные регистры** (например, `ВыручкаИСебестоимостьПродаж`):
  - Адаптировать для учета трудозатрат (в часах/днях).

---

## 2. Дополнительные объекты

### Справочники:
- **ТипыЗадачИТ**:
  - Реквизиты: `Код`, `Наименование`, `Приоритет` (высокий/средний/низкий).
- **СтатусыЗадач**:
  - Значения: "Новая", "В работе", "На проверке", "Завершена", "Отменена".

### Документ **УчетВремени**:
  - Реквизиты:
    - `Задача` (ссылка на `ЗадачиПроектов`),
    - `Исполнитель` (ссылка на `ГруппыИсполнителейЗадач`),
    - `ВремяНачала`, `ВремяОкончания`,
    - `Комментарий`.

### Регистр накопления **Трудозатраты**:
  - Измерения: `Задача`, `Исполнитель`, `Дата`.
  - Ресурсы: `ЧасыФакт`, `ЧасыПлан`.

---

## 3. Использование бизнес-процесса "Задание"

- **Этапы**:
  1. **Постановка задачи**:
     - Автоматическое создание записи в `ЗадачиПроектов`.
  2. **Назначение ответственного**:
     - Привязка к `ГруппыИсполнителейЗадач`.
  3. **Контроль выполнения**:
     - Интеграция с документом `УчетВремени`.
  4. **Завершение**:
     - Проверка заполнения `Трудозатраты` и обновление `СтатусыЗадач`.

- **Уведомления**:
  - Оповещения о приближении дедлайна через `ВидыОповещенийКлиентам`.

---

## 4. Отчеты

### 1. **Отчет по загрузке сотрудников**:
  - Данные: Из регистра `Трудозатраты`.
  - Группировка: По исполнителям и датам.
  - Визуализация: График с планом/фактом времени.

### 2. **Статус задач по проектам**:
  - Данные: Из `ЗадачиПроектов` и `СтатусыЗадач`.
  - Фильтры: По типу задачи, приоритету, сроку.

### 3. **Отклонения от сроков**:
  - Использовать `Календари` и вычисляемые поля:
    ```1c
    Если СрокИсполнения < ТекущаяДата() И Статус <> "Завершена" Тогда "Просрочено"
    ```

### 4. **Диаграмма Ганта**:
  - На основе `ЗадачиПроектов` с привязкой к календарю.

---

### Схема взаимосвязей:
```
Задание → ЗадачиПроектов → УчетВремени → Трудозатраты
       ↓
СтатусыЗадач, ТипыЗадачИТ
```

**Интеграция с мобильным приложением**:
- Использовать `ВерсииМобильныхПриложений` для синхронизации данных по задачам в реальном времени.
