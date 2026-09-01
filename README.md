# Efficient Road Heating System Design

Buried pipes melt snow off a road by warming it from below. How the pipes are laid out decides where the cold spots are, and cold spots are where snow survives. This is a COMSOL study of four layouts, asking which one holds the road surface warmest for the least pipe.

## The four layouts

Each `.mph` file is a full COMSOL Multiphysics model of one pipe cross-section arrangement, run under identical boundary conditions so the geometries can be compared directly.

| Model | Arrangement |
| --- | --- |
| `Line.mph` | Straight parallel pipes |
| `Hexagon.mph` | Hexagonal (honeycomb) |
| `Square.mph` | Square grid |
| `Triangle.mph` | Triangular |

## Method

Each layout was swept across ten geometry scales, from 1.0 down to 0.1. Shrinking the scale packs the pipes closer, which raises the minimum surface temperature but also increases the pipe length needed per unit of road area.

So two quantities are recorded together for every run:

- **pipe length per unit area** — what the layout costs to build and to pump
- **minimum surface temperature** — the coldest point on the road, which is what decides whether snow melts everywhere or only in stripes

Comparing layouts at their own scale is misleading, because a denser layout wins simply by using more pipe. The comparison below holds pipe length roughly constant instead.

## Results

Minimum surface temperature (°C) at comparable pipe length per unit area:

| Pipe length / area | Line | Hexagon | Square | Triangle |
| --- | --- | --- | --- | --- |
| ≈ 3.4 | **−2.84** | −4.13 | −4.59 | −4.62 |
| ≈ 5 | **−0.03** | −1.87 | −3.21 | −3.64 |
| ≈ 10–11.5 | **7.99** | 7.78 | 4.66 | 5.92 |

The straight parallel layout is the most efficient of the four: at every matched pipe length it holds the coldest point on the surface warmer than the others do. The triangular layout reaches the highest absolute temperatures in the raw sweep, but only by using roughly 3.5× the pipe — once that is accounted for it is the weakest of the four.

The practical reading is that the intuition "a more elaborate layout spreads heat better" does not hold here. Simple parallel runs win on heat delivered per meter of pipe.

## Opening the models

COMSOL Multiphysics 6.x with the Heat Transfer module. Open a `.mph` file directly — geometry, materials, boundary conditions and the study are all stored inside it.

## Context

Computer-Aided Engineering coursework, Hanyang University, 2023.
