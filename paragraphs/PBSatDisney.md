Physically-Based Shading at Disney
=====================================

# Passes

- New material model
- "virtually all" materials were PBS except for hair
- Separate normal for glint
- New sampled area lights
- New Image based lights
- Material library is simplified
- All materials can be represented as a texture corresponding to light angle and grazing angle starting from a grazing angle of 90 degrees
- Development of a "principled" material model, rather than entirely physically based, due to concerns of artists
- Addition of principles that aid in artist creation.

# Paragraph

The paper presents a new physically-based reflectance model designed to be artist friendly and as complete as possible. While not new at the time of the paper, the paper also pushes the importance of lighting under area lights and image based lights. Lastly, the paper also explains that the bidirectional reflectance model for any material can be completely defined by an image texture spanning grazing angle and lighting angle. It appears as if the paper was the first practical attempt at oranizing all 100 materials of the Mitsubishi Electric Research Laboratories MERL 100 into a single unified material shading model. It was not made explicit in the model, but many of the principles underlying the shading model are common engineering today, and may have been started here. Namely, the principles are: Intuitive over physical parameters, fewer parameters is better, should span zero to one, but be allowed to extend where sensible, and all combinations of all parameters should be robust and plausible.