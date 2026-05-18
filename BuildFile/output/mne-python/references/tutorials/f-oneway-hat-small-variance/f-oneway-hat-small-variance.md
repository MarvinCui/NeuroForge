# How To: F Oneway Hat Small Variance

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that f_oneway hat stabilizes F-values for near-zero variance.

## Prerequisites

**Required Modules:**
- `functools`
- `itertools`
- `numpy`
- `pytest`
- `scipy.stats`
- `numpy.testing`
- `mne`
- `mne.stats.parametric`


## Step-by-Step Guide

### Step 1: 'Test that f_oneway hat stabilizes F-values for near-zero variance.'

```python
'Test that f_oneway hat stabilizes F-values for near-zero variance.'
```

**Verification:**
```python
assert np.median(f_unreg) > 1000000.0
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

**Verification:**
```python
assert np.median(f_abs) < np.median(f_unreg)
```

### Step 3: Assign X1 = rng.normal(...)

```python
X1 = rng.normal(0, 1e-06, (10, 100))
```

**Verification:**
```python
assert np.median(f_rel) < np.median(f_unreg)
```

### Step 4: Assign X2 = rng.normal(...)

```python
X2 = rng.normal(1, 1e-06, (10, 100))
```

**Verification:**
```python
assert np.all(np.isfinite(f_abs))
```

### Step 5: Assign f_unreg = f_oneway(...)

```python
f_unreg = f_oneway(X1, X2, sigma=0.0)
```

**Verification:**
```python
assert np.all(np.isfinite(f_rel))
```

### Step 6: Assign f_abs = f_oneway(...)

```python
f_abs = f_oneway(X1, X2, sigma=0.001, method='absolute')
```

### Step 7: Assign f_rel = f_oneway(...)

```python
f_rel = f_oneway(X1, X2, sigma=0.001, method='relative')
```

**Verification:**
```python
assert np.median(f_unreg) > 1000000.0
```


## Complete Example

```python
# Workflow
'Test that f_oneway hat stabilizes F-values for near-zero variance.'
rng = np.random.RandomState(0)
X1 = rng.normal(0, 1e-06, (10, 100))
X2 = rng.normal(1, 1e-06, (10, 100))
f_unreg = f_oneway(X1, X2, sigma=0.0)
f_abs = f_oneway(X1, X2, sigma=0.001, method='absolute')
f_rel = f_oneway(X1, X2, sigma=0.001, method='relative')
assert np.median(f_unreg) > 1000000.0
assert np.median(f_abs) < np.median(f_unreg)
assert np.median(f_rel) < np.median(f_unreg)
assert np.all(np.isfinite(f_abs))
assert np.all(np.isfinite(f_rel))
```

## Next Steps


---

*Source: test_parametric.py:200 | Complexity: Intermediate | Last updated: 2026-05-18*