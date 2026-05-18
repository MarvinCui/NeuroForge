# How To: Fwhm Kde Batch

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test FWHM via weighted KDE.

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.reconst.force`


## Step-by-Step Guide

### Step 1: 'Test FWHM via weighted KDE.'

```python
'Test FWHM via weighted KDE.'
```

**Verification:**
```python
assert fwhm_narrow.shape == (1,)
```

### Step 2: Assign vals_narrow = np.array(...)

```python
vals_narrow = np.array([[5.0, 5.1, 5.0, 4.9, 5.0]], dtype=np.float32)
```

**Verification:**
```python
assert fwhm_narrow[0] >= 0
```

### Step 3: Assign weights_uniform = np.array(...)

```python
weights_uniform = np.array([[0.2, 0.2, 0.2, 0.2, 0.2]], dtype=np.float32)
```

**Verification:**
```python
assert fwhm_wide[0] > fwhm_narrow[0]
```

### Step 4: Assign fwhm_narrow = _fwhm_kde_batch(...)

```python
fwhm_narrow = _fwhm_kde_batch(vals_narrow, weights_uniform)
```

**Verification:**
```python
assert fwhm_batch.shape == (2,)
```

### Step 5: Assign vals_wide = np.array(...)

```python
vals_wide = np.array([[0.0, 2.5, 5.0, 7.5, 10.0]], dtype=np.float32)
```

**Verification:**
```python
assert fwhm_batch[1] > fwhm_batch[0]
```

### Step 6: Assign fwhm_wide = _fwhm_kde_batch(...)

```python
fwhm_wide = _fwhm_kde_batch(vals_wide, weights_uniform)
```

**Verification:**
```python
assert fwhm_wide[0] > fwhm_narrow[0]
```

### Step 7: Assign vals_batch = np.vstack(...)

```python
vals_batch = np.vstack([vals_narrow, vals_wide])
```

### Step 8: Assign weights_batch = np.vstack(...)

```python
weights_batch = np.vstack([weights_uniform, weights_uniform])
```

### Step 9: Assign fwhm_batch = _fwhm_kde_batch(...)

```python
fwhm_batch = _fwhm_kde_batch(vals_batch, weights_batch)
```

**Verification:**
```python
assert fwhm_batch.shape == (2,)
```


## Complete Example

```python
# Workflow
'Test FWHM via weighted KDE.'
vals_narrow = np.array([[5.0, 5.1, 5.0, 4.9, 5.0]], dtype=np.float32)
weights_uniform = np.array([[0.2, 0.2, 0.2, 0.2, 0.2]], dtype=np.float32)
fwhm_narrow = _fwhm_kde_batch(vals_narrow, weights_uniform)
assert fwhm_narrow.shape == (1,)
assert fwhm_narrow[0] >= 0
vals_wide = np.array([[0.0, 2.5, 5.0, 7.5, 10.0]], dtype=np.float32)
fwhm_wide = _fwhm_kde_batch(vals_wide, weights_uniform)
assert fwhm_wide[0] > fwhm_narrow[0]
vals_batch = np.vstack([vals_narrow, vals_wide])
weights_batch = np.vstack([weights_uniform, weights_uniform])
fwhm_batch = _fwhm_kde_batch(vals_batch, weights_batch)
assert fwhm_batch.shape == (2,)
assert fwhm_batch[1] > fwhm_batch[0]
```

## Next Steps


---

*Source: test_force.py:141 | Complexity: Advanced | Last updated: 2026-05-18*