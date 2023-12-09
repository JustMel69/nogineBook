# Graphics Setup

To start displaying graphics, some setup is necessary to ensure the rendered data will display properly.

We will setup the following parameters before continuing:
- [Pixels per unit](#pixels-per-unit).
- [Camera data](#camera-data).
- [Clear color](#clear-color).

## Pixels per Unit

**Pixels per unit** (PPU) defines the number of pixels that fit inside a "spatial unit". **PPU** can be set at any time, and the associated functions are the following:
```rust,ignore
Graphics::set_pixels_per_unit // Sets the current pixels per unit
Graphics::get_pixels_per_unit // Returns the current pixels per unit
```

## Camera Data

The **camera data** defines which objects will be viewed by the camera, and therefore, be rendered. Camera data can be set with the following function:
```rust,ignore
Graphics::set_cam(pos, size)
```
In most cases, `size` should follow the window's aspect ratio. The aspect ratio can be obtained with the `.get_aspect_ratio()` method.

Because the aspect ratio may change if the player changes the window size, you should set the camera data every frame.

## Clear Color

The **clear color** is the color of the screen background. The functions associated with clear color are the following:
```rust,ignore
Graphics::set_clear_col // Sets the clear color
Graphics::get_clear_col // Returns the clear color
```

You only need to run the set function once, so you can do it before the main loop.