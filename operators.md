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



