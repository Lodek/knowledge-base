```yml
entry:
  type: article
  date: 2020-10-25
  tags:
    - architecture
    - rest
```
# Intro

Recently I've been studying API Security.
The industry standard seems to make use of JWT, however I found an interesting article on why JWT is not optimal most of the times.
The alternative to JWT would be to add state management to the API.
To add to the confusion, the [Springs official guide](https://spring.io/guides/tutorials/spring-boot-oauth2/) regarding OAuth builds a SPA application with a Spring backend, which uses Spring Security to deal with OAuth and they use session management!
From the guide:
> If you look in the browser tools (F12 on Chrome or Firefox) and follow the network traffic for all the hops, you will see the redirects back and forth with GitHub, and finally you’ll land back on the home page with a new Set-Cookie header.
This cookie (JSESSIONID by default) is a token for your authentication details for Spring (or any servlet-based) applications.

It's making use of cookies and sessions in a REST API.
I am thoroughly confused, I thought REST was supposed to be stateless and JWT provided that.

