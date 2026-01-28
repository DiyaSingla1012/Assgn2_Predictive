
## Objective
The objective of this assignment is to learn an **unknown probability density function (PDF)** of a transformed random variable using **data only**, without assuming any analytical form of the distribution. A **Generative Adversarial Network (GAN)** is used to implicitly learn the distribution.

---

## Dataset Description
- Dataset used: **India Air Quality Data**
- Feature considered: **NO₂ concentration**
- The dataset contains real-valued pollution measurements collected from different monitoring stations.
- Missing values are removed before further processing.

## Transformation of Data
Each value of NO₂ concentration \( x \) is transformed using the function:

\[
z = x + a_r \sin(b_r x)
\]

where:
- Roll number \( r = 102303694 \)
- \( a_r = 0.5 \times (r \bmod 7) = 1.5 \)
- \( b_r = 0.3 \times ((r \bmod 5) + 1) = 1.5 \)

After transformation, the variable \( z \) is **standardized** to have zero mean and unit variance.

## GAN Architecture

### Generator
- Input: Noise sampled from \( \mathcal{N}(0,1) \)
- Architecture:
  - Dense (32) + LeakyReLU
  - Dense (32) + LeakyReLU
  - Dense (1)
- Output: Generated fake samples \( z_f \)

### Discriminator
- Input: Real or generated \( z \)
- Architecture:
  - Dense (16) + LeakyReLU
  - Dense (16) + LeakyReLU
  - Dense (1) with Sigmoid activation
- Output: Probability of sample being real

## Training Details
- Optimizer: Adam
- Learning rate: 0.0002
- Batch size: 64
- Epochs: 3000
- Loss function: Binary Cross Entropy

The discriminator is trained to distinguish between real and fake samples, while the generator is trained to fool the discriminator.

## PDF Estimation
After training:
1. A large number of samples are generated from the generator.
2. The probability density function is estimated using:
   - **Histogram-based density estimation**
   - **Kernel Density Estimation (KDE)**

## Results and Observations
- The GAN successfully learns the underlying distribution of the transformed variable.
- The generated samples closely match the real data distribution.
- KDE plots show smooth density curves with good mode coverage.
- Initial training instability was observed but stabilized after sufficient epochs.
- The learned PDF captures the major characteristics of the real data distribution.


## Conclusion
This assignment demonstrates that a GAN can effectively learn an unknown probability density function directly from data samples, without assuming any parametric form. The generated samples provide a good approximation of the true distribution of the transformed variable.

---
