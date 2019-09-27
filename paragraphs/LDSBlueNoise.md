A Low-Discrepancy Sampler that 
Distributes Monte Carlo Errors as a Blue Noise in Screen Space
===============================================================

# Passes

## Title/Teaser/Abstract
- Not sure how the sampler (and sample locations) has an effect on the color of the noise
- Much higher quality visuals than Random LD Sampler
  - What is "Random LD Sampler"
  - Just jittering?
- Two key properties of visual fidelity
  - Owen-Scrambled Sobol sequence
  - Errors dist as blue noise in screen space
- For even Monte Carlo noise, the image with blue noise will be perceived better
- This gamma is rarely accounted for in the math

## Contributions (in Introduction)
- Owen-scrambled Sobol sequences
- Sobol sequences can be modified by _scrambling_ and _ranking_
  - Their values are _scrambled_
  - Their order is _ranked_
- Neither of these operations negatively impact convergence
- Does not optimizer over a sample-space distance
- Introduces an energy term to optimize for blue noise
- The optimization works over arbitrary sample counts (N) and dimensions of the sample space (D)

## Skim Conclusions
- Works best with low Dimensional sample space
- Works best with smooth integrands (low spatial frequency)
  - Especially DI from area light
- Optimizing for high dimensions (large D) decreases quality in lower dimensions
  - e.g. for D=4, dimensions 1 and 2 have reduced quality
- Found repeating D=2 multiple times is best compromize
- "No significant drawbacks" ... ***spit take***
- As good as prior art _dithered sampling_ at 1spp
  - better results than prior art at higher spp
- Extrememly fast
  - 3 memory fetchs
  - 2 xors per sample (basically free)

## Skim Results

## _Recent_ Related Work

## Skim Algo/System

## Abstract, Introduction, Related Work
- _Blue-noise Dithered Sampling_
- The choice of original sampling sequence isn't considered in the original text
  - Hence the inclusion of Owen-scrambled Sobol being novel
- Tiled 128x128
- Toroidally shift a sampling pattern
  - Don't use random initial offsets
  - Use a precomputed set of offsets to maximize blue noise sampling
- Basically, figure out how to space samples in adjacent pixels as far apart as possible
  - Just do this across all pixels in the entire image 

## Results

## Algorithm/System
- P_n is the nth sample in the Owen-scrambled Sobol sequence
- s^ij is the scrambling key, there are 128^2 * D
- r^ij is the ranking keys, there are 128^2 * 1
- How to evaluate the n-th sample for a pixel at (i,j)
  1. m = n xor r^ij
  2. p^ij_n = p_m xor s^ij
- Objective is to optimize the keys such that the Monte Carlo errors are as different as possible between neighboring pixels
- Maximimize the difference between neighboring pixels for functions that approximate rendering
  - Heaviside functions f_t do that, apparently
- Compute a vector E^ij of size 65536 for 65536 random Heaviside functions
- every pixel ij gets one error vector
- Maximimize the distance beetween this error vector and the neighbors error vector

- Give every pixel a random s^ij
  - swap with simmualted annealling until max energy difference

- This only optimizes for samples at N
- Optimizing below N requires more work
- 

## Conclusions


# Paragraph
It's a relatively short paper, only two pages, but it is a relatively dense paper. Picking up roughly where Georgiev and Fajardo left _dithered sampling_, Heitz and Belcour extend the sampling patterns to remove some inefficiencies. The effect of _dithered sampling_ focuses on distance between any two sample points. Starting with white noise, _dithered sampling_ toroidally shifts pixels, the shift of any two pixels is swapped, and this process is repeated to minimize an energy function. This enenrgy function previously only included distance between pixels and how they were shifted. This new paper also includes an additional term to the energy function. This additional term approximates the Monte Carlo error of rendering (using thousands of Heaviside functions). This new energy function represents expected Monte Carlo errors and unshaped noise. The process of simulated annealling solves for the lowest energy state, which would represent Monte Carlo errors shaped to blue noise. The previous paper also had inefficiencies beyond n=1 due to the white noise mask, which loses converges when toroidally shifted. The white noise wsa replaced with an Owen-scrambled Sobol sequence, which does not have this limitation.