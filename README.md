# Turing Soup

A GPU Gray-Scott reaction-diffusion playground with an F–k parameter pad, paintable chemicals, and bioluminescent color maps.

**Status: early scaffold.** The repository currently contains the Vite + TypeScript project shell; the simulation described above is not implemented yet. `PLAN.md` describes the intended implementation.

## Planned

- Real-time Gray-Scott reaction-diffusion on the GPU (WebGL fragment shaders)
- Interactive F / k parameter pad with presets
- Painting chemicals onto the field with mouse or touch
- Bioluminescent-style color maps

## Run

```bash
npm install
npm run dev
npm test
npm run build
```

Requires WebGL.

## License

MIT
