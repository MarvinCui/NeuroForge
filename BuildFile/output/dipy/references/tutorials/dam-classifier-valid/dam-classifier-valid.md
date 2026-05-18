# How To: Dam Classifier Valid

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test dam classifier valid

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.segment.tissue`
- `dipy.utils.optpkg`


## Step-by-Step Guide

### Step 1: Assign data = value

```python
data = np.random.rand(3, 3, 3, 7) * 100
```

**Verification:**
```python
assert_equal(data.shape[-1], bvals.shape[0], 'The number of bvals must match the last dimension of data')
```

### Step 2: Assign bvals = np.array(...)

```python
bvals = np.array([0, 100, 500, 1000, 1500, 2000, 3000])
```

**Verification:**
```python
assert_equal(wm_mask.shape, (3, 3, 3), 'Shape of wm_mask should be (3, 3, 3)')
```

### Step 3: Call assert_equal()

```python
assert_equal(data.shape[-1], bvals.shape[0], 'The number of bvals must match the last dimension of data')
```

**Verification:**
```python
assert_equal(gm_mask.shape, (3, 3, 3), 'Shape of gm_mask should be (3, 3, 3)')
```

### Step 4: Assign unknown = dam_classifier(...)

```python
wm_mask, gm_mask = dam_classifier(data, bvals, wm_threshold=0.5)
```

**Verification:**
```python
assert_raises(ValueError, dam_classifier, data, bvals, wm_threshold=0.5)
```

### Step 5: Call assert_equal()

```python
assert_equal(wm_mask.shape, (3, 3, 3), 'Shape of wm_mask should be (3, 3, 3)')
```

### Step 6: Call assert_equal()

```python
assert_equal(gm_mask.shape, (3, 3, 3), 'Shape of gm_mask should be (3, 3, 3)')
```

### Step 7: Assign data = np.array(...)

```python
data = np.array([100, 80, 60, 50])
```

### Step 8: Assign bvals = np.array(...)

```python
bvals = np.array([0, 0, 100, 100])
```

### Step 9: Call assert_raises()

```python
assert_raises(ValueError, dam_classifier, data, bvals, wm_threshold=0.5)
```


## Complete Example

```python
# Workflow
data = np.random.rand(3, 3, 3, 7) * 100
bvals = np.array([0, 100, 500, 1000, 1500, 2000, 3000])
assert_equal(data.shape[-1], bvals.shape[0], 'The number of bvals must match the last dimension of data')
wm_mask, gm_mask = dam_classifier(data, bvals, wm_threshold=0.5)
assert_equal(wm_mask.shape, (3, 3, 3), 'Shape of wm_mask should be (3, 3, 3)')
assert_equal(gm_mask.shape, (3, 3, 3), 'Shape of gm_mask should be (3, 3, 3)')
data = np.array([100, 80, 60, 50])
bvals = np.array([0, 0, 100, 100])
assert_raises(ValueError, dam_classifier, data, bvals, wm_threshold=0.5)
```

## Next Steps


---

*Source: test_tissue.py:46 | Complexity: Advanced | Last updated: 2026-05-18*