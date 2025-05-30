## Архитектура расширения для учета задач специалистов 1С в УТ 11

### 1. Использование типовых объектов

Для учета задач специалистов 1С можно использовать следующие типовые объекты УТ 11:

* **Бизнес-процесс "Задание"**: можно использовать для создания задач и отслеживания их выполнения.
* **Задача исполнителя**: можно использовать для назначения задач исполнителям и контроля их выполнения.
* **Справочники**: можно использовать для хранения информации о задачах, исполнителях и статусах задач.

### 2. Дополнительные объекты и их реквизиты

Для учета задач специалистов 1С потребуются следующие дополнительные объекты:

* **Справочник "Задачи"**: для хранения информации о задачах.
	+ Реквизиты: наименование, описание, исполнитель, статус, дата начала, дата окончания.
* **Справочник "Исполнители"**: для хранения информации об исполнителях задач.
	+ Реквизиты: наименование, контактная информация.
* **Документ "Отчет о выполнении задачи"**: для регистрации выполнения задач.
	+ Реквизиты: задача, исполнитель, дата выполнения, описание выполнения.

### 3. Использование бизнес-процесса "Задание"

Бизнес-процесс "Задание" можно использовать для создания задач и отслеживания их выполнения. Для этого необходимо:

1. Создать новый бизнес-процесс "Задание" для каждой задачи.
2. Назначить исполнителя задачи в бизнес-процессе.
3. Установить статус задачи в бизнес-процессе.
4. Отслеживать выполнение задачи через бизнес-процесс.

### 4. Необходимые отчеты

Для контроля выполнения задач необходимы следующие отчеты:

* **Отчет "Список задач"**: для вывода списка задач с их статусами и исполнителями.
* **Отчет "Выполнение задач"**: для вывода информации о выполнении задач, включая дату выполнения и описание выполнения.
* **Отчет "Загруженность исполнителей"**: для вывода информации о загруженности исполнителей задачами.

Отчеты можно формировать на основе данных справочников и документов, созданных в рамках расширения.