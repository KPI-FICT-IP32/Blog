---
layout: post
title: "Лекція 5. Тест-план"
date: 2016-10-13 10:56:04 +0300
categories: kpi_s07_sw_quality
---


Існує стандарт для тестової документації: [IEEE829](https://en.wikipedia.org/wiki/Software_test_documentation)

(Title, Author, Date created, Date modified, Content, Revision history)

1. **Introduction**
2. **Features to be tested**
   - launch app
   - open doc
   - save changes
   - fonts
   - ...
3. **Features not to be tested**
4. **Test Items** -- тут декомпозиція того, що ми будемо тестувати. Розглядаємо пункти Features to be tested дуже детально. Наприклад:
   - launch app
     - launch app on iPhone
     - launch app on Android
     - launch app on Linux
     - ...
   - open doc
     - open doc with double click
     - open doc from within app
     - ...
   - ...
5. **Test approaches.** Детальний опис того, яким чином буде проводитися тестування:

   > Для кожного білда ми проводитимо smoke-testing. Щоб пришвидшити його, використовуємо автотести на Selenium Web-Driver. Тестуємо black-box способом. Потім додатково проганяємо unit-tests ...
6. **Pass/Fail item criteria** (acceptance criteria) I.E.
   - Tested on no less than 3 platforms;
   - All req are covered with all positive and no less than 2 negative tests
   - All defects with Blocker, Critical priority are fixed
   - No more than 2 medium priority defects
   - No more than 5 minor priority defects
   - ...
7. **Suspension/Resumption criteria** -- умови призупинення/продовження тестування.
8. **Environmental needs**
9. **Staff and training needs**
10. **Tester's tasks** -- Задачі тестувальника. Це більше як список обов'язків, яким, якщо що, можна прикрити 5ту точку.
11. **Test deliverables**
   - test plan
   - test case
   - test report
   - list of bugreports
   - test automation framework
   - ...
12. **Schedule** -- графік, що коли треба робити.

       | stage        | dates              |
       |--------------|--------------------|
       |analysis      | 12/10/16           |
       |test planning | nov 2016           |
       |test design   | ...                |
       |test execution| ...                |
       |regression    | ...                |
       |acceptance    |1/2/2017 - 20/2/2017|
       |reporting     | ...                |

13. **Responsibilities**

       | Who      | What          | Responsibilities            |
       |----------|---------------|-----------------------------|
       | Zhora    | manual QA     | test design, manual testing |
       | Vasya    | middle QA     | manual testing, reports     |
       | Sergey   | QA Automation | ...                         |

14. **Approvals**

       | Name  | Position | Date | Sign |
       |-------|----------|------|------|
       | Vlad  | PO       | now  | vlad |

15. **Risks** Risks and how to deal with them.
   - Accepts
   - Transfer
   - Mitigate
   - Avoid
