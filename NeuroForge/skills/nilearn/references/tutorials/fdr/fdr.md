# How To: Fdr

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test fdr

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

**Verification:**
```python
assert_almost_equal(fdr_threshold(x, 0.1), norm.isf(0.0005))
```

### Step 2: Assign x = np.linspace(...)

```python
x = np.linspace(0.5 / n, 1.0 - 0.5 / n, n)
```

**Verification:**
```python
assert fdr_threshold(x, 0.001) == np.inf
```

### Step 3: Assign unknown = 0.0005

```python
x[:10] = 0.0005
```

**Verification:**
```python
assert np.isfinite(fdr_threshold(norm.isf(pvals), 0.1))
```

### Step 4: Assign x = norm.isf(...)

```python
x = norm.isf(x)
```

### Step 5: Call rng.shuffle()

```python
rng.shuffle(x)
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(fdr_threshold(x, 0.1), norm.isf(0.0005))
```

**Verification:**
```python
assert fdr_threshold(x, 0.001) == np.inf
```

### Step 7: Assign n = 10

```python
n = 10
```

### Step 8: Assign pvals = np.linspace(...)

```python
pvals = np.linspace(1 / n, 1, n)
```

### Step 9: Assign unknown = 0.007

```python
pvals[0] = 0.007
```

**Verification:**
```python
assert np.isfinite(fdr_threshold(norm.isf(pvals), 0.1))
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
assert_almost_equal(fdr_threshold(x, 0.1), norm.isf(0.0005))
assert fdr_threshold(x, 0.001) == np.inf
n = 10
pvals = np.linspace(1 / n, 1, n)
pvals[0] = 0.007
assert np.isfinite(fdr_threshold(norm.isf(pvals), 0.1))
```

## Next Steps


---

*Source: test_thresholding.py:27 | Complexity: Advanced | Last updated: 2026-05-18*