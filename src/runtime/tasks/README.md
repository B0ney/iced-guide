# Tasks
> *Note:* In versions prior to `0.13.0`, `Task`s were originally called `Command`s.

A task is "A set of asynchronous actions to be performed by some runtime".

Basically, a task is just a [`Stream`](https://docs.rs/futures/latest/futures/stream/trait.Stream.html) that returns messages.

A task will run until it has finished and can return multiple messages during its execution.

Tasks not only allow you to run asynchronous code, but they also allow you to interact with the iced runtime; for example, [resizing the window](https://docs.rs/iced/latest/iced/window/fn.resize.html), [changing the window icon](https://docs.rs/iced/latest/iced/window/fn.change_icon.html), or outright [closing the application](https://docs.rs/iced/latest/iced/fn.exit.html). This is what distinguishes them from Subscriptions. 

## Executing a Task
In your App, you can execute a task by returning it from the [update](https://docs.rs/iced/latest/iced/application/trait.Update.html) function of your application.


Augment your app's update code if you haven't already:
```rust
pub fn update(&mut self, message: Message) -> Task<Message> {
    match message {
        /* code omitted for simplicity */
    }

    Task::none()
}
```

## Batch multiple tasks
Sometimes you want to return more than one task. 
For that, you can use the [Task::batch](https://docs.rs/iced/latest/iced/task/struct.Task.html#method.batch) function to batch a few of them together like this:
```rust
return Task::batch(vec![task1, task2, task3]);
```


