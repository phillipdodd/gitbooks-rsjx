# Testing RxJS Code

## [TestScheduler](https://rxjs-dev.firebaseapp.com/api/testing/TestScheduler)

* Tests **asynchronous** code **synchronously** by using "**virtualized" time** so that waiting times are reduced.
* Only works with code using the [**AsyncScheduler**](https://rxjs-dev.firebaseapp.com/api/index/const/asyncScheduler)
* Constructor is passed a function to be used for equality tests
* Its run method accepts a **callback function** to perform the test and is the recommend way of using the TestScheduler.

## Using TestScheduler

```typescript
let scheduler = new TestScheduler((actual, expected) => {
    //* Any framework can be use to perform the check.
    //? Perform deep equality test here
});

//* The callback function is provided an object
//* that contains the functions making up the testing API
scheduler.run(helpers => {
    //? Use methods on 'helpers' object to test code here
})
```

First, the **TestScheduler** object must be created. It's constructor requires a callback that will be passed two values: the **actual** value and the **expected** value.

Here a deep equality check can be performed using the framework of your choosing.

Afterwards, the [**run\(\)**](https://rxjs-dev.firebaseapp.com/api/testing/TestScheduler#run-) function is called with a callback that will have a **RunHelpers** object passed in as its **first argument,** containing fivefunctions that make up the **testing API**:

| Name | Description |
| :--- | :--- |
| `.cold()` | Returns a cold observable that produces **values**, **errors**, and **completion messages** using a **special syntax** |
| `.help()` | Similar to `.cold()` but with a **hot observable** instead |
| `.expectObservable()` | Called when you are aready to test the final version of your prepared observer. |
| `.expectSubscriptions()` | Similar to `expectObservable()` but with subscriptions. |
| `.flush()` | Starts the virtual timer inside the TestScheduler. Rarely needs to be manually run due to being started automatically anyway |

{% hint style="info" %}
Once you havev an **Observable** ready to test, you can apply **operators or pipes** to it like **any other** observable.
{% endhint %}

## Testing with [Mocha](https://mochajs.org/) and [Chai](https://www.chaijs.com/)

```typescript
import { TestScheduler } from 'rxjs/testing';
import { expect } from 'chai';

describe('Test Suite', () => {

    //* Declare without initialization 
    let scheduler;

    //* This bit will execute before each it() test
    beforeEach(() => {
        //* Start with a fresh TestScheduler
        scheduler = new TestScheduler((actual, expected) => {
            //* Equality function provided by Chai
            expect(actual).deep.equal(expected);
        });
    });

    it('produces a signle value and completion message', () => {
        scheduler.run(helpers => {
            //* Cold observable created using marble syntax
            //? This will immediately produce a value then 
            //? send a completion message.
            const source$ = helpers.cold('a|');

            //* Define what we expect to happen using marble syntax
            const expected = 'a|';

            helpers.expectObservable(source$).toBe(expected);
        })
    });

    it('should delay the values produced', () => {
        scheduler.run(helpers => {
            const source$ = helpers.cold('-a-b-c-d|');

            //* For the expected value, we add 5 -'s
            //* to represent 5ms
            const expected = '------a-b-c-d|';

            //* Alternatively, we could have used '5ms'
            // const expected = '5ms -a-b-c-d|';

            //* Use the delay() operator to delay each value
            //* produced by the source by 5ms
            helpers.expectObservable(source$.pipe(
                delay(5)
            ))
            .toBe(expected)
        })
    });

    it('takes the correct number of values', () => {
        scheduler.run(helpers => {
            const source$ = helpers.cold('--a--b--c--d|');

            //* Here we use parenthesis to indicate that
            //* The value 'c' will be produced and the complete
            //* message sent in the same frame.
            const expected = '--a--b--(c|)';

            //* Define the subscription with marble syntax
            //* This is to indicate when it starts and when it ends
            const sub = '^-------!'

            //* Test the Observable
            helpers.expectObservable(source$.pipe(
                take(3)
            ))
            toBe(expected);

            //* Test the Subscription
            helpers
                .expectSubscriptions(source$.subscriptions)
                .toBe(sub);
        })
    });
})
```

## 

