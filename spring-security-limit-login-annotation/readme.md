Spring Security : limit login attempts example
------------------------------------------------
In this tutorial, we will show you how to limit login attempts in Spring Security, which means, if a user try to login with an invalid password more than 3 times, the system will lock the user and make it unable to login anymore.

Technologies and tools used :
------------------------
1. Spring 4.3.0.RELEASE
2. Spring Security 4.1.1.RELEASE
3. Spring JDBC 4.3.0.RELEASE
4. Eclipse 4.2 / STS
5. JDK 1.7
6. Maven 3
7. MySQL Server 5.6
8. Tomcat 7 (Servlet 3.x)

Some quick notes for this tutorial :
-----------------------------------
1. MySQL database will be used.
2. This is a Spring Security annotation-based example.
3. Create a “users” table with column “accountNonLocked”.
4. Create a “user_attempts” table to store the invalid login attempts.
5. Spring JDBC will be used.
6. Display custom error messages based on the returned exception.
7. Create a customized “authenticationProvider”


1. Solution
Review the existing Spring Security’s authentication class, the “locked” feature is already implemented. To enable the limit login attempts, you need to set the UserDetails.isAccountNonLocked to false.

DaoAuthenticationProvider.java
package org.springframework.security.authentication.dao;

public class DaoAuthenticationProvider
	extends AbstractUserDetailsAuthenticationProvider {
	//...
}
AbstractUserDetailsAuthenticationProvider.java
package org.springframework.security.authentication.dao;

public abstract class AbstractUserDetailsAuthenticationProvider
    implements AuthenticationProvider, InitializingBean,
    MessageSourceAware {

    private class DefaultPreAuthenticationChecks implements UserDetailsChecker {
        public void check(UserDetails user) {
          if (!user.isAccountNonLocked()) {
              logger.debug("User account is locked");

          throw new LockedException(
              messages.getMessage("AbstractUserDetailsAuthenticationProvider.locked",
                 "User account is locked"), user);
          }
           //...
        }
    }
    

 4. Database
 -------------
Here are the MySQL scripts to create the users, user_roles and user_attempts tables.

4.1 Create a “users” table, with column “accountNonLocked”.
----------------------------------------------------------
users.sql

CREATE  TABLE users (
  username VARCHAR(45) NOT NULL ,
  password VARCHAR(45) NOT NULL ,
  enabled TINYINT NOT NULL DEFAULT 1 ,
  accountNonExpired TINYINT NOT NULL DEFAULT 1 ,
  accountNonLocked TINYINT NOT NULL DEFAULT 1 ,
  credentialsNonExpired TINYINT NOT NULL DEFAULT 1,
  PRIMARY KEY (username));

4.2 Create a “user_roles” table.
----------------
user_roles.sql

CREATE TABLE user_roles (
  user_role_id int(11) NOT NULL AUTO_INCREMENT,
  username varchar(45) NOT NULL,
  role varchar(45) NOT NULL,
  PRIMARY KEY (user_role_id),
  UNIQUE KEY uni_username_role (role,username),
  KEY fk_username_idx (username),
  CONSTRAINT fk_username FOREIGN KEY (username) REFERENCES users (username));

4.3 Create a “user_attempts” table.
---------------------
user_attempts.sql
CREATE TABLE user_attempts (
  id int(11) NOT NULL AUTO_INCREMENT,
  username varchar(45) NOT NULL,
  attempts varchar(45) NOT NULL,
  lastModified datetime NOT NULL,
  PRIMARY KEY (id)
);


4.4 Inserts an user for testing.
---------------------------------
INSERT INTO users(username,password,enabled) VALUES ('mkyong','123456', true);
INSERT INTO user_roles (username, role) VALUES ('mkyong', 'ROLE_USER');
INSERT INTO user_roles (username, role) VALUES ('mkyong', 'ROLE_ADMIN');


How to run the application ?
--------
http://localhost:8080/SpringSecurity/login

- Try with correct UserName and password
- Try with wrong username and password

