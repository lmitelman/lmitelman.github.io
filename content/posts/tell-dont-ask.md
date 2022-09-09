---
title: "Tell-Don’t-Ask"
date: 2022-05-08T21:33:12-03:00
draft: false
---

A few weeks ago one of the best engineers in my team, the great [Fer](https://github.com/hack2024), made a comment in a pull request:

> _"Remember not to break the Tell-Don't-Ask principle."_

Let's talk a bit about this...

In object-oriented software, a typical use case is to execute logic based on an object's internal state.
For example, sounding an alarm in case our thermometer reaches a certain temperature:

```typescript
class Thermometer() {
  private temperature: number = 0;
  
  increaseTemperature(value: number): void {
    this.temperature = this.temperature + value;
  }

  askTemperature(): number {
    return this.temperature;
  }
};

class Alarm() {
  sound(): void {
    console.log('RIIING!');
  }
};
```

With this "asking" approach, to detect the temperature and sound an alarm, we should:

```typescript
const thermometer = new Thermometer();
thermometer.increaseTemperature(35);
const temperature = thermometer.askTemperature();
if (temperature > 30) {
  const alarm = new Alarm();
  alarm.sound();
};
```
If you are doing this, chances are that the logic you are implementing should be the object's responsibility. 
It is very likely that our thermometer should be in charge of sounding the alarm in case of reaching a certain temperature.
> Procedural code gets information then makes decisions. Object-oriented code tells objects to do things.

So, let's refactor our classes with a "telling" approach...

```typescript
class Thermometer() {
  private temperature: number = 0;
  private alarm: Alarm;

  constructor(alarm: Alarm) {
    this.alarm = alarm;
  }
  
  increaseTemperature(value: number): void {
    this.temperature = this.temperature + value;
    if (this.temperature > 30) {
      this.alarm.sound();
    };
  }
};

class Alarm() {
  sound(): void {
    console.log('RIIING!');
  }
};
```

Now, instead of us checking the thermometer's internal status to sound the alarm, we "tell" him to do that:

```typescript
const alarm = new Alarm();
const thermometer = new Thermometer(alarm);
thermometer.increaseTemperature(35);
```

In conclusion, it is correct to "ask" for the state of an object and then execute a certain logic. However, if that logic is related to the object, it may need to be moved and be the responsibility of the object itself.

