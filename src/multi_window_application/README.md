# Multi-Window Applications

Creating a multi window application can get a little involved.

```rust
use std::collections::HashMap;

enum Message {
    WindowOpened(window::Id),
    WindowClosed(window::Id),
}

enum Window {
    Main,
    Settings,
    Dialog
}

#[derive(Default)]
struct App {
    windows: HashMap<window::Id, Window>,
}

impl App {
    pub fn new() -> (Self, Task<Message>) {
        let (_id, open_window) = window::open(window::Settings::default());

        (Self::Default, open_window.map(Message::WindowOpened))
    }

    pub fn view(&self, window: window::Id) -> Element<Message> {
        match self.windows.get(&window) {
            Some(window) => window.view().into()
            None => horizontal_space().into()
        }
    }
}
```

# Pitfalls to avoid
I won't deny that this is quite a lot of code! Naturally, we might be tempted and try to abstract all of this away with traits:

```rust
trait Window {
    fn update(&mut self);
    fn view(&self)
}


#[derive(Default)]
struct App {
    windows: HashMap<window::Id, Box<dyn Window>>,
}

impl App {
    fn update(&mut self, message: Message) -> Task<Message> {
        todo!()
    }
}
```

but We have our first hurdle: what should `Message` be?

We could try adding a generic parameter:

```rust
trait Window<Message> {
    fn update(&mut self, message: Message) -> Task<Message>;
    fn view(&self) -> Element<Message>;
}
```

```rust
mod settings {
    use crate::data::Config;

    type UpdateFn = fn(&mut Settings);

    enum Message {
        Autosave(bool)
    }

    struct Settings {
        staging: Option<Config>;
    }

    impl Settings {

    }
}
```



or we could just use our top level mess

but we also have another problem: the signature restricts what parameters we can pass!
Traits provide a unified interface for TODO, consequently, if there's a type



# Sharing Data Between Windows