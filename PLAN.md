# Turing Soup — plan

A GPU Gray-Scott reaction-diffusion playground with an F-k parameter pad,
paintable chemicals, and bioluminescent color maps.

## Goal

Drag across the F-k pad and watch the texture morph live — mitotic dividing
spots, coral, worms, waves — without ever resetting the simulation. Everything
runs in WebGL2 fragment shaders; a CPU reference stepper mirrors the shader so
the numerics can be unit-tested.

## Features

- WebGL2 ping-pong float framebuffers (RGBA16F) running Gray-Scott in GLSL
- 2D F-k parameter pad (Pearson map) with named presets:
  mitosis, coral, worms, spots, waves
- Click / drag on the canvas to paint chemical B
- Speed control (1–32 iterations per frame) and pause
- Color LUT picker (teal-magenta, ember, monochrome) applied in a display shader
- Reset with random seed patches or a centered seed
- Snapshot PNG export

## Core algorithm

Gray-Scott PDE, integrated per texel:

```
A' = Da * lap(A) - A*B^2 + F*(1 - A)
B' = Db * lap(B) + A*B^2 - (F + k)*B
```

3x3 weighted Laplacian: centre -1, edges 0.2, corners 0.05. Two RGBA16F
textures alternate as read/write targets. The F-k pad maps linearly to
F in [0, 0.08] and k in [0.045, 0.07].

## Architecture

```
src/
  core/
    grayscott.ts   DOM-free: laplacian, cpuStep, padToParams, presets, LUTs
    grayscott.test.ts
  gl/
    shaders.ts     GLSL sources (sim + display), shared with the CPU reference
    renderer.ts    WebGL2 context, ping-pong FBOs, paint, snapshot
  ui/
    pad.ts         F-k pad (square picker with crosshair, keyboard support)
    controls.ts    icon rail, speed, LUT, reset, export
  main.ts          wiring + render loop
  style.css        pitch-black stage, dim-cyan monospace readouts
```

## Milestones

1. Plan, license, scaffold
2. Core math + vitest (spec assertions)
3. WebGL2 renderer with ping-pong sim + display LUTs
4. F-k pad, presets, painting, speed, reset, export
5. Polish: responsive to ~380px, keyboard, focus states, smoke test
6. README, publish
