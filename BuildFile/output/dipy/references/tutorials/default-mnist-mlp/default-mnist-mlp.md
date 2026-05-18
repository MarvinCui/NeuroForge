# How To: Default Mnist Mlp

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test default mnist mlp

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
assert_(mlp.accuracy > 0.8)
```

### Step 2: Assign epochs = 5

```python
epochs = 5
```

**Verification:**
```python
assert_(mlp.loss < 0.4)
```

### Step 3: Assign unknown = mnist.load_data(...)

```python
(x_train, y_train), (x_test, y_test) = mnist.load_data()
```

**Verification:**
```python
assert_equal(mlp.accuracy, accuracy)
```

### Step 4: Assign unknown = value

```python
x_train, x_test = (x_train / 255.0, x_test / 255.0)
```

**Verification:**
```python
assert_equal(x_test_prob.shape, (10000, 10))
```

### Step 5: Assign mlp = model_mod.MultipleLayerPercepton(...)

```python
mlp = model_mod.MultipleLayerPercepton(input_shape=(28, 28), num_hidden=[128, 128])
```

### Step 6: Assign hist = mlp.fit(...)

```python
hist = mlp.fit(x_train, y_train, epochs=epochs)
```

### Step 7: Call mlp.evaluate()

```python
mlp.evaluate(x_test, y_test, verbose=2)
```

### Step 8: Assign x_test_prob = mlp.predict(...)

```python
x_test_prob = mlp.predict(x_test)
```

### Step 9: Assign accuracy = value

```python
accuracy = hist.history['accuracy'][-1]
```

### Step 10: Call assert_()

```python
assert_(mlp.accuracy > 0.8)
```

### Step 11: Call assert_()

```python
assert_(mlp.loss < 0.4)
```

### Step 12: Call assert_equal()

```python
assert_equal(mlp.accuracy, accuracy)
```

### Step 13: Call assert_equal()

```python
assert_equal(x_test_prob.shape, (10000, 10))
```


## Complete Example

```python
# Workflow
mnist = tf.keras.datasets.mnist
epochs = 5
(x_train, y_train), (x_test, y_test) = mnist.load_data()
x_train, x_test = (x_train / 255.0, x_test / 255.0)
mlp = model_mod.MultipleLayerPercepton(input_shape=(28, 28), num_hidden=[128, 128])
hist = mlp.fit(x_train, y_train, epochs=epochs)
mlp.evaluate(x_test, y_test, verbose=2)
x_test_prob = mlp.predict(x_test)
accuracy = hist.history['accuracy'][-1]
assert_(mlp.accuracy > 0.8)
assert_(mlp.loss < 0.4)
assert_equal(mlp.accuracy, accuracy)
assert_equal(x_test_prob.shape, (10000, 10))
```

## Next Steps


---

*Source: test_tf.py:87 | Complexity: Advanced | Last updated: 2026-05-18*