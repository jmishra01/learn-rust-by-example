# From Trait

```rust,editable
struct FromValue {
    value: String
}

impl From<&str> for FromValue {
    fn from(name: &str) -> FromValue {
        FromValue {
            value: name.into()
        }
    }
}

impl From<i32> for FromValue {
    fn from(value: i32) -> FromValue {
        FromValue {
            value: value.to_string()
        }
    }
}

fn main() {
    let from_value: FromValue = FromValue::from("helloWorld");
    println!("{}", from_value.value);

    let from_value: FromValue = FromValue::from(100);
    println!("{}", from_value.value);
}
```