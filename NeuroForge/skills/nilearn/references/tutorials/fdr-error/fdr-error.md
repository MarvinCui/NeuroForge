# How To: Fdr Error

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test fdr error

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `scipy.stats`
- `nilearn.datasets`
- `nilearn.exceptions`
- `nilearn.glm`
- `nilearn.glm.thresholding`
- `nilearn.image`
- `nilearn.surface.surface`
- `nilearn.surface.surface`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign n = 100

```python
n = 100
```

### Step 2: Assign x = np.linspace(...)

```python
x = np.linspace(0.5 / n, 1.0 - 0.5 / n, n)
```

### Step 3: Assign unknown = 0.0005

```python
x[:10] = 0.0005
```

### Step 4: Assign x = norm.isf(...)

```python
x = norm.isf(x)
```

### Step 5: Call rng.shuffle()

```python
rng.shuffle(x)
```

### Step 6: Assign match = 'alpha should be between 0 and 1'

```python
match = 'alpha should be between 0 and 1'
```

### Step 7: Call fdr_threshold()

```python
fdr_threshold(x, -0.1)
```

### Step 8: Call fdr_threshold()

```python
fdr_threshold(x, 1.5)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
n = 100
x = np.linspace(0.5 / n, 1.0 - 0.5 / n, n)
x[:10] = 0.0005
x = norm.isf(x)
rng.shuffle(x)
match = 'alpha should be between 0 and 1'
with pytest.raises(ValueError, match=match):
    fdr_threshold(x, -0.1)
with pytest.raises(ValueError, match=match):
    fdr_threshold(x, 1.5)
```

## Next Steps


---

*Source: test_thresholding.py:45 | Complexity: Advanced | Last updated: 2026-05-18*