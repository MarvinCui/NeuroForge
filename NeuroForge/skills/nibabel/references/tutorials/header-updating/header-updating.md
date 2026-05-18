# How To: Header Updating

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test header updating

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

### Step 1: Assign mgz = load(...)

```python
mgz = load(MGZ_FNAME)
```

**Verification:**
```python
assert_almost_equal(mgz.affine, exp_aff, 6)
```

### Step 2: Assign hdr = value

```python
hdr = mgz.header
```

**Verification:**
```python
assert_almost_equal(hdr.get_affine(), exp_aff, 6)
```

### Step 3: Assign exp_aff = np.loadtxt(...)

```python
exp_aff = np.loadtxt(io.BytesIO(b'\n    1.0000   2.0000   3.0000   -13.0000\n    2.0000   3.0000   1.0000   -11.5000\n    3.0000   1.0000   2.0000   -11.5000\n    0.0000   0.0000   0.0000     1.0000'))
```

**Verification:**
```python
assert np.all(hdr['delta'] == 1)
```

### Step 4: Call assert_almost_equal()

```python
assert_almost_equal(mgz.affine, exp_aff, 6)
```

**Verification:**
```python
assert_almost_equal(hdr['Mdc'].T, exp_aff[:3, :3])
```

### Step 5: Call assert_almost_equal()

```python
assert_almost_equal(hdr.get_affine(), exp_aff, 6)
```

**Verification:**
```python
assert_almost_equal(hdr2.get_affine(), exp_aff, 6)
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(hdr['Mdc'].T, exp_aff[:3, :3])
```

**Verification:**
```python
assert_array_equal(hdr2['delta'], 1)
```

### Step 7: Assign img_fobj = io.BytesIO(...)

```python
img_fobj = io.BytesIO()
```

**Verification:**
```python
assert_almost_equal(hdr2.get_affine(), exp_aff_d, 6)
```

### Step 8: Assign mgz2 = _mgh_rt(...)

```python
mgz2 = _mgh_rt(mgz, img_fobj)
```

**Verification:**
```python
assert_almost_equal(hdr2['delta'], np.sqrt(np.sum(RZS ** 2, axis=0)))
```

### Step 9: Assign hdr2 = value

```python
hdr2 = mgz2.header
```

**Verification:**
```python
assert_almost_equal(hdr2['Mdc'].T, RZS / hdr2['delta'])
```

### Step 10: Call assert_almost_equal()

```python
assert_almost_equal(hdr2.get_affine(), exp_aff, 6)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(hdr2['delta'], 1)
```

### Step 12: Assign exp_aff_d = exp_aff.copy(...)

```python
exp_aff_d = exp_aff.copy()
```

### Step 13: Assign unknown = value

```python
exp_aff_d[0, -1] = -14
```

### Step 14: Assign unknown = exp_aff_d

```python
mgz2._affine[:] = exp_aff_d
```

### Step 15: Call mgz2.update_header()

```python
mgz2.update_header()
```

### Step 16: Call assert_almost_equal()

```python
assert_almost_equal(hdr2.get_affine(), exp_aff_d, 6)
```

### Step 17: Assign RZS = value

```python
RZS = exp_aff_d[:3, :3]
```

### Step 18: Call assert_almost_equal()

```python
assert_almost_equal(hdr2['delta'], np.sqrt(np.sum(RZS ** 2, axis=0)))
```

### Step 19: Call assert_almost_equal()

```python
assert_almost_equal(hdr2['Mdc'].T, RZS / hdr2['delta'])
```


## Complete Example

```python
# Workflow
mgz = load(MGZ_FNAME)
hdr = mgz.header
exp_aff = np.loadtxt(io.BytesIO(b'\n    1.0000   2.0000   3.0000   -13.0000\n    2.0000   3.0000   1.0000   -11.5000\n    3.0000   1.0000   2.0000   -11.5000\n    0.0000   0.0000   0.0000     1.0000'))
assert_almost_equal(mgz.affine, exp_aff, 6)
assert_almost_equal(hdr.get_affine(), exp_aff, 6)
assert np.all(hdr['delta'] == 1)
assert_almost_equal(hdr['Mdc'].T, exp_aff[:3, :3])
img_fobj = io.BytesIO()
mgz2 = _mgh_rt(mgz, img_fobj)
hdr2 = mgz2.header
assert_almost_equal(hdr2.get_affine(), exp_aff, 6)
assert_array_equal(hdr2['delta'], 1)
exp_aff_d = exp_aff.copy()
exp_aff_d[0, -1] = -14
mgz2._affine[:] = exp_aff_d
mgz2.update_header()
assert_almost_equal(hdr2.get_affine(), exp_aff_d, 6)
RZS = exp_aff_d[:3, :3]
assert_almost_equal(hdr2['delta'], np.sqrt(np.sum(RZS ** 2, axis=0)))
assert_almost_equal(hdr2['Mdc'].T, RZS / hdr2['delta'])
```

## Next Steps


---

*Source: test_mghformat.py:217 | Complexity: Advanced | Last updated: 2026-05-18*