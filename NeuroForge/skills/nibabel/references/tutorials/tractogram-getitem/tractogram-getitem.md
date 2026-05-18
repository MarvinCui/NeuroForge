# How To: Tractogram Getitem

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test tractogram getitem

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

### Step 1: Assign tractogram_view = value

```python
tractogram_view = DATA['simple_tractogram'][::2]
```

**Verification:**
```python
assert_tractogram_item_equal(DATA['tractogram'][i], t)
```

### Step 2: Call check_tractogram()

```python
check_tractogram(tractogram_view, DATA['streamlines'][::2])
```

**Verification:**
```python
assert_array_equal(tractogram_view.affine_to_rasmm, tractogram.affine_to_rasmm)
```

### Step 3: Assign r_tractogram = value

```python
r_tractogram = DATA['tractogram'][::-1]
```

### Step 4: Call check_tractogram()

```python
check_tractogram(r_tractogram, DATA['streamlines'][::-1], DATA['tractogram'].data_per_streamline[::-1], DATA['tractogram'].data_per_point[::-1])
```

### Step 5: Assign tractogram = unknown.copy(...)

```python
tractogram = DATA['tractogram'].copy()
```

### Step 6: Assign tractogram.affine_to_rasmm = unknown.rand(...)

```python
tractogram.affine_to_rasmm = DATA['rng'].rand(4, 4)
```

### Step 7: Assign tractogram_view = value

```python
tractogram_view = tractogram[::2]
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(tractogram_view.affine_to_rasmm, tractogram.affine_to_rasmm)
```

### Step 9: Call assert_tractogram_item_equal()

```python
assert_tractogram_item_equal(DATA['tractogram'][i], t)
```


## Complete Example

```python
# Workflow
for i, t in enumerate(DATA['tractogram']):
    assert_tractogram_item_equal(DATA['tractogram'][i], t)
tractogram_view = DATA['simple_tractogram'][::2]
check_tractogram(tractogram_view, DATA['streamlines'][::2])
r_tractogram = DATA['tractogram'][::-1]
check_tractogram(r_tractogram, DATA['streamlines'][::-1], DATA['tractogram'].data_per_streamline[::-1], DATA['tractogram'].data_per_point[::-1])
tractogram = DATA['tractogram'].copy()
tractogram.affine_to_rasmm = DATA['rng'].rand(4, 4)
tractogram_view = tractogram[::2]
assert_array_equal(tractogram_view.affine_to_rasmm, tractogram.affine_to_rasmm)
```

## Next Steps


---

*Source: test_tractogram.py:569 | Complexity: Advanced | Last updated: 2026-05-18*