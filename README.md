# Canvas

`Canvas` is the sky package that ships with
[Audiosurf Tweaker](https://github.com/Unchpokable/Audiosurf-Tweaker): two skies in one, split by
the horizon, driven by the song.

- **Upper sky — Chroma.** A calm gradient with cloud, aurora and an iridescent film over it.
- **Lower sky — Dying Sun.** A swollen eclipse arc under a red haze.
- **Which one fills the screen** follows the ride: the split is a knob (`Horizon → Split`), and every
  layer fades by its own intensity, so the picture changes with the music instead of staying put.

The package is a folder — `Config.json`, shaders, a texture and `scripts/clouds.lua`. The clouds are
a sprite layer placed by Lua and lit from the sky's own lights. This variant bakes its noise into a
volume texture (`textures/noise_p8_n128.dds`), which is what makes the upper film and the haze cheap
enough to run every frame.

## Install

Copy the folder, or the release zip renamed to `Canvas.sky`, into
`Audiosurf\engine\TweakerStuff\SkyboxReplacer\Skyboxes\`, then pick **Canvas** in the Skybox tab of
the in-game overlay. It needs Audiosurf Tweaker with the in-game plugin installed. Saving a file in
the installed folder reloads the sky.

## What is in here

| | |
|---|---|
| `Config.json` | The package manifest: layers, lights, shared values, bindings and the sliders the sky offers. Maintained by hand; it is what the plugin loads. |
| `shaders/canvas.hlsl` | The fullsky pixel shader. |
| `shaders/clouds.vs.hlsl`, `shaders/clouds.ps.hlsl` | The sprite-cloud shader pair. |
| `scripts/clouds.lua` | Where the clouds are placed, and what they are painted with. |
| `textures/noise_p8_n128.dds` | The baked 3D noise the shaders sample. |

The manifest is the source of truth for a package. The `@sky` annotation block inside the shader is
read by offline tools and by the loose-shader path only; a knob that exists only there does nothing
in a package.

## Release

A tag `vX.Y.Z` packages the contents of this repository as `Canvas.sky` and attaches it to the
GitHub release. The folder form and the zip form load identically — the zip is what you ship, the
folder is what you edit.

## Licence

MIT, see [LICENSE](LICENSE). The sky manual lives in the Tweaker's repository:
[Docs/skyboxes.md](https://github.com/Unchpokable/Audiosurf-Tweaker/blob/HEAD/Docs/skyboxes.md).
