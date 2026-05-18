# How To: Setting Affine To Rasmm

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test setting affine to rasmm

## Prerequisites

**Required Modules:**
- `copy`
- `operator`
- `unittest`
- `warnings`
- `collections`
- `numpy`
- `pytest`
- `numpy.testing`
- `testing`
- `tractogram`


## Step-by-Step Guide

### Step 1: Assign tractogram = unknown.copy(...)

```python
tractogram = DATA['tractogram'].copy()
```

**Verification:**
```python
assert tractogram.affine_to_rasmm is None
```

### Step 2: Assign affine = np.diag(...)

```python
affine = np.diag(range(4))
```

**Verification:**
```python
assert tractogram.affine_to_rasmm is not affine
```

### Step 3: Assign tractogram.affine_to_rasmm = None

```python
tractogram.affine_to_rasmm = None
```

**Verification:**
```python
assert_array_equal(tractogram.affine_to_rasmm, affine)
```

### Step 4: Assign tractogram.affine_to_rasmm = affine

```python
tractogram.affine_to_rasmm = affine
```

**Verification:**
```python
assert tractogram.affine_to_rasmm is not affine
```

### Step 5: Assign tractogram.affine_to_rasmm = affine.tolist(...)

```python
tractogram.affine_to_rasmm = affine.tolist()
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(tractogram.affine_to_rasmm, affine)
```

### Step 7: Assign tractogram.affine_to_rasmm = value

```python
tractogram.affine_to_rasmm = affine[::2]
```


## Complete Example

```python
# Workflow
tractogram = DATA['tractogram'].copy()
affine = np.diag(range(4))
tractogram.affine_to_rasmm = None
assert tractogram.affine_to_rasmm is None
tractogram.affine_to_rasmm = affine
assert tractogram.affine_to_rasmm is not affine
tractogram.affine_to_rasmm = affine.tolist()
assert_array_equal(tractogram.affine_to_rasmm, affine)
with pytest.raises(ValueError):
    tractogram.affine_to_rasmm = affine[::2]
```

## Next Steps


---

*Source: test_tractogram.py:549 | Complexity: Intermediate | Last updated: 2026-05-18*