# How To: Standardize Error

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test raise error for wrong strategy.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `typing`
- `numpy`
- `pytest`
- `scipy.signal`
- `numpy`
- `numpy.testing`
- `pandas`
- `nilearn.conftest`
- `nilearn.exceptions`
- `nilearn.signal`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: 'Test raise error for wrong strategy.'

```python
'Test raise error for wrong strategy.'
```

### Step 2: Assign n_features = 10

```python
n_features = 10
```

### Step 3: Assign n_samples = 17

```python
n_samples = 17
```

### Step 4: Assign a = rng.random(...)

```python
a = rng.random((n_samples, n_features))
```

### Step 5: Call standardize_signal()

```python
standardize_signal(a, standardize='foo')
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'Test raise error for wrong strategy.'
n_features = 10
n_samples = 17
a = rng.random((n_samples, n_features))
a += np.linspace(0, 2.0, n_features)
with pytest.raises(ValueError, match="'standardize' must be one of"):
    standardize_signal(a, standardize='foo')
```

## Next Steps


---

*Source: test_signal.py:330 | Complexity: Intermediate | Last updated: 2026-05-18*