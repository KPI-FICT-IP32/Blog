---
layout: post
title: "Лекція 7. Авторизація та автентифікація в JavaEE"
date: 2016-11-16 12:20:32 +0200
categories: kpi_s07_jee
---

## JAAS

- JAAS -- Java Authentication and Authorization Service
- Присутній як в Java EE, так і в Java SE
- Доволі низькорівневий
- Документація
  - [автентикація](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jaas/tutorials/GeneralAcnOnly.html)
  - [авторизація](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jaas/tutorials/GeneralAcnAndAzn.html)
  - [JAAS reference guide](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jaas/JAASRefGuide.html)

## WildFly

### Налаштування серверу застосунків

Щоб налаштувати авторизацію і автентикацію у wildfly, необхідно у standalone.xml додати security realm:

```xml

<security-domain name="dbdomain">
    <authentication>
        <login-module code="Database" flag="required">
            <module-option name="dsJndiName" value="java:MySqlDS"/>
            <module-option name="prinipalQuery" value="select password from users where login = ?"/>
            <module-option name="rolesQuery" value="select role,'Roles' from user_roles where login = ?"/>
            <module-option name="hashAlgorithm" value="SHA-256"/>
            <module-option name="hashEncoding" value="BASE64"/>
        </login-module>
    </authentication>
</security-domain>
```

Також у проекті потрібно описати wildfly-web.xml

### Приклад проекту

Приклад JavaEE проекту з використанням JAAS: [[github]](https://github.com/DmytroKanivets/CarsRentalService). Автор проекту: [Дмитро](https://github.com/DmytroKanivets)
