# How To: Default Cnn1Ddenoiser Sequential

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test default Cnn1DDenoiser sequential

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
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign normal_img = rng.random(...)

```python
normal_img = rng.random((10, 10, 10, 30))
```

**Verification:**
```python
assert data.shape == x.shape
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

### Step 8: Assign data = model.predict(...)

```python
data = model.predict(x)
```

### Step 9: Call model.evaluate()

```python
model.evaluate(nos_img, normal_img, verbose=2)
```

### Step 10: Assign _ = value

```python
_ = hist.history['accuracy'][0]
```

**Verification:**
```python
assert data.shape == x.shape
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
normal_img = rng.random((10, 10, 10, 30))
nos_img = normal_img + rng.normal(loc=0.0, scale=0.1, size=normal_img.shape)
x = rng.random((10, 10, 10, 30))
model = cnnden_mod.Cnn1DDenoiser(30)
model.compile(optimizer='adam', loss='mean_squared_error', metrics=['accuracy'])
epochs = 1
hist = model.fit(nos_img, normal_img, epochs=epochs)
data = model.predict(x)
model.evaluate(nos_img, normal_img, verbose=2)
_ = hist.history['accuracy'][0]
assert data.shape == x.shape
```

## Next Steps


---

*Source: test_cnn_1denoiser.py:42 | Complexity: Advanced | Last updated: 2026-05-18*