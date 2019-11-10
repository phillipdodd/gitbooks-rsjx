# Subjects

**Subjects** are _both_ **Observers** _and_ **Observers.**

They can **produce their own values**, **proxy values**, have **state** and maintain a list of **other Observers** subscribed to them.

Because they maintain a list of objects that  subscribe to them, Subjects are **multicast** instead of **uni-cast**.

In the following diagram, we see a **Subject** that has subscribed to an **Observable** and also has **two separate** **Observers** subscribed to the **Subject.** When the **Observer** on the left produces values, the **Subject** receives them and then produces them for each Observer subscribing to it.

![](../.gitbook/assets/image%20%281%29.png)

![](../.gitbook/assets/image.png)



