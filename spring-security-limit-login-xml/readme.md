spring-security-limit-login
-----------------------------
In this tutorial, we will show you how to limit login attempts in Spring Security, which means, if a user try to login with an invalid password more than 3 times, the system will lock the user and make it unable to login anymore.

Technologies and tools used :
----------------------------
Spring 4.3.0.RELEASE
Spring Security 4.1.1.RELEASE
Spring 4.3.0.RELEASE
Eclipse 4.2
JDK 1.7
Maven 3
MySQL Server 5.6
Tomcat 7 (Servlet 3.x)
Some quick notes for this tutorial :

MySQL database will be used.
----------------------------
This is a Spring Security annotation-based example.
Create a “users” table with column “accountNonLocked”.
Create a “user_attempts” table to store the invalid login attempts.
Spring JDBC will be used.
Display custom error messages based on the returned exception.
Create a customized “authenticationProvider”


How to run the application? 
----------------------------
http://localhost:8080/SpringSecurity/login

- try with correct username and password
- try with incorrect username and password
