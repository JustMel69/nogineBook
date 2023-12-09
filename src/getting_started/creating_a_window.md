# Creating a Window

Creating a window in **Nogine** revolves around a `WindowCfg` object. This object defines the initial configuration of your window, following the [builder pattern](https://en.wikipedia.org/wiki/Builder_pattern).

`WindowCfg` allows to set these initial parameters:
- **Resolution** through the `.res()` method.
- **Title** thorugh the `.title()` method.
- **Window mode** through the `.mode()` method.

First, we'll create a `WindowCfg` object.
```rust,ignore
use nogine::window::{WindowMode, WindowCfg};

fn main() {
    let window_cfg = WindowCfg::default()
        .res((1280, 720))
        .title("Hello Window!")
        .mode(WindowMode::Fullscreen);
}
```

Once we have our `WindowCfg`, we can initialize the window by calling the `.init()` method. This method will return an instance of the `Window` type with the provided configuration.
To prevent the application from closing, we'll add a `loop {}` after creating the window.
```rust,ignore
use nogine::window::{WindowMode, WindowCfg};

fn main() {
    let window_cfg = WindowCfg::default()
        .res((1280, 720))
        .title("Hello Window!")
        .mode(WindowMode::Fullscreen);

    let window = window_cfg.init().expect("Couldn't open the window.");

    loop {};
}
```

If you execute the code now, you'll find that the window will not behave properly. This is normal as we are not currently handling any window event, but we'll address it in the next chapter.