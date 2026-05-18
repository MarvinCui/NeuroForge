# How To: Cosine Order

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test cosine order

## Prerequisites

**Required Modules:**
- `io`
- `os`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `fileholders`
- `openers`
- `spatialimages`
- `testing`
- `tests`
- `tests`
- `tmpdirs`
- `volumeutils`
- `wrapstruct`
- `mghformat`


## Step-by-Step Guide

### Step 1: Assign data = np.arange.reshape(...)

```python
data = np.arange(60, dtype=np.int32).reshape((3, 4, 5))
```

**Verification:**
```python
assert_almost_equal(img.affine, aff, 6)
```

### Step 2: Assign aff = np.diag(...)

```python
aff = np.diag([2.0, 3, 4, 1])
```

**Verification:**
```python
assert_almost_equal(hdr2['Mdc'].T, RZS / zooms)
```

### Step 3: Assign unknown = value

```python
aff[0] = [2, 1, 0, 10]
```

**Verification:**
```python
assert_almost_equal(hdr2['delta'], zooms)
```

### Step 4: Assign img = MGHImage(...)

```python
img = MGHImage(data, aff)
```

### Step 5: Call assert_almost_equal()

```python
assert_almost_equal(img.affine, aff, 6)
```

### Step 6: Assign img_fobj = io.BytesIO(...)

```python
img_fobj = io.BytesIO()
```

### Step 7: Assign img2 = _mgh_rt(...)

```python
img2 = _mgh_rt(img, img_fobj)
```

### Step 8: Assign hdr2 = value

```python
hdr2 = img2.header
```

### Step 9: Assign RZS = value

```python
RZS = aff[:3, :3]
```

### Step 10: Assign zooms = np.sqrt(...)

```python
zooms = np.sqrt(np.sum(RZS ** 2, axis=0))
```

### Step 11: Call assert_almost_equal()

```python
assert_almost_equal(hdr2['Mdc'].T, RZS / zooms)
```

### Step 12: Call assert_almost_equal()

```python
assert_almost_equal(hdr2['delta'], zooms)
```


## Complete Example

```python
# Workflow
data = np.arange(60, dtype=np.int32).reshape((3, 4, 5))
aff = np.diag([2.0, 3, 4, 1])
aff[0] = [2, 1, 0, 10]
img = MGHImage(data, aff)
assert_almost_equal(img.affine, aff, 6)
img_fobj = io.BytesIO()
img2 = _mgh_rt(img, img_fobj)
hdr2 = img2.header
RZS = aff[:3, :3]
zooms = np.sqrt(np.sum(RZS ** 2, axis=0))
assert_almost_equal(hdr2['Mdc'].T, RZS / zooms)
assert_almost_equal(hdr2['delta'], zooms)
```

## Next Steps


---

*Source: test_mghformat.py:256 | Complexity: Advanced | Last updated: 2026-05-18*