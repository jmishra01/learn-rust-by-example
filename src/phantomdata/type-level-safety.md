# Type-Level Safety

`PhantomData` prevents mixing different kinds of units at the type level.

```rust,editable
use std::marker::PhantomData;

struct Meter;
struct Second;

struct Quantity<Unit> {
    value: f64,
    _unit: PhantomData<Unit>
}

type Distance = Quantity<Meter>;
type Time = Quantity<Second>;

fn speed(d: Distance, t: Time) -> f64 {
    d.value / t.value
}

fn main() {
    let distance: Distance = Distance {value: 10.0, _unit: PhantomData};
    let time: Time = Quantity {value: 5.0, _unit: PhantomData};
    
    // This code will not compiled. As we passing the datatype is different.
    // Comment below line, and uncomment line next line. Then code compile and run.
    let result = speed(time, distance);
    // let result = speed(distance, time);
    
    println!("Speed: {}", result);
}
```

## Type-safety without using PhantomData
Use can also achieve type safety without using PhantomData also. 


```rust,editable

struct Distance(f64);
struct Second(f64);

fn speed(distance: Distance, time: Second) -> f64 {
    distance.0 / time.0
}

fn main() {
    let distance = Distance(10.0);
    let time = Second(5.0);
    
    // This code will not compiled. As we passing the datatype is different.
    // Comment below line, and uncomment line next line. Then code compile and run.
    let result = speed(time, distance);
    // let result = speed(distance, time);
    
    println!("Speed: {}", result);
}
```