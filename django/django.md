
# Views and class views

Overtime Django evolved its view system to be more sophisticated.
At first, let there be function based views.
This minimal setup worked but proved hard to created good abstractions.

As an alternative, django provided class based views which provides internal routing for Http methods.
Each HTTP method calls a class method with the same name.
The class based view infrastructure leverages Python's multi-polymorphic nature.
