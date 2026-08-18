# mithril

A real-time 3D renderer written from scratch in C++20 + OpenGL 4.1 core, on Apple
Silicon macOS. Not a game engine — no ECS, no editor, no scripting layer, no asset
pipeline. Goal of the OpenGL phase: render Sponza at 60fps with PBR materials, IBL,
cascaded shadow maps, and a post-processing stack, then port the render layer to Metal.

## Building

Requires CMake ≥ 3.20 and a C++20 compiler (tested with Apple Clang).

```sh
cmake -S . -B build
cmake --build build
./build/mithril
```

GLFW is fetched automatically via CMake's `FetchContent`. glad2 (OpenGL 4.1 core
loader) is vendored under `third_party/`.

## Stack

| Concern | Choice |
|---|---|
| Language | C++20 |
| Window/input | GLFW |
| GL loader | glad2 (GL 4.1 core) |
| Math | glm |
| Images | stb_image |
| Models | cgltf (glTF 2.0) |
| UI | Dear ImGui (debug HUD only) |

## Status

Phase 0 (toolchain) — window, clear color, hardcoded triangle.
