# How To: Slr Empty After Length Filtering

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that slr_with_qbx raises ValueError when all streamlines are
filtered out by length constraints.

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.align.streamlinear`
- `dipy.data`
- `dipy.io.streamline`
- `dipy.tracking.distances`
- `dipy.tracking.streamline`


## Step-by-Step Guide

### Step 1: 'Test that slr_with_qbx raises ValueError when all streamlines are\n    filtered out by length constraints.\n    '

```python
'Test that slr_with_qbx raises ValueError when all streamlines are\n    filtered out by length constraints.\n    '
```

**Verification:**
```python
assert_raises(ValueError, slr_with_qbx, f1, f2, verbose=False, rm_small_clusters=1, greater_than=1000, less_than=np.inf, qbx_thr=[2], progressive=True)
```

### Step 2: Assign fname = get_fnames(...)

```python
fname = get_fnames(name='fornix')
```

**Verification:**
```python
assert_raises(ValueError, slr_with_qbx, f1, f2, verbose=False, rm_small_clusters=1, greater_than=0, less_than=1, qbx_thr=[2], progressive=True)
```

### Step 3: Assign fornix = value

```python
fornix = load_tractogram(fname, 'same', bbox_valid_check=False).streamlines
```

### Step 4: Assign f = Streamlines(...)

```python
f = Streamlines(fornix)
```

### Step 5: Assign f1 = f.copy(...)

```python
f1 = f.copy()
```

### Step 6: Assign f2 = f.copy(...)

```python
f2 = f.copy()
```

### Step 7: Call assert_raises()

```python
assert_raises(ValueError, slr_with_qbx, f1, f2, verbose=False, rm_small_clusters=1, greater_than=1000, less_than=np.inf, qbx_thr=[2], progressive=True)
```

### Step 8: Call assert_raises()

```python
assert_raises(ValueError, slr_with_qbx, f1, f2, verbose=False, rm_small_clusters=1, greater_than=0, less_than=1, qbx_thr=[2], progressive=True)
```


## Complete Example

```python
# Workflow
'Test that slr_with_qbx raises ValueError when all streamlines are\n    filtered out by length constraints.\n    '
fname = get_fnames(name='fornix')
fornix = load_tractogram(fname, 'same', bbox_valid_check=False).streamlines
f = Streamlines(fornix)
f1 = f.copy()
f2 = f.copy()
assert_raises(ValueError, slr_with_qbx, f1, f2, verbose=False, rm_small_clusters=1, greater_than=1000, less_than=np.inf, qbx_thr=[2], progressive=True)
assert_raises(ValueError, slr_with_qbx, f1, f2, verbose=False, rm_small_clusters=1, greater_than=0, less_than=1, qbx_thr=[2], progressive=True)
```

## Next Steps


---

*Source: test_whole_brain_slr.py:131 | Complexity: Advanced | Last updated: 2026-05-18*