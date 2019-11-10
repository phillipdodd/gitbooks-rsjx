# Schedulers

**Schedulers** control:

* **when** an Observable **begins executing** 
* **when notifications** are sent to its Observers.



<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><a href="https://rxjs-dev.firebaseapp.com/api/index/const/queueScheduler">queueScheduler</a>
      </td>
      <td style="text-align:left">
        <ul>
          <li><em>synchronously </em>places tasks on a <b>queue </b>instead of immediate
            execution</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://rxjs-dev.firebaseapp.com/api/index/const/asyncScheduler">asyncScheduler</a>
      </td>
      <td style="text-align:left">
        <ul>
          <li>executes observers <em><b>a</b>synchronously. </em>&quot;As if you&apos;d
            used <b>setTimeout()</b>&quot;</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://rxjs-dev.firebaseapp.com/api/index/const/asapScheduler">asapScheduler</a>
      </td>
      <td style="text-align:left">
        <ul>
          <li>executes observers <em>asynchronously </em>but uses a different task queue
            than the <b>asyncScheduler</b>. It uses the <b>microtask queue</b>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://rxjs-dev.firebaseapp.com/api/index/const/animationFrameScheduler">animationFrameScheduler</a>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Used for browser animations</li>
          <li>Perform task when <code>window.requestAnimationFrame</code> would fire</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://rxjs-dev.firebaseapp.com/api/testing/TestScheduler">TestScheduler</a>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Used for testing</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>{% page-ref page="../additional-notes/javascript-event-loop.md" %}

```typescript
import { merge, queueScheduler, asapScheduler, asyncScheduler } from 'rxjs';

console.log('Start Script');

//* Create differently scheduled observables
//! Note the scheduler used as the optional second parameter

let queue$ = of('QueueScheduler (synchronous)', queueScheduler);

let asap$ = of('AsapScheduler (async micro task)', asapScheduler);

let async$ = of('AsyncScheduler (async task)', asyncScheduler);

//* Output will be the same regardless of param order
merge(async$, asap$, queue$)
    .subscribe(
        value => console.log('value')
);

console.log('End script.')
    
//* Output

// Start script.
// QueueScheduler(synchronous)
// End Script.
// AsapScheduler (async micro task)
// AsyncScheduler (async task)
```

## [observeOn Operator](https://rxjs-dev.firebaseapp.com/api/operators/observeOn)

The **observeOn\(\)** operator takes a **scheduler** as an argument and will return an **observable** that has had the specifed scheduler applied to it.

When used within a **pipe\(\)**, any observables produced from that point onwards will use the specified scheduler:

```typescript
import {
    from, observeOn,
    queueScheduler, asyncScheduler
} from 'rxjs';

console.log('Start Script');

from([1, 2, 3, 4], queueScheduler).pipe(
    tap(value => console.log(`Value: ${value}`)),
    observeOn(asyncScheduler),
    tap(value => console.log(`Doubled value: ${value * 2}`))
);

console.log('End script.')
    
//* Output

// Start script.
// Value: 1
// Value: 2
// Value: 3
// Value: 4
// End Script.
// Doubled Value: 2
// Doubled Value: 4
// Doubled Value: 6
// Doubled Value: 8
```

{% hint style="info" %}
Without the **observeOn** applied in the middle of the pipe in the example above, the output would have **all been synchronous**, logging the doubled values **among** the non-doubled values, instead of tossing all of the second taps\(\)'s onto the **async task queue.**
{% endhint %}

## 

## 

