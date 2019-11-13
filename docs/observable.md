# Observables

## Description

An **Observable** is a representation of any set of values over a any set of time.

{% hint style="danger" %}
An **Observable** is **not** **executed** until an object **subscribes** to it. **Each** call to subscribe triggers an **independent execution** for a particular observer.
{% endhint %}

## Common ways to Create Observables

### Observable Constructor

An **Observable's constructor** will want a **function** that tells it **with what to** _**do**_ with the **subscriber** that it creates. 

After which the Observable's [**subscribe** **function**](https://rxjs-dev.firebaseapp.com/api/index/class/Observable) will need to be called to **create a** [**Subscriber**](https://rxjs-dev.firebaseapp.com/api/index/class/Subscriber#constructor) and begin executing the Observable.

The **subscribe** function \(Line 11 below\) takes as its first argument a **function defining subscriber.next\(\)**. 

```typescript
function sub(subscriber) {
    //* Assuming that allBooks is an array of objects...
    for (let book of allBooks) {
        subscriber.next(book);
    }
}

let allBooksObservable$ = new Observable(sub);

//* Observable does not execute until subscribed to:
allBooksObservable$.subscribe(book => console.log(book.title));
```

{% hint style="info" %}
**Further documentation** can be found here about **Line 11** in the example above, the [**Subscriber object's constructor**](https://rxjs-dev.firebaseapp.com/api/index/class/Subscriber#constructor)\*\*\*\*
{% endhint %}

The **subscriber** implements the **Observer's** **interface,** giving access to the three functions: 

1. `next()`
2. `error()`
3. `complete()`

\(In addition to an **optional `closed` boolean**\)

{% hint style="warning" %}
**No new values** will be produced by the **Observable** once `error()` or `complete()` are called.
{% endhint %}

**next\(\)** produces a value, **error\(\)** takes a string and is for reporting an error message, and **complete\(\)** indicates when the process is complete. To define all three, the example above could also be written as:

```typescript
let allBooksObservable$ = new Observable(subscriber => {
    
    if (document.title === 'oh no') {
        subscriber.error('Incorrect book title');
    }
    
    let book of allBooks {
        subscriber.next(book);
    }

    setTimeout(() => {
        subscriber.complete();
    }, 2000);

});

//* Observable does not execute until subscribed to:
allBooksObservable$.subscribe();

```

If `error()` is called, the code will stop and **will not run** any **aditional code** past that point.

### of, from, and fromEvent

These are three functions that can be **imported** from the **RxJS library** to create **Observables**. "They are not the only ones, but are the most common."

#### [of](https://rxjs-dev.firebaseapp.com/api/index/function/of)

Good for creating an **Observable** from **data that you already have.** While there are multiple ways of calling it, ultimately you just pass it a list of values that you want the created Observable to produce.

#### [from](https://rxjs-dev.firebaseapp.com/api/index/function/from)

Takes an arg that is an object already encapsulating a group of data.

#### [fromEvent](https://rxjs-dev.firebaseapp.com/api/index/function/fromEvent)

Designed to report on events from DOM elements.

```javascript
let button = document.getElementById('mybutton');
fromEvent(button, 'click')
    .subscribe(event => {
        //* Do things in response to the JS event
    });
```

#### 







## Observer

## Objects with simple Interface

## Subscribers



