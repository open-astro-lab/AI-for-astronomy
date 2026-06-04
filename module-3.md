---

---

# AI for Astrophysics — Module 3

## Hands-On Python — Neural Networks on Astronomical Data

---

## This is where it becomes real

Modules 1 and 2 gave you the framework: what AI is, and how it is used in astrophysics.

This module is different. Here, you will write code.

By the end, you will have built a neural network that takes real stellar measurements as input and learns to classify stars. Every step is explained. You do not need prior experience with machine learning libraries — the code is written for someone encountering these tools for the first time.

![The Milky Way core above the ESO telescope at Paranal, Chile](https://apod.nasa.gov/apod/image/2407/Paranal_Twardy2048.jpg)
*Data collected at observatories like this feeds into exactly the kind of pipeline you are about to build.*

---

## What you will build

A neural network that takes three measurements of a star:

- **Temperature** (in Kelvin)
- **Luminosity** (relative to the Sun)
- **Radius** (relative to the Sun)

And predicts which **stellar class** the star belongs to: Red Dwarf, Brown Dwarf, White Dwarf, Main Sequence, Supergiant, or Hypergiant.

This is a real classification problem. The dataset contains 240 stars with confirmed labels. Your network will learn the patterns in the data and then classify new stars it has never seen.

---

## What you need

- A Google account (to use Google Colab — free, no installation required)
- The dataset linked on the final page of this course
- A willingness to read error messages without panic

That is genuinely everything.

---

## Step 1: Understanding the data

Before writing a single line of code, look at what you are working with.

The dataset has the following columns:

| Column | What it means |
|---|---|
| `Temperature (K)` | Surface temperature of the star in Kelvin |
| `Luminosity (L/Lo)` | Brightness relative to the Sun |
| `Radius (R/Ro)` | Size relative to the Sun |
| `Absolute magnitude (Mv)` | True brightness on the astronomical magnitude scale |
| `Star type` | A number from 0 to 5 representing the stellar class |
| `Star color` | Dominant color |
| `Spectral Class` | O, B, A, F, G, K, or M |

Your neural network will use the first four numerical columns to predict `Star type`.

This is called **supervised learning** — the model learns from labeled examples.

![A simplified Hertzsprung-Russell diagram showing stellar classification regions](https://chandra.harvard.edu/edu/formal/stellar_ev/story/hr.jpg)
*. Each region corresponds to a star type. Your neural network will learn these boundaries from data — without being told where they are.*

---

## Step 2: Loading the data

Open your Colab notebook (https://colab.research.google.com/) and begin.

The first thing to do is load the data and take a look at it.

```python
import pandas as pd

# Load the dataset
df = pd.read_csv('https://docs.google.com/spreadsheets/d/12G-HwAvH7waLkn0pA4mbuWjkw-C4SdMLeeG_a_rtOoc/edit?gid=139654193#gid=139654193')

# See the first few rows
df.head()
```

Run this cell. You should see the first five rows of the dataset appear as a table.

Now check the shape — how many rows and columns:

```python
print(df.shape)
```

And check that there are no missing values, which would confuse the model:

```python
print(df.isnull().sum())
```

If every column shows 0, you are ready to proceed.

---

## Step 3: Preparing the data

Neural networks work with numbers. Before training, you need to prepare the data in two ways.

**Separate inputs from outputs.**

```python
# Input features
X = df[['Temperature (K)', 'Luminosity(L/Lo)', 'Radius(R/Ro)', 'Absolute magnitude(Mv)']].values

# Output labels (what we want to predict)
y = df['Star type'].values
```

**Scale the inputs.**

The four input features are on very different scales — temperature is in the tens of thousands, while luminosity might be 0.0001 for a dim star. Neural networks train much better when all inputs are on a similar scale.

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)
```

`StandardScaler` transforms each feature so it has a mean of 0 and a standard deviation of 1. The underlying data does not change — only the scale.

**Split into training and test sets.**

You need to hold back some data that the model will never see during training. This is your honest evaluation of how well it has actually learned.

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X_scaled, y, test_size=0.2, random_state=42
)

print(f"Training samples: {len(X_train)}")
print(f"Test samples: {len(X_test)}")
```

80% of the data trains the model. 20% tests it afterward.

---

## Step 4: Building the neural network

Now you build the model itself. You will use **Keras**, a library that makes neural network construction readable.

```python
import tensorflow as tf
from tensorflow import keras

model = keras.Sequential([
    keras.layers.Dense(64, activation='relu', input_shape=(4,)),
    keras.layers.Dense(64, activation='relu'),
    keras.layers.Dense(6, activation='softmax')
])
```

What this creates:

- **Input layer**: accepts 4 features (one per column)
- **Hidden layer 1**: 64 neurons, ReLU activation
- **Hidden layer 2**: 64 neurons, ReLU activation
- **Output layer**: 6 neurons (one per star class), softmax activation

The softmax activation converts the final layer's numbers into probabilities that add up to 1. The class with the highest probability is the model's prediction.

**Compile the model** — tell it how to learn:

```python
model.compile(
    optimizer='adam',
    loss='sparse_categorical_crossentropy',
    metrics=['accuracy']
)

model.summary()
```

`model.summary()` prints the network's architecture. Take a moment to read it — see how the layers connect and how many parameters the model has.

![Diagram of a simple neural network with input, hidden, and output layers](https://apod.nasa.gov/apod/image/9906/deepsky_aat.jpg)
*Data flows from input to output through layers of transformations — the same way light passes through optical elements in a telescope before becoming a useful image.*

---

## Step 5: Training the model

This is the step where the learning actually happens.

```python
history = model.fit(
    X_train, y_train,
    epochs=100,
    batch_size=16,
    validation_split=0.1,
    verbose=1
)
```

- **epochs**: how many times the model passes through the entire training dataset
- **batch_size**: how many samples the model processes before updating its parameters
- **validation_split**: 10% of training data held back to monitor performance during training

Watch the output as it trains. You should see `loss` decreasing and `accuracy` increasing over the epochs.

**Plot the training history:**

```python
import matplotlib.pyplot as plt

plt.figure(figsize=(12, 4))

plt.subplot(1, 2, 1)
plt.plot(history.history['accuracy'], label='Training accuracy')
plt.plot(history.history['val_accuracy'], label='Validation accuracy')
plt.xlabel('Epoch')
plt.ylabel('Accuracy')
plt.title('Model Accuracy Over Time')
plt.legend()

plt.subplot(1, 2, 2)
plt.plot(history.history['loss'], label='Training loss')
plt.plot(history.history['val_loss'], label='Validation loss')
plt.xlabel('Epoch')
plt.ylabel('Loss')
plt.title('Model Loss Over Time')
plt.legend()

plt.tight_layout()
plt.show()
```

A healthy training curve shows both training and validation accuracy rising together and then leveling off. If training accuracy is high but validation accuracy is much lower, the model has overfit — it has memorized the training data rather than learning a generalizable pattern.

---

## Step 6: Evaluating the model

Now test the model on data it has never seen.

```python
test_loss, test_accuracy = model.evaluate(X_test, y_test, verbose=0)
print(f"Test accuracy: {test_accuracy:.2%}")
```

A well-trained model on this dataset should reach somewhere above 90% accuracy. If yours is lower, try increasing the number of epochs and retraining.

**Go further with a confusion matrix:**

A confusion matrix shows not just overall accuracy, but exactly which classes the model confuses with each other.

```python
from sklearn.metrics import confusion_matrix, ConfusionMatrixDisplay
import numpy as np

y_pred = np.argmax(model.predict(X_test), axis=1)

class_names = ['Brown Dwarf', 'Red Dwarf', 'White Dwarf',
               'Main Sequence', 'Supergiant', 'Hypergiant']

cm = confusion_matrix(y_test, y_pred)
disp = ConfusionMatrixDisplay(confusion_matrix=cm, display_labels=class_names)
disp.plot(xticks_rotation=45)
plt.title('Confusion Matrix — Star Classification')
plt.tight_layout()
plt.show()
```

Each row represents the true class. Each column represents the predicted class. Perfect classification would show all values along the diagonal. Off-diagonal values show where the model made mistakes.

Look at the confusion matrix carefully. Are some star types consistently confused with each other? What physical properties might explain that?

---

## Step 7: Classifying a new star

The real payoff — use your trained model to classify a star it has never seen.

```python
import numpy as np

# A new star: temperature, luminosity, radius, absolute magnitude
new_star = np.array([[3068, 0.002, 0.17, 16.12]])

# Scale it the same way the training data was scaled
new_star_scaled = scaler.transform(new_star)

# Get predictions
prediction = model.predict(new_star_scaled)
predicted_class = np.argmax(prediction)

class_names = ['Brown Dwarf', 'Red Dwarf', 'White Dwarf',
               'Main Sequence', 'Supergiant', 'Hypergiant']

print(f"Predicted class: {class_names[predicted_class]}")
print(f"\nConfidence for each class:")
for name, prob in zip(class_names, prediction[0]):
    print(f"  {name}: {prob:.2%}")
```

The model does not just output a single label. It outputs a probability for every class. This is important — a prediction with 97% confidence means something different from one with 52% confidence.

Try changing the input values. Use extreme temperatures or luminosities. Watch how the confidence distribution shifts.

![Color-coded scatter plot of stars by temperature and luminosity](https://apod.nasa.gov/apod/image/0511/crabmosaic_hst_big.jpg)
*The Crab Nebula — remnant of a supernova. The dense, spinning neutron star at its center would appear as a single data point in your dataset. Your model would classify it in milliseconds.*

---

## What you just did

Step back and look at what this notebook actually contains:

1. You loaded real astronomical data
2. You preprocessed it — scaling, splitting, separating inputs from outputs
3. You built a neural network with a specific architecture for this problem
4. You trained it by showing it examples
5. You evaluated it honestly on data it never saw during training
6. You used it to classify new stars and read the confidence scores

This is the core of a machine learning pipeline. Researchers working on galaxy classification, exoplanet detection, and gravitational wave analysis are running versions of exactly this same sequence of steps — just with larger datasets and more complex architectures.

---

## What to try next

Once you have the basic model working, experiment:

- **Change the number of layers** — add a third hidden layer and see if accuracy improves
- **Change the number of neurons** — try 128 neurons per layer instead of 64
- **Add dropout** — a technique that helps prevent overfitting by randomly disabling neurons during training: `keras.layers.Dropout(0.3)`
- **Add more input features** — include `Spectral Class` by encoding it as a number and see whether it helps

Each of these changes will teach you something about how neural networks behave.

---

## Key idea to remember

**A model is only as good as its training data.**

The stars in this dataset are well-measured and correctly labeled. In real research, data is messy, incomplete, and sometimes wrong. Learning to build models is only half the skill. The other half is understanding your data well enough to know when to trust what the model tells you.

---

### End of Module 3

---

This site is open source. [Improve this page](https://github.com/open-astro-lab/ai-for-astrophysics/edit/main/docs/module-3.md)
