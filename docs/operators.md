# Operators

**Operators** are **functions** that take some **configuration information** and return **functions**. 

The **function that is created** takes an **Observable** as an **argument** and **returns** an **Observable.**

```typescript
// manually applied
let source$ = of(1, 2, 3, 4, 5);

//* The 'map' RxJS operator
let doubler = map(value => value * 2);

let doubled$ = doubler(source$);

doubled$.subscribe(
    value => console.log(value)
);
```

## Categories of Operators

### Transformation

Returns an Observable that is **fundamentally different** than the source Observable.

### Filtering

### Combination

### Utility

Tend to involve changing **how** or **when** values are produced without changing the actual **value.**

### Conditional

Supplies values when certain conditions are met. Similar to filtering.

### Aggregate

Look at all the values produced and produce a single value, typically a min or max of them.

### Multicasting

Unique to "Subjects"

## Custom Operators

**Custom Operators** can be easily created by following their basic structure:

```typescript
//* Accept necessary config arguments
function myOperator(config1, config2, ...etc) {
    //* Return a function that takes an Observable as an arg
    return function (source$) {
        //* This function must return an Observable
        return newObservable$
    }
}
```

Because our **custom operator** returns a **function** that itself **receives an Observable** as an argument and **returns an Observable**, this means we are able to use **other operators** inside of our custom one:

```typescript
let source$ = of(1, 2, 3, 4, 5);

function doubleOperator() {
    return map(value => value * 2);
}

source$.pipe(
    doubleOperator()
)
.subscribe(
    doubleValue => console.log(doubledValue)
)
```

If we were to use _**more than one**_ other operator inside of our custom operator, we'd need to use the **pipe** method, like so:

```typescript
//* Accept necessary config arguments
function myOperator(config1, config2, ...etc) {
    //* Return a function that takes an Observable as an arg
    return function (source$) {
        //* This function must return an Observable
        return newObservable$
    }
}

let source$ = of(1, 2, 3, 4, 5);

function doubleOperator() {
    return map(value => value * 2);
}

function quadrupleOperator() {
    return $source => $source.pipe(
        doubleOperator(),
        doubleOperator()
    )
}

source$.pipe(
    quadrupleOperator()
)
.subscribe(
    quadrupleValue => console.log(doubledValue)
)
```



