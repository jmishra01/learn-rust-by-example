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
    println!("Speed: {}", speed(distance, time));
}
```
