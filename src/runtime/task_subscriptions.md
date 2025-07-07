# Tasks and Subscriptions
As you develop your iced application, you will eventually need to run code that takes TODO.

If you try to run code in your update function:

```rust
fn update(&mut self, message: Message) {
    match message {
        Message::ParseDocument(document) => {
            // ???
        }
    }
}
```

Or if you need to listen to RF (Radio Frequency) signal recorded by a raspberry-pi.




Tasks and Subscriptions are two sides of the same coin - both use the streams to run asynchronous code.

Therefore, it would make sense to understand streams and their properties.



<!-- Sometimes you have a task that takes some time to complete and should run in the background.
If you run it in your update function, the GUI becomes locked and unresponsive until the task is finished.
This could be a web request or an operation that listens for external events.

Iced offers two solutions to this issue: `Task` and `Subscription`.

A task runs until it completes, whereas a subscription continues running as long as the application requires it.

In this chapter, we will examine both solutions and explore how to use them.
 -->

## When to use Tasks

## When to prefer Subscriptions
