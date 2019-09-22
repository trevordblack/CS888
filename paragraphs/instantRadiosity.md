Instant Radiosity
==================

# Paper

## Title/Teaser/Abstract
- Pretty Pictures
- The title is descriptive
  - Instant, zero time
  - Radiosity, rendering method for GI by reflections off diffuse surfaces
- Not sure if Radiosity was defined here, or in earlier literature
- Very little of the algo is covered in the abstract
- An extension of the rendering equation
- Utilization of graphics hardware !!!
- "Deterministic technique" for solving GI
- "Jittered low discrepancy sampling"

## Contributions (in Introduction)
- Quasi-random walk in hardware (gpu) only using the rendering eq
- "Resume the mathematical model" of GI problem
- quasi-Monte Carlo integration and quasi-random walk principle
- Extensions of basic algo
  - AA using jittered LDS
  - Specular effects
  - realtime application ???

## Skim Conclusions
- New method of rendering from the radiance equation (rendering equation?)
- M point lights are created across all light sources
- 1 point lights is used to generate one image
- M images are superimposed for the final image
- Can use existing ray-intersection techniques
- Any light requires an isometry from light space to a unit-square
- Jittered LDS

## Skim Results
- Jittered Hammersley converges best of 4 sampling techniques

## _Recent_ Related Work

## Skim Algorithm/System
- Within the context of_radiosity_, the BRDF is simplified
  $$ f_r = f_d(y) := \frac{\rho_d(y)}{\pi} $$
  - rho_d is just the reflectivity (color) of the (assumedly diffuse) surface
- Use of the Halton sequence in the quasi-Monte Carlo
- Hammersley sequence points are guaranteed to be a minimum distance from each other
  - But it is prone to aliasing
- The paper introduces jittering the Hammersley sequence to remove instances of aliasing
- Realtime effects
  - The last N frames are stored and averaged to produce temporal anti-aliasing

## Abstract, Introduction, Related Work

## Results

## Algorithm/System (maybe rederive)

## Conclusions


# Paragraph

The paper introduces a number of new techniques specific to the task of solving for global illumination through the task of solving for radiosity. While radiositiy has fallen out of the common literature today, it was a valuable tool at the time of the paper's publication. The techniques introduced are still in use today. Lights are sampled by mapping the area of the light emission to the unit square, I could not determine if this was novel at the time of publication. Rays are traced from the light and are path traced through the scene according to diffuse reflection. The choice of random number generation was created with the novel introduction of a low discrepancy sampling by combining the existing two-dimensional Hammersley sampling sequence and jittering by way of strata. While graphics hardware was not wholly at the time of the publication, the paper represents the first concerted effort to expose this hardware for use in photorealistic path tracing.