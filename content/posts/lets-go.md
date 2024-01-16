---
title: "Let's Go"
date: 2023-12-29T10:33:12-03:00
draft: true
---

En un intento por lograr que nuestros servicios sean más óptimos, performantes y veloces, con nuestro equipo en Pomelo decidimos comenzar a implentar Go en algunos de los microservicios dentro de nuestra arquitectura.

¿Por que Go 


-----------------------------------------------------------------------

# (Composing Structs) Embedded Structures in Golang
In the Go programming language, Embedded Structures are a way to reuse a struct’s fields without having to inherit from it.

https://www.geeksforgeeks.org/embedded-structures-in-golang/

Promoted fields
Fields that belong to an embedded struct can be accessed directly through the outer struct variable. So, we can say that the fields of the embedded struct are promoted to the outer struct, and thus they are called the promoted fields.

-----------------------------------------------------------------------

# Why they say that Go is "cheaper" than other languages like Java?
- Compilation Speed: Go's fast compilation times mean that developers can iterate and test their code rapidly. This speed of compilation can lead to shorter development cycles and reduce the cost of development.

- Scalability: Go is known for its efficiency in handling concurrent tasks, thanks to goroutines and channels. This efficiency allows developers to build scalable applications that can handle high levels of concurrency without the need for extensive hardware resources. This scalability can translate into cost savings by optimizing server and infrastructure costs.

- Efficiency: Go's runtime performance is often comparable to or better than languages like Java. Efficient code execution can lead to cost savings in terms of hardware and cloud computing resources, as less computing power is needed to achieve the same results.

-----------------------------------------------------------------------

Go is not (a traditional) object-oriented language

https://chat.openai.com/share/cbe5cd1d-53cd-41f7-abb7-a05f382af10c

https://medium.com/@yesnandam/why-golang-choose-composition-as-its-base-rather-than-inheritance-1225d22a4798
https://medium.com/geekculture/why-golang-is-a-better-choice-for-your-next-project-8d042a77a30f
https://www.bairesdev.com/blog/why-golang-is-so-fast-performance-analysis/

---

- *[The Art of Enbugging, Andy Hunt and Dave Thomas (2003)](https://media.pragprog.com/articles/jan_03_enbug.pdf).*