# Soft Jelly Interaction

An interactive soft-body jelly simulation exploring deformation, elasticity, material response, and tactile digital interaction in real time.

**[Launch the interactive experience](https://iiiiiiiian.github.io/soft-jelly-interaction/)**

[![Soft Jelly Interaction](docs/soft-matter-jelly-lab.png)](https://iiiiiiiian.github.io/soft-jelly-interaction/)

## Overview

Soft Jelly Interaction is a browser-based experiment built around a deformable 3D jelly form. Rather than treating the object as a predefined animation, the project simulates its physical structure in real time, allowing users to grab, pull, release, and observe localized deformation across the surface.

The project focuses on the relationship between soft-body physics, translucent material rendering, and direct interaction.

## Interaction

- Click or touch anywhere on the jelly surface and drag it.
- Pulling different regions produces localized deformation.
- Release the jelly to observe its elastic and inertial response.
- Switch between Berry, Mint, and Honey material variations.
- Adjust stiffness and internal damping independently.
- Reset the jelly while preserving the current material parameters.
- Sliders support keyboard controls including arrow keys, `Home`, and `End`.

## Technical Implementation

### Soft-Body Simulation

`lib/soft-body.ts` implements a CPU-based XPBD soft-body solver.

The simulation uses:

- 343 particles
- 1,296 tetrahedral volume constraints
- elastic edge constraints
- gravity
- ground friction
- velocity damping
- a fixed 120 Hz simulation step

Simulation states are interpolated to drive a higher-resolution visual surface.

Raycast barycentric coordinates map the exact grab position on the rendered mesh back to simulation particles. This allows interaction to create localized stretching and deformation rather than simply transforming or scaling the entire object.

### Rendering

`lib/jelly.ts` contains the Three.js rendering system.

The visual material combines:

- physically based transmission
- double-sided surfaces
- clearcoat
- light absorption
- approximate thickness information

- refracted environmental lighting
- dynamically updated normals
- soft contact shadows

The renderer prioritizes WebGPU and falls back to WebGL2 when WebGPU is unavailable.

### Interface

`app/page.tsx` manages interaction controls and the application interface.

The project runs entirely in the browser and does not require server-side data storage.

## Running Locally

Requires Node.js 22.13 or later.

```bash
npm install
npm run dev
```

Open the localhost address displayed in the terminal.

To create a production build:

```bash
npm run build
```

The generated static site can be deployed through GitHub Pages or another static hosting service.

WebGPU requires HTTPS or localhost. Browsers without WebGPU support automatically fall back to WebGL2.

## AI-Assisted Development

This project was developed with AI-assisted coding and iteration using **GPT-6 Astra**, including support for implementation, debugging, interaction refinement, and technical development.

The project concept, interaction direction, visual decisions, testing, and final implementation were developed through an iterative human-AI workflow.

## Repository

**Source:** [github.com/iiiiiiiian/soft-jelly-interaction](https://github.com/iiiiiiiian/soft-jelly-interaction)

**Live:** [iiiiiiiian.github.io/soft-jelly-interaction](https://iiiiiiiian.github.io/soft-jelly-interaction/)
