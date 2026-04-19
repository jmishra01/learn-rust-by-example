# Scalar Type

## Signed Integers

`i8`, `i16`, `i32`, `i128`, and `isize`.

```rust,editable
fn main() {
    {
        let mut x: i8 = 127;
        x = x.wrapping_add(1);
        println!("{:?}", x);
    } 
    // Add two numbers of different integer types
    {
        let x: i8 = 10;
        let y: i16 = 100;
        let z = (x as i16) + y;
        
        println!("{:?}", z);
    }
    // Max value of each integer types
    {
        println!("Max value of i8: {:?}", i8::MAX);
        println!("Max value of i16: {:?}", i16::MAX);
        println!("Max value of i32: {:?}", i32::MAX);
        println!("Max value of i128: {:?}", i128::MAX);
        println!("Max value of isize: {:?}", isize::MAX);
    }
}
```