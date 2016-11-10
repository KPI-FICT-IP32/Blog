---
layout: post
title: "Лекція 7. Баг-репорт"
date: 2016-11-10 10:49:37 +0200
categories: kpi_s07_sw_quality
---

Bug Report -- документ, який описує дефект у застосунку.
Дефект/Баг -- невідповідність фактичного результату очікуваному.

Алгоритм поведінки при виявленні дефекту

1. Занотувати, що відбулося
2. Зробити скріншот або зняти невеликий скрінкаст; логи
3. відтворити (двічі або тричі) -- щоб зрозуміти, як часто відтворюється
4. Комунікація з командою (може хтось щось про це знає)
5. Пошук дуюблікатів у баг-трекері
6. Локалізація дефекту (аналіз потенційних факторів, які впливають на відтворюваність багу)
7. Пишемо Summary (заголовок/title). Хороший Summary відповідає на 3 питання:

   - Що?
   - Де?
   - Коли?

8. Пишемо Issue Description і заносимо в баг-трекер

Приклад:

```
Summary: 
    Changes in HTML doc currently opened is not saved
    when [Save] button is clicked in Text Edit app

Environment:
    OS: any (MacOS, Win)
    Browser: Chrome, Firefox, Safari, Opera, IE (version any)

Build (version):
    Text Edit v1.1.23b

Priority: Medium / Major (пріоритет з точки зору бізнеса)
Severity: Medium (пріоритет з технічної точки зору)

Description:

    Pre-condition (optional):
        существует файл формата HTML, который коректно открывается
        в браузере и он сейчас открыт в браузере в система

    Steps To Reproduce:
        1. Launch text editor
        2. Open any html file that was previously opened in browser
        3. Make any changes in content HTML document;
        4. Save changes in document
        5. Reload page in your browser
        6. Observe the result on screen in your browser

    Actual result:
        Changes are not saved, previous version of HTML doc is displayed.

    Expected Result: 
        The document is displayed without any corruptions
        and shows changes made during steps

    Additional info:
        if user closes browser and then click on [Save] button 
        in Text Edit app - changes saved successfully.
```
