---
title: "Tell-Don’t-Ask"
date: 2022-05-08T21:33:12-03:00
draft: false
categories: [ Software Engineering ]
---

A few weeks ago, one of the best engineers on my team made an important comment in a pull request:

>  _"Remember not to break the Tell-Don't-Ask principle."_
>
> — The great [Fer](https://github.com/hack2024).

Let's delve into this concept a bit...

In object-oriented software, a typical use case involves executing logic based on an object's internal state. For instance, consider a scenario where we want to sound an alarm if a thermometer reaches a certain temperature:

```typescript
class Thermometer {
  private temperature: number = 0;

  increaseTemperature(value: number): void {
    this.temperature += value;
  }

  getTemperature(): number {
    return this.temperature;
  }
};

class Alarm {
  sound(): void {
    console.log('RIIING!');
  }
};
```

In this "asking" approach, to detect the temperature and sound an alarm, we would have to:

```typescript
const thermometer = new Thermometer();
thermometer.increaseTemperature(35);
const temperature = thermometer.getTemperature();
if (temperature > 30) {
  const alarm = new Alarm();
  alarm.sound();
};
```

However, following the Tell-Don't-Ask principle suggests that the logic should reside within the object itself if it is related to that object. In other words, the thermometer should be responsible for sounding the alarm when it reaches a certain temperature. This promotes more object-oriented code as opposed to procedural code.

> **Procedural code gets information then makes decisions. Object-oriented code tells objects to do things.**

With this in mind, let's refactor our classes using a "telling" approach:

```typescript
class Thermometer {
  private temperature: number = 0;
  private alarm: Alarm;

  constructor(alarm: Alarm) {
    this.alarm = alarm;
  }

  increaseTemperature(value: number): void {
    this.temperature += value;
    if (this.temperature > 30) {
      this.alarm.sound();
    }
  }
};

class Alarm {
  sound(): void {
    console.log('RIIING!');
  }
};
```

Now, instead of checking the thermometer's internal status to sound the alarm, we "tell" the thermometer to handle that:

```typescript
const alarm = new Alarm();
const thermometer = new Thermometer(alarm);
thermometer.increaseTemperature(35);
```

To summarize, it is acceptable to "ask" for the state of an object and then execute certain logic based on that information. However, if that logic is inherently related to the object, it should be moved and become the responsibility of the object itself. By adhering to the Tell-Don't-Ask principle, we can create more maintainable and object-oriented code.

---

- *[The Art of Enbugging, Andy Hunt and Dave Thomas (2003)](https://media.pragprog.com/articles/jan_03_enbug.pdf).*