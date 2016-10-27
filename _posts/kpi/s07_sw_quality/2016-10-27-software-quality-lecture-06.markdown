---
layout: post
title: "Лекція 6. Тестова документація"
date: 2016-10-27 10:20:00 +0300
categories: kpi_s07_sw_quality
---

Тестова документація:

1. Test plan
2. Test report
3. Test-case
4. Checklist

## Test-case

**Test-case** -- документ, що містить послідовність кроків для перевірки одного критерію.

Структура документу:

1. IDEA -- власне, мета test-case. Наприклад:

   > Проверить, как едет себя дверь комнаты 2-13 при попытке открыть её, не открыв замок

2. Title -- коротка назва документу. У зв'язку з тим, що у проектах зазвичай достобіса test-cases, є сенс якось осмислено і структуровано заповнювати це поле.

   > 2-13MDoorLockedOpen

3. Pre-condition (optional) -- описує дії, або умови, які не є частиною тесту, але є необхідними для його виконання

   > 1. The door is locked
   > 2. User is outside the room

4. Steps -- кроки тесту

   > 1. Подойди к двери
   > 2. Проверни дверную ручку по часовой
   > 3. Потяни дверь на себя 
   > 4. Посмотри состояние двери

5. Expected result

   > Дверь не открылась и осталась целой

6. (optional) Post-conditions -- кроки для "чистки" після тесту

Однією з переваг test-case є простота створення bug-report

## Checklist

Формат checklist:

| ID | Tester actions     | System Response (Expected result) |
|----|--------------------|-----------------------------------|
| 1  | Open the home page | Welcome text is displayed on top <br/> [menu][user][payments][settings] menu items are present <br/>Banner is displayed<br/>… |
| 2  | Click on [User] menu item | Window with buttons [Log In] and [Sign Up] is displayed on screen |
| 3  | Click on [Sign Up] button | "Registration: Step1" screen is opened; <br/> bla bla bla fields are displayed |
| 4  | Click on [Menu] >> Save as >> Save as pdf | … |
| …  | … | … |
