# NTSC frei0r plugin

[frei0r](https://dyne.org/software/frei0r/) filter plugin based on [ntsc-rs](https://ntsc.rs).
[ffmpeg](https://ffmpeg.org/ffmpeg-filters.html#frei0r-1) and [MLT](https://www.mltframework.org/features/)
both support frei0r plugins.

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

Scale `input.mp4` to 480p and apply the ntsc filter using a preset:
```sh-session
FREI0R_PATH=target/release ffmpeg -i input.mp4 \
  -vf scale=size=640x480:force_original_aspect_ratio=decrease:reset_sar=1:flags=lanczos,frei0r=ntsc:presets/Low-Power-NTSC.json \
  -y output.mp4
```

Apply ntsc filter to a testcard video:
```sh-session
FREI0R_PATH=target/release ffmpeg -f lavfi \
  -i testsrc2=duration=4:size=640x480:rate=30 \
  -vf frei0r=ntsc:presets/Low-Power-NTSC.json \
  -pix_fmt yuv422p \
  -y output.mp4
```

Result:

https://github.com/user-attachments/assets/1cd369f0-4218-4a78-9295-030933893e7f
