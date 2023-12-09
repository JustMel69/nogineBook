# Forcing Framerate

Something related to the main loop is forcing a framerate. This is actually desirable in many cases to reduce the strain on CPU and GPU resources.

The `Window` type comes with a `.force_framerate()` method to do exactly this, altough it needs some setup.

The `.force_framerate()` method requires two parameters, the `last_frame` and the `target_framerate`.

## Obtaining the Last Frame

To obtain the last frame we can do something like this:
```rust,ignore
use std::time::Instant;

use nogine::window::{WindowMode, WindowCfg};

fn main() {
    // --snip--

    let mut last_frame = Instant::now();
    while window.is_running() {
        window.pre_tick(None);

        // Game logic here

        window.post_tick();
        last_frame = Instant::now();
    }
}
```

## Forcing Framerate

Once we have the last frame, we can finally call the `.force_framerate()` method. It must be called before modifying the `last_frame` variable.
```rust,ignore
use std::time::Instant;

use nogine::window::{WindowMode, WindowCfg};

fn main() {
    // --snip--

    let mut last_frame = Instant::now();
    while window.is_running() {
        window.pre_tick(None);

        // Game logic here

        window.post_tick();
        window.force_framerate(last_frame, 60.0 /* fps */);
        last_frame = Instant::now();
    }
}
```

## Obtaining the Timestep

Forcing the framerate only guarantees that the framerate will not **excede** the target framerate, but on lower end devices or poorly optimized games the framerate may be much less than the target.

For this very reason, it is desirable to have a `time_step` variable.
```rust,ignore
use std::time::Instant;

use nogine::window::{WindowMode, WindowCfg};

fn main() {
    // --snip--

    let mut last_frame = Instant::now();
    let mut time_step: f32 = 1.0 / 60.0;
    while window.is_running() {
        window.pre_tick(None);

        // Game logic here

        window.post_tick();

        window.force_framerate(last_frame, 60.0 /* fps */);
        time_step = last_frame.elapsed().as_secs_f32();
        last_frame = Instant::now();
    }
}
```