# architecture-future_2_0
Задание к спринту 11 ("Построение архитектуры данных и технологические тренды")

## Описание кейса «Будущее 2.0».

### О компании
Компания «Будущее 2.0» начиналась как медицинский стартап. Со временем он стал успешным. Теперь, чтобы ставить диагнозы и назначать лечение, врачи используют новейшее оборудование и ИИ. Не так давно компания купила банк, чтобы оказывать своим клиентам финансовые услуги. А сейчас она собирается интегрировать в свою систему несколько фармацевтических компаний и компанию, которая производит электронику для медицинского оборудования.   

Исторически все данные в компании «Будущее 2.0» лежали в DWH. Его построили на базе SQL-сервера с большим количеством бизнес-логики и интерфейсом на Power Builder для прямой работы операторов в клиниках.   

В DWH лежат:
- Данные по клиентам.
- Медицинские карты и истории болезни, в том числе — данные исследований, выполненных в ходе лечения.
- Финансовая история.
- Счета.
- Данные о кредитах.
- Данные по персоналу больницы.
- Данные по инвентаризации.
- Финансовая отчётность и много другой информации.   
   
Бизнес хочет развивать все направления независимо, но в то же время иметь единую картину по бизнес-показателям. При этом уже сейчас нужную отчётность сложно построить за разумное время: очень много данных (сотни терабайт) и вариантов их использования. Это порождает большое количество трансформаций, что в свою очередь замедляет time-to-market и приводит к снижению производительности. В итоге сложные отчёты можно ждать часами.   
    
Руководство поставило перед вами две задачи. Нужно:
1. **Сделать удобную «витрину данных».** Это портал самообслуживания, который легко масштабировать вне зависимости от количества бизнесов и их бизнес-целей. По задумке, сотрудник может получить здесь отчёт по любым срезам, которые выберет, если это позволяет его уровень доступа. Ещё нужно добавить возможность конструировать отчёты самостоятельно. Обратите внимание: в витрину данных не нужно добавлять медицинские карты, истории болезней и результаты медицинских исследований. Эти данные компания не будет использовать для аналитики.   
2. **Предоставить архитектурное решение по изменению IТ-ландшафта в области работы с данными.** Оно должно предусматривать интеграцию новых бизнесов без дописывания огромного количества бизнес-логики в DWH.   

Бизнес разрешил при необходимости отказаться от легаси-систем и мигрировать на новые сервисы, если вы предоставите весомое обоснование.

#### Лендскейп компании

**В структуре компании выделяются четыре подразделения:**
- Головной офис.
- Клиники.
- ИИ-сервисы для работы с медицинскими данными в виде отдельной компании.
- Финтех-сервисы в виде отдельной компании с банковской лицензией.   
   
**В рамках кейса нужно поработать с такими продуктами:**
- Финтех-сервисы.
- Внутренняя медицинская система-DWH с клиентским интерфейсом и дополнительной бизнес-логикой под финтех- и ИИ-сервисы.
- Много кастомизаций BI-системы поверх DWH.
- ИИ-сервисы для работы с медицинскими данными.
- Слой интеграций через старую шину данных.   

**Сейчас развёрнуты такие технологии, сервисы и приложения:**
- DWH на базе Microsoft SQL-сервера 2008 года.
- Power BI.
- Power Builder.
- Шина на базе Apache Camel.
- ИИ-сервисы на Python.
- Финтех-сервисы на Golang и Java.
   
Так выглядят потоки данных в компании:
![](потоки_данных.png)

### Цели бизнеса

- **Промежуточное состояние (через пару месяцев).**  Сформировано архитектурное решение по трансформации. Уточнены границы доменов и связи между ними. Запланированы конкретные проекты в доменах по развитию «витрины данных».
- **Финальное состояние (через год).** Реализован портал самообслуживания. Бизнес-пользователи в доменах могут использовать данные в рамках новой архитектуры. На этом этапе можно на некоторое время сохранить легаси-системы в отдельных доменах.
   
В рамках проектной работы вы поработаете над промежуточным состоянием. Финальное состояние — за пределами ваших текущих задач, но его нужно учитывать для принятия решений.


## Задачи

### Задание 1

1. **Спроектируйте архитектуру системы через год.** Составьте диаграмму контейнеров в модели C4.
2. **Опишите проблемные места.** Сделайте это в удобной для вас форме. Например, можете использовать список или таблицу. Постарайтесь формулировать описания так, чтобы они были понятны не только инженерам, но и бизнесу.
3. **Приоритизируйте выявленные проблемы.** Для этого вы можете использовать методы, которые изучили на курсе. Например, MoSCoW или матрицу Эйзенхауэра.

**Решение:**
- [Диаграмма контейнеров](Task1/container_diagram.drawio)
- [Диаграмма контейнеров в формате PNG](Task1/container_diagram.png)
- [Проблемные места и приоритизация проблем](Task1/problems.md)

### Задание 2

1. **Разделите систему на домены**, чтобы их можно было независимо развивать без необходимости реализовать новую логику в DWH.
2. **Отразите потоки данных между доменами.** Для этого отрисуйте Data Flow Diagram. Отразите на ней запланированные изменения в архитектуре.
3. **Аргументируйте логику разделения на домены.** Опишите преимущества, которые получит компания, если разделит систему на домены так, как вы предлагаете.
   
**Решение:**
- [Data Flow Diagram](Task2/DFD.drawio)
- [Data Flow Diagram в формате PNG](Task2/DFD.png)
- [Логика разделения на домены](Task2/arguments.md)

### Задание 3

1. **Сформируйте технический радар.** Отразите на нём текущие технологии и методологии, а также предлагаемые изменения и технологии, которые сопутствуют основному стеку. Оформите радар в виде таблицы или круговой диаграммы.
2. **Составьте роадмап.** Отразите здесь изменения в технологическом ландшафте компании. Радар должен содержать этапы, их результаты, ответственные команды и ресурсы, которые потребуются. Оформите роадмап в draw.io или в другом инструменте на свой выбор.
3. **Обоснуйте изменения.** Опишите, зачем нужен каждый из этапов, которые вы включили в роадмап. Можете сделать это в том же файле, что и сам артефакт.
   
**Решение:**
- [Технический радар](Task3/techradar.md)
- [Роадмап](Task3/roadmap.drawio)
- [Роадмап в формате PNG](Task3/roadmap.png)
- [Аргументация](Task3/argumentation.md)

