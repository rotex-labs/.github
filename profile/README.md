<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/rotex-readme-banner-dark.svg">
    <source media="(prefers-color-scheme: light)" srcset="assets/rotex-readme-banner-light.svg">
    <img alt="Rotex: One API. Every GPU. Zero cost." src="assets/rotex-readme-banner-light.svg" width="1200">
  </picture>
</p>

**Rotex Engine** is a modular Rust graphics engine. Its core is one rendering API over **Vulkan**, **Direct3D 12**, **OpenGL / WebGL** and **wgpu**, built from small crates and vertical feature slices. Zero-cost abstraction (static dispatch, no per-command allocation) is a core design goal and is being worked toward; it is not shipped yet.

- **Core slices** behave the same on every backend.
- **Extension slices** (ray tracing, mesh shaders, bindless and others) are opt-in at compile time through `Supports<Feature>`.
- Every feature reports **Native**, **Emulated** or **Absent** for each backend, so nothing fails silently.

### Crates

| Crate | Layer | What it does |
|---|---|---|
| [`rotex-types`](https://github.com/rotex-labs/rotex-types) | spine | Descriptors, formats, capability model |
| [`rotex-core`](https://github.com/rotex-labs/rotex-core) | spine | `Device`, command encoders, capability traits |
| [`rotex-vulkan`](https://github.com/rotex-labs/rotex-vulkan) | backend | Vulkan via `ash` |
| [`rotex-wgpu`](https://github.com/rotex-labs/rotex-wgpu) | backend | wgpu: WebGPU, Metal and more |
| [`rotex-d3d12`](https://github.com/rotex-labs/rotex-d3d12) | backend | Direct3D 12 *(in progress)* |
| `rotex-gl` | backend | OpenGL 4.x / ES 3 / WebGL2 *(planned)* |
| [`rotex-graph`](https://github.com/rotex-labs/rotex-graph) | graph | Render graph with automatic barriers |
| [`rotex-shader-core`](https://github.com/rotex-labs/rotex-shader-core) | tools | Shared shader types |
| [`rotex-shader-cooker`](https://github.com/rotex-labs/rotex-shader-cooker) | tools | One shader source cooked for every backend |
| [`rotex-window`](https://github.com/rotex-labs/rotex-window) / [`rotex-winit`](https://github.com/rotex-labs/rotex-winit) | platform | Window abstraction and winit integration |
| [`rotex-math`](https://github.com/rotex-labs/rotex-math) / [`rotex-color`](https://github.com/rotex-labs/rotex-color) | utility | Math and color types |

### Backend status

<p>
  <img src="assets/badges/rotex-backend-vulkan-active.svg" alt="Vulkan: active" height="28">
  <img src="assets/badges/rotex-backend-wgpu-active.svg" alt="wgpu: active" height="28">
  <img src="assets/badges/rotex-backend-d3d12-in-progress.svg" alt="D3D12: in progress" height="28">
  <img src="assets/badges/rotex-backend-opengl-planned.svg" alt="OpenGL: planned" height="28">
  <img src="assets/badges/rotex-backend-webgl-planned.svg" alt="WebGL: planned" height="28">
  <img src="assets/badges/rotex-backend-metal-planned.svg" alt="Metal: planned" height="28">
</p>

<sub>Brand assets: <a href="https://github.com/rotex-labs/rotex-assets">rotex-assets</a> · Code licensed under MIT</sub>
