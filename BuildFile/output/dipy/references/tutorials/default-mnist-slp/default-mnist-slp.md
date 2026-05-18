# How To: Default Mnist Slp

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test default mnist slp

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
assert_(slp.accuracy > 0.9)
```

### Step 2: Assign epochs = 5

```python
epochs = 5
```

**Verification:**
```python
assert_(slp.loss < 0.4)
```

### Step 3: Assign unknown = mnist.load_data(...)

```python
(x_train, y_train), (x_test, y_test) = mnist.load_data()
```

**Verification:**
```python
assert_equal(slp.accuracy, accuracy)
```

### Step 4: Assign unknown = value

```python
x_train, x_test = (x_train / 255.0, x_test / 255.0)
```

**Verification:**
```python
assert_equal(x_test_prob.shape, (10000, 10))
```

### Step 5: Assign slp = model_mod.SingleLayerPerceptron(...)

```python
slp = model_mod.SingleLayerPerceptron(input_shape=(28, 28))
```

### Step 6: Assign hist = slp.fit(...)

```python
hist = slp.fit(x_train, y_train, epochs=epochs)
```

### Step 7: Call slp.evaluate()

```python
slp.evaluate(x_test, y_test, verbose=2)
```

### Step 8: Assign x_test_prob = slp.predict(...)

```python
x_test_prob = slp.predict(x_test)
```

### Step 9: Assign accuracy = value

```python
accuracy = hist.history['accuracy'][-1]
```

### Step 10: Call assert_()

```python
assert_(slp.accuracy > 0.9)
```

### Step 11: Call assert_()

```python
assert_(slp.loss < 0.4)
```

### Step 12: Call assert_equal()

```python
assert_equal(slp.accuracy, accuracy)
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
slp = model_mod.SingleLayerPerceptron(input_shape=(28, 28))
hist = slp.fit(x_train, y_train, epochs=epochs)
slp.evaluate(x_test, y_test, verbose=2)
x_test_prob = slp.predict(x_test)
accuracy = hist.history['accuracy'][-1]
assert_(slp.accuracy > 0.9)
assert_(slp.loss < 0.4)
assert_equal(slp.accuracy, accuracy)
assert_equal(x_test_prob.shape, (10000, 10))
```

## Next Steps


---

*Source: test_tf.py:67 | Complexity: Advanced | Last updated: 2026-05-18*