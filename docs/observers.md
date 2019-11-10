# Observers

> **anonymous Observer Collection of callback functions** that process **values** and **messages** received from an **Observable**

**Observers** have an **interface** that mirrors **Observables**: they have a `next`, `error`, and `complete` function.

```typescript
let myObserver = {
    next: value => console.log(`value: ${value}`),
    error: err => console.log(`err: ${err}`),
    complete: () => console.log('done')
}
```

Created like this, as an **object literal**, it can be passed to an **Observable's subscribe** function. 

Alternatively, an object will be created for you if you instead pass three functions into the Observable's `subscribe()` function.

```typescript
let myObservable$.subscribe(
    value => console.log(`value: ${value}`),
    err => console.log(`err: ${err}`),
    () => console.log('done')
);
```

## Subscriptions

The **subscribe** function returns a [**Subscription**](https://rxjs-dev.firebaseapp.com/guide/subscription) object which has the important [**unsubscribe** ](https://rxjs-dev.firebaseapp.com/api/index/class/Subscription#unsubscribe-)**method** to cancel a subscription to an observable.



