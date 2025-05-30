# Анализ решений моделей

## Llama 4 Scout
- **Понимание метаданных 1С** – модель использует справочники, документы и перечисления, однако полностью игнорирует регистры. (3/5)
- **Механизмы учёта** – описаны лишь сами документы, без движения по регистрам и без ссылок на механизмы проведения. (1/5)
- **Отчётность** – приведён перечень отчётов с параметрами и выходными таблицами, но без указания источников данных/СКД. (3/5)
- **Полнота решения** – покрыты все необходимые аспекты (планирование, время, стоимость, контроль), но на концептуальном уровне. (4/5)

## Llama 4 Maverick
- **Понимание метаданных 1С** – корректно разделяет справочники, документы и два регистра. (4/5)
- **Механизмы учёта** – явно прописан регистр накопления «Время…» и регистр сведений «Стоимость часа», что даёт основу для проведения документов. (4/5)
- **Отчётность** – описаны три отчёта, указаны источники (документы, регистры), но без деталей виртуальных таблиц. (3/5)
- **Полнота решения** – все требования промпта отражены. (4/5)

## DeepSeek R1
- **Понимание метаданных 1С** – использует справочники, документы, информационный и накопительный регистр, а также план видов характеристик. (4/5)
- **Механизмы учёта** – наличие регистра истории статусов и расчётов стоимости на основании документа «УчётВремени» демонстрирует продуманные движения. (4/5)
- **Отчётность** – четыре отчёта с алгоритмами формирования, подчёркнута работа с запросами; СКД не упомянуто, но структура отчётов проработана. (4/5)
- **Полнота решения** – охватывает все аспекты, добавлены уведомления, контроль бюджета, интеграции. (5/5)

## Qwen 3 32B
- **Понимание метаданных 1С** – описание не указывает типы объектов (справочник/документ/регистр), используются обобщённые таблицы. (2/5)
- **Механизмы учёта** – регистры и движения документов не описаны. (1/5)
- **Отчётность** – отчёты детализированы, но не указаны источники данных (регистры, виртуальные таблицы). (2/5)
- **Полнота решения** – большая детализация, охватывает роли, интеграции, методы. (4/5)

## GLM 4 32B
- **Понимание метаданных 1С** – объекты названы нетипично, отсутствует явное разделение на справочники и документы. (2/5)
- **Механизмы учёта** – отсутствует описание движений и регистров. (1/5)
- **Отчётность** – отчёты перечислены без привязки к регистрам. (2/5)
- **Полнота решения** – основные требования соблюдены, но меньше детализации процессов учёта. (4/5)

## Gemma 3 27B
- **Понимание метаданных 1С** – классическая структура справочников и документов с перечислениями; регистры отсутствуют. (4/5)
- **Механизмы учёта** – базируется на документе «Учет времени», но без регистров движения; механизм расчётов не уточнён. (3/5)
- **Отчётность** – широкий перечень отчётов, есть расчёт прибыли, диаграмма Ганта, однако не указан источник данных (СКД/запросы). (3/5)
- **Полнота решения** – решение наиболее содержательное, включает расширения и рекомендации. (5/5)

### Сводная таблица оценок

| Модель | Понимание метаданных 1С | Механизмы учёта | Отчётность | Полнота решения | Итог |
| --- | --- | --- | --- | --- | --- |
| Llama 4 Scout | 3 | 1 | 3 | 4 | 11 |
| Llama 4 Maverick | 4 | 4 | 3 | 4 | 15 |
| DeepSeek R1 | 4 | 4 | 4 | 5 | 17 |
| Qwen 3 32B | 2 | 1 | 2 | 4 | 9 |
| GLM 4 32B | 2 | 1 | 2 | 4 | 9 |
| Gemma 3 27B | 4 | 3 | 3 | 5 | 15 |
