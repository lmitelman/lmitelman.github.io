---
title: "Entities, DTOs and Value Objects"
date: 2022-12-11T00:15:00-03:00
draft: true
# tags:
#   - example
---

To raise our technical standards, with my teammates we decided to go back to basics for a few weeks. Under the wings of my great colleagues [Fer](https://github.com/hack2024) and [Cesar](https://github.com/cesar-lp), our goal was to reinforce the fundamentals of _Domain Driven Design_.

As you have read in the title, today we will explore two important design patterns to transfer data between different layers of an application: __Entities__, __Data Transfer Objects__ and __Value Objects__.

> _"If you can’t rederive concepts from the basics as you need them, you’re lost."_ 


https://sharegpt.com/c/x25sNIb
https://sharegpt.com/c/IE17oX8

<br>

### What is an Entity?

### What is a DTO?

A __Data Transfer Object__ (DTO) is a data structure that is used to represent the data of an object in an application, without having any behavior or logic associated with it.

For example, if a user's information needs to be passed from a web application's frontend to its backend, a User DTO could be used to represent the user's data in a consistent and easy-to-use format.

```typescript
class User {
  constructor(
    public id: number,
    public firstName: string,
    public lastName: string,
    public email: string,
  ) {}
}
```

### What is a Value Object?

On the other hand, a __Value Object__ is a type of object that is defined by its value, rather than by its identity. Value Objects can be used in many different ways, but one common use case is to represent data that is expected to be consistent and immutable.

<ins>When should you use it?<ins>

---

- *[Domain-Driven Design Quickly, Abel Avram and Floyd Marinescu (2007)](https://www.amazon.com/Domain-Driven-Design-Quickly-Abel-Avram/dp/1411609255).*