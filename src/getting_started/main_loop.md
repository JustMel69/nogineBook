# Creating the Main Loop

The **main loop** of an application is, as its name implies, the loop that handles the logic that must be constantly executed.

Luckily for us, **Nogine** automatically handles most of the main loop handling, so the required setup is minimal. A basic main loop in **Nogine** works like so:
```rust,ignore
use nogine::window::{WindowMode, WindowCfg};

fn main() {
    let window_cfg = WindowCfg::default()
        .res((1280, 720))
        .title("Hello Window!")
        .mode(WindowMode::Fullscreen);

    let mut window = window_cfg.init().expect("Couldn't open the window.");

    while window.is_running() {
        window.pre_tick(None);
        window.post_tick();
    }
}
```

In case you are wondering why the first parameter of the `.pre_tick()` method is `None`, this will be answered in the [Custom Render Pipeline](../adv_graphics/custom_render_pipeline.md) chapter, but there's no need to worry about that currently.