# How To: Simple Model Data

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: simple model data

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `io`
- `operator`
- `warnings`
- `cloudpickle`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `pymc`
- `pymc.variational.opvi`
- `pymc.model.transform.basic`
- `pymc.pytensorf`
- `pymc.variational.inference`
- `pymc.variational.opvi`
- `tests`

**Setup Required:**
```python
# Fixtures: use_minibatch
```

## Step-by-Step Guide

### Step 1: Assign n = 1000

```python
n = 1000
```

### Step 2: Assign sigma0 = 2.0

```python
sigma0 = 2.0
```

### Step 3: Assign mu0 = 4.0

```python
mu0 = 4.0
```

### Step 4: Assign sigma = 3.0

```python
sigma = 3.0
```

### Step 5: Assign mu = value

```python
mu = -5.0
```

### Step 6: Assign data = value

```python
data = sigma * np.random.randn(n) + mu
```

### Step 7: Assign d = value

```python
d = n / sigma ** 2 + 1 / sigma0 ** 2
```

### Step 8: Assign mu_post = value

```python
mu_post = (n * np.mean(data) / sigma ** 2 + mu0 / sigma0 ** 2) / d
```

### Step 9: Assign data = pm.Minibatch(...)

```python
data = pm.Minibatch(data, batch_size=128)
```


## Complete Example

```python
# Setup
# Fixtures: use_minibatch

# Workflow
n = 1000
sigma0 = 2.0
mu0 = 4.0
sigma = 3.0
mu = -5.0
data = sigma * np.random.randn(n) + mu
d = n / sigma ** 2 + 1 / sigma0 ** 2
mu_post = (n * np.mean(data) / sigma ** 2 + mu0 / sigma0 ** 2) / d
if use_minibatch:
    data = pm.Minibatch(data, batch_size=128)
return {'n': n, 'data': data, 'mu_post': mu_post, 'd': d, 'mu0': mu0, 'sigma0': sigma0, 'sigma': sigma}
```

## Next Steps


---

*Source: test_inference.py:56 | Complexity: Advanced | Last updated: 2026-05-18*