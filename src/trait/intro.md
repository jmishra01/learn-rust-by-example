# Trait

Trait are used to define shared behaviour that different types can implement.

## Without using trait

Without using trait, each struct have to implement print_field method.
As the number of struct increase, duplicate code increase.
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
Shared behavior (here `field` method), is implement by struct. 
`show_field` implemented as function, which take two arguments,
`name` and reference of `Machine`. Any struct which implement
trait `Machine` method can pass as reference to the second 
argument of `show_field` function.

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