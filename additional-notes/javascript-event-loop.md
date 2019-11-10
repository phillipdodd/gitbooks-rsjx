# Javascript Event Loop

From [this Pluralsight video](https://app.pluralsight.com/course-player?clipId=a71d498b-4a9c-4533-acd1-e1a1d7f3688f).

![](../.gitbook/assets/image%20%283%29.png)

Javascript uses a **single event loop** to process tasks **synchronously.** 

With each step of the loop, **one Sync Task** is executed. 

When the **Sync Queue** is done, it will check to see if there is an **Async Task** available to be executed. If there is, it will take the **next one** waiting and **process it.**

![](../.gitbook/assets/image%20%284%29.png)

There is also the **Async Microtask Queue**. It is given priority over the other **Async Queue,** and unlike the **Async Queue**, the event loop will take _all_ the awaiting **Microtask** **Queue** tasks instead of just the next one.

![](../.gitbook/assets/image%20%285%29.png)

