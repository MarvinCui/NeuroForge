# How To: Default Mnist Sequential

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test default mnist sequential

## Prerequisites

**Required Modules:**
- `importlib`
- `os`
- `sys`
- `warnings`
- `numpy.testing`
- `pytest`
- `dipy.utils.optpkg`


## Step-by-Step Guide

### Step 1: Assign mnist = value

```python
mnist = tf.keras.datasets.mnist
```

**Verification:**
```python
assert_(accuracy > 0.9)
```

### Step 2: Assign epochs = 5

```python
epochs = 5
```

### Step 3: Assign unknown = mnist.load_data(...)

```python
(x_train, y_train), (x_test, y_test) = mnist.load_data()
```

### Step 4: Assign unknown = value

```python
x_train, x_test = (x_train / 255.0, x_test / 255.0)
```

### Step 5: Assign model = tf.keras.models.Sequential(...)

```python
model = tf.keras.models.Sequential([tf.keras.layers.Input(shape=(28, 28)), tf.keras.layers.Flatten(), tf.keras.layers.Dense(128, activation='relu'), tf.keras.layers.Dropout(0.2), tf.keras.layers.Dense(10, activation='softmax')])
```

### Step 6: Call model.compile()

```python
model.compile(optimizer='adam', loss='sparse_categorical_crossentropy', metrics=['accuracy'])
```

### Step 7: Assign hist = model.fit(...)

```python
hist = model.fit(x_train, y_train, epochs=epochs)
```

### Step 8: Call model.evaluate()

```python
model.evaluate(x_test, y_test, verbose=2)
```

### Step 9: Assign accuracy = value

```python
accuracy = hist.history['accuracy'][-1]
```

### Step 10: Call assert_()

```python
assert_(accuracy > 0.9)
```


## Complete Example

```python
# Workflow
mnist = tf.keras.datasets.mnist
epochs = 5
(x_train, y_train), (x_test, y_test) = mnist.load_data()
x_train, x_test = (x_train / 255.0, x_test / 255.0)
model = tf.keras.models.Sequential([tf.keras.layers.Input(shape=(28, 28)), tf.keras.layers.Flatten(), tf.keras.layers.Dense(128, activation='relu'), tf.keras.layers.Dropout(0.2), tf.keras.layers.Dense(10, activation='softmax')])
model.compile(optimizer='adam', loss='sparse_categorical_crossentropy', metrics=['accuracy'])
hist = model.fit(x_train, y_train, epochs=epochs)
model.evaluate(x_test, y_test, verbose=2)
accuracy = hist.history['accuracy'][-1]
assert_(accuracy > 0.9)
```

## Next Steps


---

*Source: test_tf.py:38 | Complexity: Advanced | Last updated: 2026-05-18*