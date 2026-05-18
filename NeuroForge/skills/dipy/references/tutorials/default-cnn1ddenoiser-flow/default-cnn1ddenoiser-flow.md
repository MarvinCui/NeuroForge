# How To: Default Cnn1Ddenoiser Flow

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test default Cnn1DDenoiser flow

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `importlib`
- `os`
- `sys`
- `warnings`
- `pytest`
- `dipy.testing.decorators`
- `dipy.utils.optpkg`

**Setup Required:**
```python
# Fixtures: pytestconfig, rng
```

## Step-by-Step Guide

### Step 1: Assign normal_img = rng.random(...)

```python
normal_img = rng.random((10, 10, 10, 30))
```

**Verification:**
```python
assert accuracy > 0
```

### Step 2: Assign nos_img = value

```python
nos_img = normal_img + rng.normal(loc=0.0, scale=0.1, size=normal_img.shape)
```

### Step 3: Assign x = rng.random(...)

```python
x = rng.random((10, 10, 10, 30))
```

### Step 4: Assign model = cnnden_mod.Cnn1DDenoiser(...)

```python
model = cnnden_mod.Cnn1DDenoiser(30)
```

### Step 5: Call model.compile()

```python
model.compile(optimizer='adam', loss='mean_squared_error', metrics=['accuracy'])
```

### Step 6: Assign epochs = 1

```python
epochs = 1
```

### Step 7: Assign hist = model.fit(...)

```python
hist = model.fit(nos_img, normal_img, epochs=epochs)
```

### Step 8: Assign _ = model.predict(...)

```python
_ = model.predict(x)
```

### Step 9: Call model.evaluate()

```python
model.evaluate(nos_img, normal_img, verbose=2)
```

### Step 10: Assign accuracy = value

```python
accuracy = hist.history['accuracy'][0]
```

**Verification:**
```python
assert accuracy > 0
```

### Step 11: Call model.summary()

```python
model.summary()
```


## Complete Example

```python
# Setup
# Fixtures: pytestconfig, rng

# Workflow
normal_img = rng.random((10, 10, 10, 30))
nos_img = normal_img + rng.normal(loc=0.0, scale=0.1, size=normal_img.shape)
x = rng.random((10, 10, 10, 30))
model = cnnden_mod.Cnn1DDenoiser(30)
if pytestconfig.getoption('verbose') > 0:
    model.summary()
model.compile(optimizer='adam', loss='mean_squared_error', metrics=['accuracy'])
epochs = 1
hist = model.fit(nos_img, normal_img, epochs=epochs)
_ = model.predict(x)
model.evaluate(nos_img, normal_img, verbose=2)
accuracy = hist.history['accuracy'][0]
assert accuracy > 0
```

## Next Steps


---

*Source: test_cnn_1denoiser.py:62 | Complexity: Advanced | Last updated: 2026-05-18*