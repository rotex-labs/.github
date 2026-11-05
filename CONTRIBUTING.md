# Contributing to Rotex

Thanks for helping. This guide applies to every repository in `rotex-labs` that does not have its own `CONTRIBUTING.md`.

## How the code is organised

Rotex is a set of Rust crates. Crates that change together live in one repository. GPU backends stay in their own repositories. Open issues and pull requests on the repository that contains the crate.

| Repository | Crates |
|---|---|
| [`rotex-math`](https://github.com/rotex-labs/rotex-math) | `rotex-math`, `rotex-color` |
| [`rotex-core`](https://github.com/rotex-labs/rotex-core) | `rotex-types`, `rotex-core`, `rotex-conformance`, `rotex-graph`, `rotex-emulation` |
| [`rotex-shader`](https://github.com/rotex-labs/rotex-shader) | `rotex-shader-core`, `rotex-shader-cooker` |
| [`rotex-window`](https://github.com/rotex-labs/rotex-window) | `rotex-window`, `rotex-winit` |
| [`rotex-vulkan`](https://github.com/rotex-labs/rotex-vulkan), [`rotex-wgpu`](https://github.com/rotex-labs/rotex-wgpu), [`rotex-gl`](https://github.com/rotex-labs/rotex-gl), [`rotex-d3d12`](https://github.com/rotex-labs/rotex-d3d12) | one backend each |

Dependencies only point downward. Inside a slice repository, sibling crates depend on each other by path plus version. A dependency that crosses repositories names a published crates.io version.

Rules of thumb:
- Backend-specific concepts (SPIR-V details, descriptor-set indices, D3D root signatures) stay in the backend crate, never in the spine.
- A new feature is a **vertical slice**: types in `rotex-types`, a capability trait or marker in `rotex-core`, an implementation in each backend that supports it, and conformance tests, in one change.
- Every backend reports the feature as **Native**, **Emulated** or **Absent**. Emulation must be explicit and documented.
- Core slices must behave the same on every backend. Optional hardware features (ray tracing, mesh shaders, bindless, VRS) are extension slices behind `Supports<Feature>`.

## Building

You need a stable Rust toolchain (`rustup`) and, for the Vulkan backend, a Vulkan driver (the Vulkan SDK helps for validation layers).

```sh
cargo build --workspace
cargo test --workspace
cargo fmt --all -- --check
cargo clippy --workspace --all-targets -- -D warnings
# web targets
rustup target add wasm32-unknown-unknown
cargo check -p rotex-wgpu --target wasm32-unknown-unknown
```

In a slice repository, keep `--workspace`. In a single-crate backend repository, drop it.

## Conformance tests

Backend behaviour is checked by tests that run the same scenario on every available backend and compare results against the capability each backend reports. When you add or change a slice:
- add a test that runs on every backend that reports it Native or Emulated, and that checks Absent backends reject it at compile time or report it Absent;
- run the tests on every backend you have hardware or drivers for, and say in the PR which ones you ran;
- tests that need a GPU should skip cleanly when no adapter is found, so CI on headless runners still passes.

## Commits and pull requests

- Use [Conventional Commits](https://www.conventionalcommits.org/): `feat(vulkan): ...`, `fix(core): ...`, `docs: ...`, `refactor(types)!: ...` for breaking changes. The scope is the crate name without `rotex-`.
- Keep pull requests focused; one slice or fix per PR.
- Run `fmt`, `clippy` and tests before pushing.
- Breaking API changes need a note in the PR description and the crate changelog.

## Code of conduct

Everyone taking part follows the [Code of Conduct](CODE_OF_CONDUCT.md).

## License

By contributing you agree that your contribution is licensed under the MIT License used by the crate.
