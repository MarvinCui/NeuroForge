# How To: User Potential

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test user potential

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `scipy.sparse`
- `pymc`
- `pymc.pytensorf`
- `pymc.step_methods.hmc`


## Step-by-Step Guide

### Step 1: Assign model = pymc.Model(...)

```python
model = pymc.Model()
```

**Verification:**
```python
assert called
```

### Step 2: Assign called = value

```python
called = []
```

### Step 3: Assign pot = Potential(...)

```python
pot = Potential(floatX([1]))
```

**Verification:**
```python
assert called
```

### Step 4: Call pymc.Normal()

```python
pymc.Normal('a', mu=0, sigma=1)
```

### Step 5: Assign step = pymc.NUTS(...)

```python
step = pymc.NUTS(potential=pot)
```

### Step 6: Call called.append()

```python
called.append(1)
```

### Step 7: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', '.*number of samples.*', UserWarning)
```

### Step 8: Call pymc.sample()

```python
pymc.sample(10, step=step, chains=1)
```


## Complete Example

```python
# Workflow
model = pymc.Model()
with model:
    pymc.Normal('a', mu=0, sigma=1)
called = []

class Potential(quadpotential.QuadPotentialDiag):

    def energy(self, x, velocity=None):
        called.append(1)
        return super().energy(x, velocity)
pot = Potential(floatX([1]))
with model:
    step = pymc.NUTS(potential=pot)
    with warnings.catch_warnings():
        warnings.filterwarnings('ignore', '.*number of samples.*', UserWarning)
        pymc.sample(10, step=step, chains=1)
assert called
```

## Next Steps


---

*Source: test_quadpotential.py:138 | Complexity: Advanced | Last updated: 2026-05-18*