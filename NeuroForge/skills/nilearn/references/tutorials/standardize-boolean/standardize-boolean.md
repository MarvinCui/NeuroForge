# How To: Standardize Boolean

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test standardize_signal with standardize as boolean.

TODO (nilearn >= 0.15) remove this test

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

### Step 1: 'Test standardize_signal with standardize as boolean.\n\n    TODO (nilearn >= 0.15) remove this test\n    '

```python
'Test standardize_signal with standardize as boolean.\n\n    TODO (nilearn >= 0.15) remove this test\n    '
```

**Verification:**
```python
assert_array_equal(standardize_signal(a), standardize_signal(a, standardize=True))
```

### Step 2: Assign n_features = 10

```python
n_features = 10
```

**Verification:**
```python
assert_array_equal(standardize_signal(a, standardize=None), standardize_signal(a, standardize=False))
```

### Step 3: Assign n_samples = 17

```python
n_samples = 17
```

### Step 4: Assign a = rng.random(...)

```python
a = rng.random((n_samples, n_features))
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(standardize_signal(a), standardize_signal(a, standardize=True))
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(standardize_signal(a, standardize=None), standardize_signal(a, standardize=False))
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'Test standardize_signal with standardize as boolean.\n\n    TODO (nilearn >= 0.15) remove this test\n    '
n_features = 10
n_samples = 17
a = rng.random((n_samples, n_features))
a += np.linspace(0, 2.0, n_features)
assert_array_equal(standardize_signal(a), standardize_signal(a, standardize=True))
assert_array_equal(standardize_signal(a, standardize=None), standardize_signal(a, standardize=False))
```

## Next Steps


---

*Source: test_signal.py:391 | Complexity: Intermediate | Last updated: 2026-05-18*