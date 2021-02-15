```yml
book:
  title: unit testing principles, practices and patterns
  date: 2021-02-15
```
# Overview
It's not often that I read a book and its preface hits home.
The experience he describes with tests is exactly how I feel about them.
I know they are important and I want to improve my test writing but it's difficult when it feels like a waste of time.

Writing extensive boiler plates to mock a bunch of classes in order to test 3 lines of code feels awful.
What also feels terrible is testing internal logic.
Unit testing *should* be a blackbox test.
Testing internal logic ties the test to the implementation which makes it brittle.

# 1
- enterprise app: usually automate an organization's internal processes. They often have complex business logic, which isn't really logical and low performance requirements.

