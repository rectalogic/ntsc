# NTSC frei0r plugin

[ffmpeg](https://ffmpeg.org/ffmpeg-filters.html#frei0r-1) and [MLT](https://www.mltframework.org/features/) both support [frei0r](https://dyne.org/software/frei0r/) plugins.

## Build

```sh-session
$ cargo build --release
$ cargo xtask package
# plugin now in target/release
```

## Usage

Copy the plugin to your frei0r plugins directory, or on macOS/Linux set `FREI0R_PATH` environment variable.
Create a preset using the [ntsc-rs application](https://ntsc.rs/docs/standalone-application/)
or download presets from the [ntsc-rs discussions](https://github.com/ntsc-rs/ntsc-rs/discussions).

```sh-session
FREI0R_PATH=target/release ffmpeg -i <input.mp4> \
  -vf scale=size=640x480:force_original_aspect_ratio=decrease:reset_sar=1:flags=lanczos,frei0r=ntsc:path/to/preset.json \
  -y <output.mp4>
```
