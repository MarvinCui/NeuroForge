# How To: Slr One Streamline

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test slr one streamline

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

### Step 1: Assign fname = get_fnames(...)

```python
fname = get_fnames(name='fornix')
```

**Verification:**
```python
assert_raises(ValueError, slr_with_qbx, f1_one, f2, verbose=False, rm_small_clusters=50, greater_than=20, less_than=np.inf, qbx_thr=[2], progressive=True)
```

### Step 2: Assign fornix = value

```python
fornix = load_tractogram(fname, 'same', bbox_valid_check=False).streamlines
```

**Verification:**
```python
assert_raises(ValueError, slr_with_qbx, f2, f1_one, verbose=False, rm_small_clusters=50, greater_than=20, less_than=np.inf, qbx_thr=[2], progressive=True)
```

### Step 3: Assign f = Streamlines(...)

```python
f = Streamlines(fornix)
```

### Step 4: Assign f1_one = Streamlines(...)

```python
f1_one = Streamlines([f[0]])
```

### Step 5: Assign f2 = f.copy(...)

```python
f2 = f.copy()
```

### Step 6: Call assert_raises()

```python
assert_raises(ValueError, slr_with_qbx, f1_one, f2, verbose=False, rm_small_clusters=50, greater_than=20, less_than=np.inf, qbx_thr=[2], progressive=True)
```

### Step 7: Call assert_raises()

```python
assert_raises(ValueError, slr_with_qbx, f2, f1_one, verbose=False, rm_small_clusters=50, greater_than=20, less_than=np.inf, qbx_thr=[2], progressive=True)
```


## Complete Example

```python
# Workflow
fname = get_fnames(name='fornix')
fornix = load_tractogram(fname, 'same', bbox_valid_check=False).streamlines
f = Streamlines(fornix)
f1_one = Streamlines([f[0]])
f2 = f.copy()
f2._data += np.array([50, 0, 0])
assert_raises(ValueError, slr_with_qbx, f1_one, f2, verbose=False, rm_small_clusters=50, greater_than=20, less_than=np.inf, qbx_thr=[2], progressive=True)
assert_raises(ValueError, slr_with_qbx, f2, f1_one, verbose=False, rm_small_clusters=50, greater_than=20, less_than=np.inf, qbx_thr=[2], progressive=True)
```

## Next Steps


---

*Source: test_whole_brain_slr.py:94 | Complexity: Intermediate | Last updated: 2026-05-18*