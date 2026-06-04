---

---

# AI for Astrophysics — Module 2

## AI Techniques in Astrophysics

---

## From concept to practice

In Module 1, you learned what machine learning is at its core: systems that find patterns in data by learning from examples.

Now the question is: what does that actually look like when applied to real astrophysics?

This module walks through the specific problems where AI has changed how research is done — and the techniques used to solve them.

*

---

## Problem 1: Galaxy Classification

### What the problem is

Galaxies come in distinct shapes — spiral, elliptical, lenticular, irregular, and many subtypes within each category. A galaxy's morphology (shape) tells astronomers about its age, how it formed, and what stage of evolution it is in.

For decades, classification was done by eye. In the early 2000s, the Galaxy Zoo project asked volunteers worldwide to classify images from the Sloan Digital Sky Survey. Over 100,000 people participated. It worked — but it could not scale to future surveys producing hundreds of millions of galaxy images.

### How AI solves it

This is a **supervised learning** problem. Researchers trained convolutional neural networks (CNNs) — a type of neural network designed specifically for image data — on the Galaxy Zoo classifications.

After training on hundreds of thousands of labeled images, the network learned to classify galaxies as accurately as a human expert, in a fraction of the time.

The same CNN approach is now used for: identifying gravitational lenses, detecting merging galaxies, and flagging unusual morphologies that might indicate new phenomena.



---

## Problem 2: Star Classification and Spectral Analysis

### What the problem is

Every star produces a unique spectrum — a pattern of bright and dark lines at specific wavelengths that acts like a fingerprint for its chemical composition, temperature, and physical state.

Modern spectroscopic surveys like SDSS (Sloan Digital Sky Survey) and LAMOST collect spectra from millions of stars. Extracting useful information from millions of spectra by hand is not realistic.

### How AI solves it

Machine learning models — both traditional methods like **random forests** and modern neural networks — have been trained to:

- Automatically assign spectral types to stars (O, B, A, F, G, K, M)
- Measure stellar parameters like temperature, gravity, and metallicity directly from raw spectra
- Identify rare stellar objects — stars with unusual chemical signatures that a standard pipeline might miss

The Gaia space mission, which has catalogued over a billion stars, uses automated classification pipelines that rely heavily on these methods.



---

## Problem 3: Exoplanet Detection

### What the problem is

One of the most successful methods of finding planets around other stars is the **transit method**: when a planet passes in front of its host star, it blocks a small fraction of the star's light, causing a tiny, periodic dip in brightness.

NASA's Kepler and TESS missions have collected brightness measurements (light curves) from hundreds of thousands of stars, each recorded over months or years. Each light curve needs to be examined for the characteristic dip pattern of a planetary transit.

### How AI solves it

Researchers at Google trained a neural network on confirmed and false-positive transit signals from Kepler data. The result, published in 2018, found two previously missed exoplanets in data that had already been analyzed by conventional methods.

This is now standard practice. Neural networks scan light curves automatically, ranking candidates by likelihood. Human experts then focus their time on the most promising detections rather than scanning every data point manually.

The technique has since been applied to gravitational microlensing — another planet-detection method — with similar success.


---

## Problem 4: Gravitational Wave Detection

### What the problem is

Gravitational waves are ripples in spacetime produced by extreme events — colliding black holes, merging neutron stars. The LIGO and Virgo detectors measure these waves as tiny distortions in the length of laser beams traveling kilometers through metal arms.

The signals are incredibly faint and buried in noise. Traditional detection relies on matched filtering: comparing the incoming signal against a bank of theoretical templates. This works, but is computationally expensive, and may miss signals that don't match existing templates well.

### How AI solves it

Deep learning models — specifically a type called a **convolutional neural network** applied to time-series data — have been trained to detect gravitational wave signals directly from raw detector output.

These models can identify signals in milliseconds rather than the hours required by traditional methods. They are also sensitive to signal types that template banks might not cover, including signals from sources we haven't fully modeled yet.

Several detections confirmed by LIGO have now been cross-checked against neural network classifiers as part of the standard pipeline.


*Two black holes spiraling toward merger — an event that sends gravitational waves across the universe. Detecting these faint signals in noisy data is exactly where AI has proven its value.*

---

## Problem 5: Cosmological Simulations and Emulation

### What the problem is

Understanding how the universe evolved from the Big Bang to today requires running large-scale computer simulations of gravity, gas physics, and dark matter. These simulations are extraordinarily computationally expensive — a single high-resolution simulation can take weeks on hundreds of processors.

Cosmologists need to run many simulations with different physical parameters to understand how each parameter affects the result. Running thousands of full simulations is not feasible.

### How AI solves it

Researchers train neural networks on a smaller number of full simulations, then use those networks as **emulators** — fast approximations that can predict the result of a simulation with a given set of parameters in seconds rather than weeks.

This approach, sometimes called **neural network emulation**, has reduced the computational cost of parameter estimation in cosmology by orders of magnitude. It is now used to constrain the properties of dark energy, dark matter, and the large-scale structure of the universe.

![Large-scale structure of the universe from a cosmological simulation](https://apod.nasa.gov/apod/image/9811/lss_2df_960.jpg)
*The large-scale structure of the universe — the cosmic web of filaments and voids. Simulating its formation accurately requires methods that AI has made dramatically more tractable.*

---

## Techniques used across these problems

Looking across all five problems, a few methods come up repeatedly:

**Convolutional Neural Networks (CNNs)**
Used wherever the input is an image or can be structured like one — galaxy morphology, spectra plotted as 2D maps, gravitational wave strain data.

**Random Forests**
An older but still widely used technique. Effective for tabular data (tables of measurements) where interpretability matters. Often used as a baseline before trying neural networks.

**Recurrent Neural Networks (RNNs) and Transformers**
Used for sequential data — light curves, time-series signals, long spectral sequences. These architectures are designed to handle data where order matters.

**Transfer Learning**
Training a network on one large dataset and then fine-tuning it on a smaller domain-specific dataset. This is especially useful in astrophysics, where labeled data is often scarce.

---

## A pattern across all of these

In every problem above, the same structure appears:

1. A large volume of data that would take humans impractical amounts of time to process
2. A pattern in that data that, once identified, is consistent enough to be learned
3. A machine learning model trained to find that pattern automatically

The astrophysics does not disappear. Understanding the physics is still what tells researchers which features to look at, what patterns to expect, and when a model's output should be trusted or questioned.

AI is a tool. The science is still science.

---

## What comes next

In Module 3, you will stop reading about these methods and start using one.

You will build a neural network in Python that classifies stars using real data — working through the same kind of pipeline that researchers use in practice.

---

### End of Module 2

---

This site is open source. [Improve this page](https://github.com/open-astro-lab/ai-for-astrophysics/edit/main/docs/module-2.md)
