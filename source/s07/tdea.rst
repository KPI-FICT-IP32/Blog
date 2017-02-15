=============================================
Технології розробки корпоративних застосувань
=============================================

:Лектор: Подрубайло Олександр Олександрович
:Сайт курсу: `Технологія Java EE <http://jee-comsys.blogspot.com/>`_

.. contents::
   :depth: 3
..

--------------

Лекція 1. JDBC. Servlets.
=========================
date: 2016-09-28 12:29:32 +0300

    Вы – жертвы экспериментальной программы

    © Подрубайло О. О.

JDBC
----

JDBC – Java Database Connectivity. JDBC – паттерн моста (bridge). Тут у
ролі реалізації виступають класи JDBC, а у ролі абстракції – застосунок,
який пише програміст.

Клієнт працює з базою в рамках транзакцій. Транзакції є атомарними
операціями. Транзакції задовольняють принципу ACID:

-  Atomic
-  Consistency
-  Isolation
-  Durability

На практиці ACID є доволі накладним, тому сучасні системи, що працюють з
розоділеними даними відовідають принципам BASE

-  Basicaly Availabile
-  ще щось там
-  Eventual Consistency

JDBC – це доволі проста і тупа штука, і вже не входить у склад JEE.

Схема роботи з JDBC:

#. Встановити з’єднання
#. Створити запит (statement)

   -  Statement – просто текст запиту
   -  PreparedStatement – готує запит із параметрами.
   -  CallableStatement – заздалегідь заготовані процедури. Ці процедури
      використовуються в базі, щоб оптимізувати виконання спеціальних
      запитів.

#. Отримати ResultSet

Як працювати із з’єднаннями
~~~~~~~~~~~~~~~~~~~~~~~~~~~

З’єднання – канал зв’язку користувача з базою. На одного користувача
виділяти одне з’єднання – погано. На одного клієнта (застосунок) треба
виділяти декілька з’єднань. Точна кількість з’єднань залежить від
великої кількості різних факторів. Зазвичай для реалізації декількох
з’єдннь використовується пул з’єднань (Connection pool).

Коли іде робота тільки з одним з’єднанням – це не дуже правильно.
З’єднання можуть перериватися по різних причинах.

Варіанти

-  на кожну транзакцію використовувати своє з’єднання і після транзакції
   закривати.
-  моніторити стан з’єднань і закривати вбиті

::

    +-----------------+
    |ConnectionManager|
    +-----------------+
    |+getConnection() |
    +-----------------+
             |
             |
    +-----------------+
    |       DAO       |
    +-----------------+
    |+findById()      |<---- // connManager.getConnection() 
    +-----------------+

Правильно у ``getConnection`` ловити помилки і у блоці ``catch`` кидати
``RuntimeException``, який кладе увесь застосунок. Логіка створення
з’єднання (можливого перестворення у випадку помилок, тощо) повинна бути
у менеджері з’єднань. **Цей підхід застосовний тільки для синхронних
операцій**.

Servlet
-------

    Сервлет – краєугольный камень веб-разработки на Java

Веб-контейнер – фігня, яка вміє прийняти ``war``, правильного його
встановити і запустити.

Коли Java тільки з’явилася і почала працювати з вебом, сервери були
слабкі і була точка зору, що Java-аплета буде достатньо. Проблеми
аплетів:

-  працюють на стороні клієнта, а значить клієнт при бажанні може їх
   модифікувати
-  jar-файли великі (особливо, якщо там багато залежностей)

Servlet виконується тільки на сервері, повертає веб-контейнеру
ServletResponse, а веб-контейнер повертає читабельну для користувача
інформацію без java-коду і java-логіки.

В Java сервлети представлені у вигляді ``HttpServlet``. Сам Servlet
реалізовує патерн *template method*.

Наразі в чистому вигляді сервлети використовуються рідко. Зазвичай –
разом із рядом надбудов. Але це все одно ті ж самі севлети з тими ж
принципами роботи.

--------------

Лекція 2. JSF.
==============
date: 2016-10-05 12:29:32 +0300

-  `Слайди
   лекції(pdf) <https://vk.com/doc135321152_438074235?hash=0b93d16ab725dc4593&dl=98527b9d15bb987d89>`_
-  `Слайди лекції(Google
   presentation) <https://docs.google.com/presentation/d/1y3z8k42E0se5ns-I_c1pcNH_n6qWUULjTJ8UqShtpw0/edit>`_
-  `Простий приклад застосунку з використанням
   JSF <https://github.com/ValkoVolodya/jsf-lecture-demo>`_

--------------

Лекція 3. JPA.
==============
date: 2016-10-12 12:29:32 +0300

-  `Слайди
   лекції(pptx) <https://vk.com/doc86287709_438256799?hash=5b2f476573189a3299&dl=1c7e4e411c3779a039>`_
-  `Простий приклад застосунку з використанням JPA
   (zip) <https://vk.com/doc86287709_438256748?hash=5f289c7463c431ccfa&dl=6a742187609521805b>`_
-  `Простий приклад застосунку з використанням JPA
   (GitHub) <https://github.com/SichYuriy/JavaEE_KPI/tree/master/LectionExample>`_

Матеріал підготували: `Юрій <https://github.com/SichYuriy>`_ та
`Віта <https://github.com/VitaKaras>`_

--------------

Лекція 5. JMS.
==============
date: 2016-11-02 12:20:00 +0300


-  `Слайди лекції (google
   presentation) <https://docs.google.com/presentation/d/1_rPM8hjhqLd3twAQE2wyHDgPKX3XE43S761kuJjfdPA/edit?usp=sharing>`__
-  `Пример использования JMS (google
   drive) <https://drive.google.com/open?id=0B1I60TTGSx02eVktSmhBTTZjNXM>`__

Матеріал підготували: `Тетяна <https://github.com/ttatus>`_ та `Андрій <https://github.com/crosshp>`_

--------------

Лекція 7. Авторизація та автентифікація в JavaEE.
=================================================
date: 2016-11-16 12:20:32 +0200

JAAS
----

-  JAAS – Java Authentication and Authorization Service
-  Присутній як в Java EE, так і в Java SE
-  Доволі низькорівневий
-  Документація
-  `автентикація <http://docs.oracle.com/javase/7/docs/technotes/guides/security/jaas/tutorials/GeneralAcnOnly.html>`__
-  `авторизація <http://docs.oracle.com/javase/7/docs/technotes/guides/security/jaas/tutorials/GeneralAcnAndAzn.html>`__
-  `JAAS reference
   guide <http://docs.oracle.com/javase/7/docs/technotes/guides/security/jaas/JAASRefGuide.html>`__

WildFly
-------

Налаштування серверу застосунків
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Щоб налаштувати авторизацію і автентикацію у wildfly, необхідно у
standalone.xml додати security realm:

.. code:: xml

    <security-domain name="dbdomain">
        <authentication>
            <login-module code="Database" flag="required">
                <module-option name="dsJndiName" value="java:MySqlDS"/>
                <module-option name="principalQuery" value="select password from users where login = ?"/>
                <module-option name="rolesQuery" value="select role,'Roles' from user_roles where login = ?"/>
                <module-option name="hashAlgorithm" value="SHA-256"/>
                <module-option name="hashEncoding" value="BASE64"/>
            </login-module>
        </authentication>
    </security-domain>

Також у проекті потрібно описати wildfly-web.xml

Приклад проекту
~~~~~~~~~~~~~~~

Приклад JavaEE проекту з використанням JAAS:
`[github] <https://github.com/DmytroKanivets/CarsRentalService>`__.
Автор проекту: `Дмитро <https://github.com/DmytroKanivets>`__


Лекція 11. Моніторинг та оптимізація Java-застосунків.
======================================================
date: 2016-12-21 12:20:00 +0200

- Слайди лекції. `[github] <https://kpi-fict-ip32.github.io/slides/jee-monitoring-and-optimization/>`_, `[slideshare] <http://www.slideshare.net/OlexandrKovalchuk/jeemonitoringandoptimization>`_

Матеріал підготували: `Владислав <https://github.com/VladislavZavadsky>`_ та `Олександр <https://github.com/anxolerd>`_.
