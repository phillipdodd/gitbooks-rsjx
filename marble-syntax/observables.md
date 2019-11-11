# Observables

{% hint style="info" %}
A **frame** is a unit to represent **virtual time** in a **TestScheduler.** Each one represents **one virtual millisecond**.
{% endhint %}

```typescript
//* Context being inside the callback of a TestScheduler...
let source$ = helpers.cold('-a-b-c');
```

Here, the `cold()` function is accepting a **marble diagram.** Each dash is representing the **passing** of **one virtual millisecond** and each **letter** is representing **produced values.**

In the above example, each **value** is produced separated by **one virtual millisecond**. In this next example,

```typescript
//* Context being inside the callback of a TestScheduler...
let source$ = helpers.cold('--a-4---c-8|');
```

There is a **new character** of `|`. This pipe character represents a completion signal. Next,

```typescript
//* Context being inside the callback of a TestScheduler...
let source$ = helpers.cold('  --a-4 12ms c-8#');
```

**Note:**

* **Whitespace is ignored** in marble syntax strings**.** 
* As a way of **shorthand,** `12ms` ****is an acceptable way to indicate **12 milliseconds** -- 12 `-`'s are **not required**. Using this shorthand _**does**_ require a leading and trailing whitespace.
  * `m` can be used for minutes
  * `s` can be used for seconds
* The `#` character is used to represent an **error** that occurs within the Observable.

In this example, we look at a **hot** observable produced with `helpers.hot()`

```typescript
//* Context being inside the callback of a TestScheduler...
let source$ = helpers.hot('-a-^-b-(cde)---f|');
```

Here, the `^` character represents the point at which a **subscription** the **hot** oberservable **begins.** These are unique to describing hot observables.

Several values enclosed in parethesis, like `(cde)` in the example above, is a syntax that is **not** just limited to hot observables.

This indicates that these three tasks, **c**, **b** and **e**, will occur **synchronously** in the **same frame.**

