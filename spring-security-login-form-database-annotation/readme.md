spring-security-loginform-database-annotation
----------------------------------------------
In this tutorial, we will show you how to perform database authentication (using Annotations) in Spring Security.

Technologies used :
---------------------
- Spring 4.3.0.RELEASE
- Spring Security 4.0.0.RELEASE
- Spring JDBC 4.0.0.RELEASE
- Eclipse 4.2 / STS
- JDK 1.7
- Maven 3.2.x
- Tomcat 6 or 7 or 8 (Servlet 3.x)
- MySQL Server 5.6

Previous login-form in-memory authentication will be reused, enhance to support the following features :

Database authentication, using Spring-JDBC and MySQL.
Spring Security, JSP TagLib, sec:authorize access="hasRole('ROLE_USER')
Customize a 403 access denied page.


To perform database authentication, you have to create tables to store the users and roles detail. Please refer to this Spring Security user-schema reference. Here are the MySQL scripts to create users and user_roles tables.

Note::
Username “mkyong”, with role_user and role_admin.
Username “alexa”, with role_user.


How to run the application?
-----------------------------
http://localhost:8080/SpringSecurity/

For Successful Login::
-----------------------
http://localhost:8080/SpringSecurity/login
- Username/Pwd : mkyong / 123456
- Username/Pwd : alex / 123456

Login using 'mkyong', after login type http://localhost:8080/SpringSecurity/admin, you should be able to see admin page.

Login using 'alex', after login type http://localhost:8080/SpringSecurity/admin, you should not be able to see admin page.



Reference URL:
---------------
- http://www.mkyong.com/spring-security/spring-security-form-login-using-database/
- http://docs.spring.io/spring-security/site/docs/3.2.3.RELEASE/reference/htmlsingle/#user-schema