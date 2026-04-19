# Closure

Closure is an anonymous function that can `capture` variables from its surrounding environment.

```rust,editable
fn main() {
    let pi: f32 = 3.14;
    
    // Single line closure.
    let area = |x: f32| pi * x * x;
    
    let n: f32 = 10.0;
    let result = area(n);
    
    println!("Area of cicle: {}", result);
}
```


