# Lifetime

`PhantomData` forces the compiler to track lifetimes in patterns that involve unsafe code.

The examples below make this easier to understand:

- **Reference with lifetime** - The compiler reports an error at compile time if a value is used after its lifetime has ended.
- **Reference with unsafe code** - The compiler does not enforce the same lifetime checks inside unsafe pointer usage.
- **Reference with unsafe code plus PhantomData** - `PhantomData` makes the compiler enforce lifetime checks.

## Reference with lifetime
The Rust compiler checks the lifetime of each variable. If a variable does not live long enough
and is used after its scope ends, compilation fails with a lifetime error.

```rust,editable

struct Quantity<'a> {
    value: &'a i32
}

impl<'a> Quantity<'a> {
    fn new(n: &'a i32) -> Self {
        Self {
            value: n
        }
    }
}

fn main() {
    let quantity;
    {
        let n: i32 = 10;
        quantity = Quantity::new(&n);
    }
    println!("value: {}", quantity.value);
}
```

## Reference with unsafe code
The Rust compiler does not run the same lifetime checks over unsafe pointer access, so the code below compiles and runs.
The output may appear correct, but it is not reliable.

`Why do we get 42 in the output?`
Because `n` has gone out of scope, but the value `42` may still remain at the memory location pointed to by `ptr`.

```rust,editable
// Use *const i32 pointer to i32 value. No lifetime `'a` symbol required.
struct Quantity {
    ptr: *const i32
}

impl Quantity {
    fn new(n: &i32) -> Self {
        Self {
            ptr: n
        }
    }
}

fn main() {
    let quantity;
    {
        let n: i32 = 42;
        quantity = Quantity::new(&n);
    }
    unsafe {
        println!("value: {}", *quantity.ptr);
    }
}
```

## Reference with unsafe code plus PhantomData
`PhantomData` makes the Rust compiler track the lifetime, and it reports an error if a value is accessed beyond its scope.

Below code will not compile.
```rust,editable
use std::marker::PhantomData;

struct Quantity<'a> {
    ptr: *const i32,
    _marker: PhantomData<&'a i32>
}

impl<'a> Quantity<'a> {
    fn new(n: &'a i32) -> Self {
        Self {
            ptr: n,
            _marker: PhantomData
        }
    }
}

fn main() {
    let quantity;
    {
        let n: i32 = 42;
        quantity = Quantity::new(&n);
    }
    unsafe {
        println!("value: {}", *quantity.ptr);
    }
}
```
