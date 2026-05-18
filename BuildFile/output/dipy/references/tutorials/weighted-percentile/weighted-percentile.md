# How To: Weighted Percentile

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test weighted percentile computation.

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.reconst.force`


## Step-by-Step Guide

### Step 1: 'Test weighted percentile computation.'

```python
'Test weighted percentile computation.'
```

**Verification:**
```python
assert q50.shape == (1,)
```

### Step 2: Assign vals = np.array(...)

```python
vals = np.array([[1, 2, 3, 4, 5]], dtype=np.float32)
```

**Verification:**
```python
assert 2.0 <= q50[0] <= 4.0
```

### Step 3: Assign weights = np.array(...)

```python
weights = np.array([[0.2, 0.2, 0.2, 0.2, 0.2]], dtype=np.float32)
```

**Verification:**
```python
assert_almost_equal(q50_conc[0], 1.0)
```

### Step 4: Assign q50 = _weighted_percentile(...)

```python
q50 = _weighted_percentile(vals, weights, 0.5)
```

**Verification:**
```python
assert q75.shape == (2,)
```

### Step 5: Assign weights_conc = np.array(...)

```python
weights_conc = np.array([[1.0, 0.0, 0.0, 0.0, 0.0]], dtype=np.float32)
```

**Verification:**
```python
assert q75[1] > q75[0]
```

### Step 6: Assign q50_conc = _weighted_percentile(...)

```python
q50_conc = _weighted_percentile(vals, weights_conc, 0.5)
```

### Step 7: Call assert_almost_equal()

```python
assert_almost_equal(q50_conc[0], 1.0)
```

### Step 8: Assign vals_batch = np.array(...)

```python
vals_batch = np.array([[1, 2, 3, 4, 5], [10, 20, 30, 40, 50]], dtype=np.float32)
```

### Step 9: Assign weights_batch = np.array(...)

```python
weights_batch = np.array([[0.2, 0.2, 0.2, 0.2, 0.2], [0.2, 0.2, 0.2, 0.2, 0.2]], dtype=np.float32)
```

### Step 10: Assign q75 = _weighted_percentile(...)

```python
q75 = _weighted_percentile(vals_batch, weights_batch, 0.75)
```

**Verification:**
```python
assert q75.shape == (2,)
```


## Complete Example

```python
# Workflow
'Test weighted percentile computation.'
vals = np.array([[1, 2, 3, 4, 5]], dtype=np.float32)
weights = np.array([[0.2, 0.2, 0.2, 0.2, 0.2]], dtype=np.float32)
q50 = _weighted_percentile(vals, weights, 0.5)
assert q50.shape == (1,)
assert 2.0 <= q50[0] <= 4.0
weights_conc = np.array([[1.0, 0.0, 0.0, 0.0, 0.0]], dtype=np.float32)
q50_conc = _weighted_percentile(vals, weights_conc, 0.5)
assert_almost_equal(q50_conc[0], 1.0)
vals_batch = np.array([[1, 2, 3, 4, 5], [10, 20, 30, 40, 50]], dtype=np.float32)
weights_batch = np.array([[0.2, 0.2, 0.2, 0.2, 0.2], [0.2, 0.2, 0.2, 0.2, 0.2]], dtype=np.float32)
q75 = _weighted_percentile(vals_batch, weights_batch, 0.75)
assert q75.shape == (2,)
assert q75[1] > q75[0]
```

## Next Steps


---

*Source: test_force.py:114 | Complexity: Advanced | Last updated: 2026-05-18*