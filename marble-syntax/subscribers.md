# Subscribers

The **beginning** of a subscription is represented by an `^` character and the **end** is represented by an `!`. In this example, we see it subscribe and then un-subscribe **4 milliseconds** later.

```typescript
let subscription = '^---!';
```

In _this_ example, the subscription **subscribes** on the **third frame** and _never_ **un-subscribes.**

```typescript
let subscription = '--^-';
```

The **same shorthand** for describing periods of time that is used for **observables** can be used here for **subscriptions** as well.

```typescript
let subscription = '^ 10ms !';
```

