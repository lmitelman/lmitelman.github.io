---
title: "The Art of Silent Launches"
date: 2024-01-26T15:33:12-03:00
draft: true
description: "Personal lessons from the trenches about my experience with gradual rollouts of features."
categories: [ Software Engineering ]
ShowToC: true
---

My experience at a company with a digital wallet service, used by over 3 million people, was a lesson in unexpected challenges. During my time there, my team and I developed a new feature that was eagerly anticipated by our users. We didn't anticipate the overwhelming response at its launch, which led to a massive surge in traffic. Our tech infrastructure, unprepared for such a load, was overwhelmed and eventually collapsed.

Now, let's look at some better ways to introduce new features without encountering these problems. I will discuss different strategies of **Gradual Rollouts**, a phased approach in engineering for releasing updates. This enables testing stability and performance with a limited audience, identifying issues with minimal overall user impact.

<p style="margin-top: 45px;"></p>

### Dark Launching

Dark Launching is primarily a backend technique that involves introducing a new feature, which is then released for current users without their knowledge. This technique provides insights into how the feature would be behaving in production, without actually impacting users.

We adjust the process to call the new feature as it would in production, doing all the work but without displaying any results, ensuring it remains invisible to users. Meanwhile, this allows test engineers to evaluate the new feature in a real-world setting without impacting the user experience.

<img src="/images/dark-launching.png" alt="Dark Launching" style="width:90%; height:auto;">

This process allows for performance testing, issue detection, infrastructure scaling assessments and stress testing under actual traffic conditions. Dark launching is particularly effective for critical updates where precision is crucial and risks are high. Its strength lies in testing features discreetly, maintaining user experience while identifying potential issues early. However, it requires significant backend effort and may not capture real user reactions or feedback, as users are unaware of the changes being tested.
Essentially, it offers a safer, more effective way to ensure new updates are ready for broader release.

<p style="margin-top: 45px;"></p>

### Canary Release

Canary Release is a method used to minimize the risk of deploying new versions by initially introducing the update to a small group of users. This approach involves gradually extending the update across the entire system.

This technique starts with the new version being deployed to a part of the infrastructure not yet accessed by users, and then the process continues by gradually routing some user traffic to the  new version.

<img src="/images/canary-release.png" alt="Canary Release" style="width:90%; height:auto;">
<p style="margin-top: 30px;"></p>

The term is derived from an [old mining practice](https://www.smithsonianmag.com/smart-news/story-real-canary-coal-mine-180961570/), where miners took canaries into mines as an early warning system against toxic gases. Just as the canary would alert miners to danger, a canary release detects potential issues in a software update before it affects all users.

In modern distributed systems, instead of using a router for this process, various strategies are employed. These include rolling out updates to specific geographic regions first or to specific user groups based on criteria like user behavior, device type, or membership tier.

Canary Release is particularly effective for applications requiring extensive user feedback where minimizing risk is crucial. The major advantage lies in its ability to detect issues early with minimal user impact. However, it demands meticulous monitoring and can lead to a slower overall release process.

> 💡 <span style="color: #9B9C9D;">
The concepts of **Dark Launching** and **Canary Release** have evolved over time, leading to some confusion. Nowadays, they are often used interchangeably, but it's important to note that they are not the same.
</span>

Alongside the mentioned strategies, **Feature Toggles** are essential in implementing Canary Releases. They enable the introduction of new features within the same production environment. This approach allows for incremental rollouts to these specific user groups, streamlining the release process and reducing the need for maintaining multiple environments.

<img src="/images/feature-toggle.png" alt="Feature Toggles" style="width:80%; height:auto;">

> 💡 <span style="color: #9B9C9D;"> **Feature Toggle** is also referred to as **Feature Flag** in some engineering contexts, highlighting its role in enabling and disabling certain features.
</span>

<p style="margin-top: 45px;"></p>

### Shadow Testing

Shadow testing is a technique used to compare the current environment with a new one that includes a new feature. Its purpose is to identify and reduce potential risks before releasing the new feature to users, all without users ever knowing it's happening.

In shadow testing, we observe how real users interact with our system by examining their actual traffic, all without impacting the code or the experience of users in the production environment.

<img src="/images/shadow-testing.png" alt="Shadow Testing" style="width:150%; height:auto;">

A replica of the production environment is created to mimic real user traffic. This environment serves as a _shadow_ of the production environment. The new feature is then tested in a different environment. After testing, the responses from both environments are compared by test engineers to identify any risks before introducing the new feature to the production environment.

This technique is particularly convenient in scenarios where accurate performance assessment under real-world conditions is essential, without the risk of disrupting user experience. It’s ideal for systems that handle sensitive data or complex transactions, where unnoticed errors could lead to significant issues. 

The primary advantage of Shadow Testing is its ability to provide a realistic evaluation of new features, without affecting end users. However, it can be resource-intensive to set up and maintain a parallel environment, and it may not fully capture user experience aspects, since interactions are only simulated, not directly observed.

<p style="margin-top: 45px;"></p>

### TL;DR

| Gradual&nbsp;Rollout&nbsp;Strategy   | Description |
| ------------------------------- | ----------- |
| **Dark Launching**              | Deploying a feature in production without making it visible to users. The functionality is _dark_ to users, but can be selectively enabled for testing purposes. |
| **Canary Release**              | Rolling out a new feature incrementally to a small subset of users before a full deployment, often implemented through the use of **Feature Toggles**.    |
| **Shadow Testing**              | Duplicating real traffic to a parallel new service version, which processes it without affecting or being noticed by users, allowing performance and stability testing under real conditions. |

<p style="margin-top: 80px;"></p>

---

<h1 style="font-size: smaller; margin-top: 24px; margin-bottom: 16px;">Acknowledgements</h1>
<span style="font-size:smaller;">
With appreciation for the contributions of my dear friends and former colleagues, <a href="https://www.linkedin.com/in/bautista-coronado/" target="_blank">Bautista Coronado</a> and <a href="https://www.linkedin.com/in/mauro-maulini-50b02192/" target="_blank">Mauro Maulini</a>. Their valuable input and dedicated reviews were instrumental during the drafting process of this article.
</span>

---

- _["The Top 10 Adages in Continuous Deployment" by C. Parnin et al. (2017)](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=7927896&isnumber=7927880)_

- _["We’re Doing It Live" by G. Schermann, J. Cito, P. Leitner, U. Zdun and H. C. Gall (2018)](https://www.sciencedirect.com/science/article/abs/pii/S0950584917302136?via%3Dihub)._


