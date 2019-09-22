Global Illumination using Photon Maps
======================================

# Passes

## Title/Teaser/Abstract
- Introduces concept of photon maps
- Significant improvement in GI speed, accuracy, versatility
- Two passes
  1. Two photon maps are tracing from the lights and storing these as they hit surfaces
    - One map is high res for caustics visible to the camera
    - One map is low res for rendering
  2. The scene is rendered by dist rt algo using photon maps
- Are shadow rays sent to photon maps?
- Directional info (scattering BRDF?) is used to estimate radiance on all surfaces (except spec and high-gloss surfaces)
- Estimated radiance on surfaces is used to limit recursion (importance sampling)

## Contributions (in Introduction)
- Photon maps were _not_ introduced in this paper, but in prior work by the author
- Photon maps used to generate optimized sampling directions
- reduces number of shadow rays
- reduces # of reflections

## Skim Conclusions
- Caustics are rendered directly from the caustic photon map
- Photon maps provide an efficient tool for GI

## Skim Results
- Could use photon map to determine spp
- Could use phton map to represent light paths in volumes
- Light tracing scales linearly with # of lights
- The paper mentions adding an additional pass to create a 3-pass method for initial importance information for the photons of the two photon map
  - No implementation is provided for this initial pass
  - As lights scale into the 10,000s for modern scenes, has this become important
- Number of photons is limited by available memory

## _Recent_ Related Work

## Skim Algo/System
- _caustics photon map_ and _global photon map_
- photons stored in balanced kd-tree
- Only send shadow rays when adjacent photons are a mix of shadow photons and direct illumination photons OR if too few adjacent photons
- Never compute caustics using Monte Carlo sampling, the caustic photon map is rendered directly

## Abstract, Introduction, Related Work

## Results

## Algorithm/System

## Conclusions


# Paragraph

While not introduced directly in this paper, the idea of photon maps is explored and enumerated. Photon maps provide an efficient means of rendering global illumination, and noticeably improved rendering of caustics. Most of the techniques outlined in the paper are copied over from the author's previous work with other collaborators. Photon maps are created by tracing from the lights to the surfaces in the scene. A low density of tracing from the light produces a simulated direct illumination (to be later used for global illumination). A high denisty of rays are traced to render caustics. This paper (and previous papers) single out caustics as requiring a higher denisty pass, but other, high-information denisty visual effects could likewise benefit from distinct high-density light tracing. The number of shadow rays for direct illumination is reduced by referring to the local photon maps: Areas with adjacaent direct illumination photons and shadow photons, or areas with too few of both, have shadow rays sent, otherwise none are sent and the photon maps can be referenced directly.