Spring Security password hashing example

In this tutorial, we will show you how to use BCryptPasswordEncoder to hash a password and perform a login authentication in Spring Security.

In the old days, normally, we used MD5 Md5PasswordEncoder or SHA ShaPasswordEncoder hashing algorithm to encode a password… you are still allowed to use whatever encoder you like, but Spring recommends to use BCrypt BCryptPasswordEncoder, a stronger hashing algorithm with randomly generated salt.

Technologies used :

Spring 4.3.0.RELEASE
Spring Security 4.1.1.RELEASE
Spring JDBC 4.3.0.RELEASE
MySQL Server 5.6
1.Review PasswordEncoder

The familiar old authentication PasswordEncoder interface is deprecated…

package org.springframework.security.authentication.encoding;

//Implementation : Md5PasswordEncoder and ShaPasswordEncoder @Deprecated public interface PasswordEncoder { Instead, you should use this new crypto PasswordEncoder interface.

package org.springframework.security.crypto.password;

//Implementation : BCryptPasswordEncoder public interface PasswordEncoder {

Generate a BCrypt Password First, hash a password and put it into a database, for login authentication later. This example uses BCryptPasswordEncoder to hash a password “123456”.
PasswordEncoderGenerator.java package com.mkyong.web.controller;

import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;

public class PasswordEncoderGenerator {

public static void main(String[] args) {

int i = 0;
while (i < 10) {
    String password = "123456";
    BCryptPasswordEncoder passwordEncoder = new BCryptPasswordEncoder();
    String hashedPassword = passwordEncoder.encode(password);

    System.out.println(hashedPassword);
    i++;
}
} } In BCrypt hashing algorithm, each time, a different hash value of length 60 is generated.

$2a$10$EblZqNptyYvcLm/VwDCVAuBjzZOI7khzdyGPBr08PpIi0na624b8. $2a$10$trT3.R/Nfey62eczbKEnueTcIbJXW.u1ffAo/XfyLpofwNDbEB86O $2a$10$teJrCEnsxNT49ZpXU7n22O27aCGbVYYe/RG6/XxdWPJbOLZubLIi2 $2a$10$BHG59UT6p7bgT6U2fQ/9wOyTIdejh4Rk1vWilvl4b6ysNPdhnViUS $2a$10$W9oRWeFmOT0bByL5fmAceucetmEYFg2yzq3e50mcu.CO7rUDb/poG $2a$10$HApapHvDStTEwjjneMCvxuqUKVyycXZRfXMwjU0rRmaWMsjWQp/Zu $2a$10$GYCkBzp2NlpGS/qjp5f6NOWHeF56ENAlHNuSssSJpE1MMYJevHBWO $2a$10$gwbTCaIR/qE1uYhvEY6GG.bNDQcZuYQX9tkVwaK/aD7ZLPptC.7QC $2a$10$5uKS72xK2ArGDgb2CwjYnOzQcOmB7CPxK6fz2MGcDBM9vJ4rUql36 $2a$10$6TajU85/gVrGUm5fv5Z8beVF37rlENohyLk3BEpZJFi6Av9JNkw9O

It's normal to get a different value each time you hash a value with BCrypt, because salt is generated randomly. In this tutorial, we get the first output and inserts it into the database.

How run the application ?

http://localhost:8080/spring-security-password-hashing/login

try username/pwd : mkyong / 123456