# Trait

Traits are used to define shared behavior that different types can implement.

## Without using trait

Without a trait, each struct has to implement the `print_field` method on its own.
As the number of structs increases, the amount of duplicated code also increases.
```rust,editable
struct Car {
    name: String
}

struct Bike {
    name: String
}
impl Car {
    fn print_field(&self) {
        println!("Name of car is `{}`", self.name);
    }
}

impl Bike {
    fn print_field(&self) {
        println!("Name of bike is `{}`", self.name);
    }
}

fn main() {
    let car = Car {name: "Hyundai Creta".into()};
    let bike = Bike {name: "Royal Enfield: Meteros".into()};
    
    car.print_field();
    bike.print_field();
    
}
```

## Using trait
The shared behavior here is the `field` method, which is implemented by each struct.
The `show_field` function takes two arguments: `name` and a reference to `Machine`.
Any struct that implements the `Machine` trait can be passed as the second argument to `show_field`.

```rust,editable
trait Machine {
    fn field(&self) -> &str;
}

struct Car {
    name: String
}

struct Bike {
    name: String
}

impl Machine for Car {
    fn field(&self) -> &str {
        &self.name
    }
}

impl Machine for Bike {
    fn field(&self) -> &str {
        &self.name
    }
}

fn show_field(name: &str, machine: &dyn Machine) {
    println!("Name of {} is `{}`", name, machine.field());
}

fn main() {
    let car = Car {name: "Hyundai: Creta".into()};
    let bike = Bike {name: "Royal Enfield: Meteros".into()};

    show_field("car", &car);
    show_field("bike", &bike);
}
```
