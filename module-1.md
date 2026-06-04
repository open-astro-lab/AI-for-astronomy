---
layout: default
title: AI for Astrophysics — Module 1
description: A beginner-friendly introduction to what AI and machine learning actually are.
---

# AI for Astrophysics — Module 1

## What is AI? Foundations of Machine Learning

---

## Who is this for?

This module is for **anyone** — no background in AI, statistics, or advanced mathematics required.

If you have ever heard terms like "machine learning," "neural network," or "deep learning" and wondered what they actually mean beneath the buzzwords, this is where you find out.

You do **not** need to be a programmer yet.  
You only need to be **willing to think**.

![A wide view of the Milky Way over an observatory](https://apod.nasa.gov/apod/image/2501/MilkyWayTelescope_Cobianchi_2048.jpg)
*Modern observatories collect more data every night than a human team could analyze in a lifetime. AI is how researchers keep up.*

---

## Why does astrophysics need AI?

For most of astronomy's history, data came slowly.

A few observations per night. A handful of stars per study. Teams of researchers working for years to classify a few thousand objects.

That is no longer the case.

Today, a single survey telescope can photograph **billions of galaxies** in a few years. The Square Kilometre Array, currently being built, will generate more data per day than the entire internet.

No human team can process that.

This is why AI entered astrophysics — not as a trend, but out of necessity. The universe is producing more information than we have hands to sort through.

![The Square Kilometre Array telescope site in Western Australia](https://apod.nasa.gov/apod/image/2210/SKA_site_2022.jpg)
*Construction of the Square Kilometre Array — when complete, it will require AI just to handle the data flow.*

---

## What is Artificial Intelligence, really?

Here is what AI is **not**:

- It is not a robot with human-like understanding
- It is not magic
- It is not a system that thinks the way you think

Here is what AI **is**:

**AI is a set of mathematical methods that allow computers to find patterns in data and make decisions based on those patterns.**

That is it. The intimidating vocabulary around AI often hides a surprisingly concrete idea: teach a computer to recognize patterns by showing it many examples.

---

## The core idea: learning from examples

Think about how you learned to recognize a dog.

Nobody gave you a precise mathematical definition of "dog." You were shown dogs — many of them, in many contexts — and your brain gradually built a pattern that lets you identify one instantly now.

Machine learning works the same way. Instead of programming rules by hand, you feed a system thousands of examples and let it figure out the pattern itself.

![Hubble Space Telescope image of various galaxy morphologies](https://apod.nasa.gov/apod/image/9802/galaxies_hst.jpg)
*Galaxies come in many shapes — spiral, elliptical, irregular. Classifying them manually once took years. AI systems trained on labeled images can now do it in seconds.*

This is why "machine learning" is called what it is. The machine is **learning** — adjusting itself based on the examples it sees — rather than following a fixed set of rules.

---

## Three key terms you need to know

### 1. Model

A **model** is the mathematical structure that learns from data. Think of it as a function: you put data in, you get a prediction out.

Before training, a model knows nothing. After training on many examples, it can generalize — make reasonable predictions on data it has never seen before.

### 2. Training

**Training** is the process of showing a model many examples so it can learn the pattern. During training, the model adjusts its internal numbers (called parameters) to reduce the gap between its predictions and the correct answers.

### 3. Features

**Features** are the measurements you feed into a model. In astrophysics, features might be:

- A star's brightness at different wavelengths
- The shape of a galaxy in an image
- The period of a repeating signal

The model learns which features matter most for the task at hand.

---

## Types of machine learning — the big three

### Supervised Learning

You give the model labeled examples. Each input comes with a correct answer.

Example in astrophysics: you show the model 10,000 galaxy images, each labeled "spiral" or "elliptical." The model learns to classify new galaxy images on its own.

### Unsupervised Learning

No labels. You give the model raw data and ask it to find structure.

Example: you give the model spectra from 100,000 stars and ask it to find natural groupings — without telling it what those groups should be.

### Reinforcement Learning

The model learns by trial and error, receiving rewards for good decisions and penalties for bad ones.

This is less common in astrophysics, but has applications in telescope scheduling and autonomous observation systems.

![Schematic of supervised vs unsupervised learning concepts](https://apod.nasa.gov/apod/image/0002/deepfield_hst_big.jpg)
*The Hubble Deep Field — thousands of galaxies in a single image. Sorting through data like this by hand is not realistic. Supervised learning changed that.*

---

## What is a neural network?

A **neural network** is one type of machine learning model — and currently the most powerful and widely used.

It is loosely inspired by the structure of the brain, though the analogy should not be taken literally.

A neural network is made up of **layers of simple mathematical operations**, chained together. Each layer takes the output of the previous one and transforms it slightly. After many layers, the network can recognize surprisingly complex patterns.

The word "deep" in "deep learning" simply means the network has many layers. More layers allow the network to learn more abstract patterns.

You do not need to understand the mathematics yet. What matters is the idea:

**Many simple steps chained together can produce surprisingly intelligent behavior.**

---

## What machine learning cannot do

It is just as important to understand the limits:

- A model can only learn patterns that exist in its training data
- If the training data is biased or incomplete, the model's predictions will be too
- A model that performs perfectly on training data may fail badly on new data (this is called **overfitting**)
- Models do not "understand" anything — they find correlations, which is not the same as understanding causation

These limitations matter in astrophysics. A model trained on one type of galaxy survey may perform poorly on data from a different telescope. Knowing when to trust a model — and when not to — is a skill researchers spend years developing.

---

## How this connects to the rest of the course

In Module 2, you will see exactly how these concepts are applied to specific astrophysics problems.

In Module 3, you will build and run a neural network yourself using real astronomical data.

This module gave you the vocabulary and the mental framework. The next two modules make it concrete.

---

## Key idea to remember

**AI is not magic. It is pattern recognition, learned from data.**

Understanding that one sentence puts you ahead of most people who use these tools without thinking carefully about what they are actually doing.

---

### End of Module 1

---

This site is open source. [Improve this page](https://github.com/open-astro-lab/ai-for-astrophysics/edit/main/docs/module-1.md)
