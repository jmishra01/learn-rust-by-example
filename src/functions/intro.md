# Functions

## Intro
Function is a block of code, mainly focus on single task.
It can take input arguments, and return a value of certain types. Input arguments and return values is optional

In Rust, you can define function with keyword `fn` followed by function name, and a set of parentheses.
Curly brackets contain function body.


```rust,editable
fn pi() -> f32 {
    3.14
}
fn main() {
    let r: f32 = 10.0;
    let pi_value = pi();
    
    println!("Area of cirle: {}", pi_value * r * r);
}
```

## Return

- **Implicit Return**: Last expression in a block (without a semicolon) is automatically returned.
- **Explicit return**: Using the `return` keyword for early returns.

```rust,editable
fn fibonacci_series(n: i32) -> i32 {
    // Use `return` keyword to return value.
    if n < 1 { return 0; }
    if n < 2 { return 1; }
    // Last statement of function block without semicolon, return implicitly.
    fibonacci_series(n - 1) + fibonacci_series(n - 2)
}

fn main() {
    let n = 10;
    let result = fibonacci_series(n);
    println!("Fib({}) => {}", n, result);
}
```
