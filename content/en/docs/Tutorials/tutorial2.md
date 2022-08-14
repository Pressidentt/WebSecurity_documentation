---
title: "CSRF"
weight: 5
description: >
 We ill takl about preventing CSRF attack
---

Cross-site request forgery (also known as CSRF) is a web security vulnerability that allows an attacker to induce users to perform actions that they do not intend to perform. It allows an attacker to partly circumvent the same origin policy, which is designed to prevent different websites from interfering with each other.

---

As in other web-frameworks, Nest provide built in library for preventing that attack.

*Download*

{{% pageinfo %}}
npm i --save csurf
{{% /pageinfo %}}

*Then, in main.ts*

 ```js
import * as csurf from 'csurf';
app.use(csurf());
 ```

---
