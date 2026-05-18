# How To: Gibbs 4D

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test gibbs 4d

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.denoise.gibbs`


## Step-by-Step Guide

### Step 1: Assign image4d = np.zeros(...)

```python
image4d = np.zeros((6 * Nre, 6 * Nre, 2, 2))
```

**Verification:**
```python
assert_array_almost_equal(image4d_cor[:, :, 0, 0], image_cor)
```

### Step 2: Assign unknown = image_gibbs

```python
image4d[:, :, 0, 0] = image_gibbs
```

**Verification:**
```python
assert_array_almost_equal(image4d_cor[:, :, 1, 0], image_cor)
```

### Step 3: Assign unknown = image_gibbs

```python
image4d[:, :, 1, 0] = image_gibbs
```

**Verification:**
```python
assert_array_almost_equal(image4d_cor[:, :, 0, 1], image_cor)
```

### Step 4: Assign unknown = image_gibbs

```python
image4d[:, :, 0, 1] = image_gibbs
```

**Verification:**
```python
assert_array_almost_equal(image4d_cor[:, :, 1, 1], image_cor)
```

### Step 5: Assign unknown = image_gibbs

```python
image4d[:, :, 1, 1] = image_gibbs
```

### Step 6: Assign image4d_cor = gibbs_removal(...)

```python
image4d_cor = gibbs_removal(image4d)
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(image4d_cor[:, :, 0, 0], image_cor)
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(image4d_cor[:, :, 1, 0], image_cor)
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(image4d_cor[:, :, 0, 1], image_cor)
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(image4d_cor[:, :, 1, 1], image_cor)
```


## Complete Example

```python
# Workflow
image4d = np.zeros((6 * Nre, 6 * Nre, 2, 2))
image4d[:, :, 0, 0] = image_gibbs
image4d[:, :, 1, 0] = image_gibbs
image4d[:, :, 0, 1] = image_gibbs
image4d[:, :, 1, 1] = image_gibbs
image4d_cor = gibbs_removal(image4d)
assert_array_almost_equal(image4d_cor[:, :, 0, 0], image_cor)
assert_array_almost_equal(image4d_cor[:, :, 1, 0], image_cor)
assert_array_almost_equal(image4d_cor[:, :, 0, 1], image_cor)
assert_array_almost_equal(image4d_cor[:, :, 1, 1], image_cor)
```

## Next Steps


---

*Source: test_gibbs.py:118 | Complexity: Advanced | Last updated: 2026-05-18*