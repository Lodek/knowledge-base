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

# States in REST
An interesting solution to the problem of state in REST can be found [here](https://stackoverflow.com/questions/2641901/how-to-manage-state-in-rest).

The gist of it is, in case of a FSM-like flow, where you need pre conditions to transition through screens or a complex flow, each step should use API endpoints to manage data transitions.
> The REST answer is that state should be sent back-and-forth with each request/response.

In another case where one is creating a resource for a "session", that resource should be made available using the standard REST interface.
> If you are, on the other hand, trying to manage some sort of new object on the server--such as a shopping cart--then the REST answer is that you are actually creating a new entity that can be accessed like any other by a direct URL [...]

This approach is coherent with how REST manage data, so it makes perfect sense.
Even if it's a transient and volatile object, respecting the API's interface is a good way to go about this without having to keep all of that on the frontend, like I've done in the past using an Angular Service.

Two notes I want ot make about that: clearly it doesn't matter *where* that data is stored, it could be in an in-memory db; secondly in the shopping cart example, the interface for that would be a REST resource like anything else.

The approach of temporary entities like that introduces complexity though, namely, how to deal with abandoned flows.
that is, what if an user makes a shopping cart and gives up on the purchase.

That stackoverflow link is a gem with interesting discussions.
I still don't have the answer but it seems like there's no clear answer here.
Going full REST statelesness seems to add a lot of complexity, using sessions and such violates contraints.

# Cookies and REST
Contrary to my prior believes, cookies don't break REST, it's just another way to store information which is overall more secure and well established than Local Storage.

[Read](https://softwareengineering.stackexchange.com/questions/141019/should-cookies-be-used-in-a-restful-api)


A really good resource is a [talk](https://skillsmatter.com/skillscasts/5398-the-state-of-securing-restful-apis-with-spring) given by a member of spring security.
He addresses practical concerns.
Cookies are more convenient and good enough; it seems to be a "practicality beats purity" situation.
