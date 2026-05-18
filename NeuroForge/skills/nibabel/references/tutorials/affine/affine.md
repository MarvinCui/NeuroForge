# How To: Affine

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test affine

## Prerequisites

**Required Modules:**
- `glob`
- `os.path`
- `os.path`
- `warnings`
- `numpy`
- `pytest`
- `numpy`
- `numpy.testing`
- `fileholders`
- `nifti1`
- `openers`
- `parrec`
- `testing`
- `volumeutils`
- `test_arrayproxy`


## Step-by-Step Guide

### Step 1: Assign hdr = PARRECHeader(...)

```python
hdr = PARRECHeader(HDR_INFO, HDR_DEFS)
```

**Verification:**
```python
assert_array_equal(default, scanner)
```

### Step 2: Assign default = hdr.get_affine(...)

```python
default = hdr.get_affine()
```

**Verification:**
```python
assert_array_equal(scanner[:3, :3], fov[:3, :3])
```

### Step 3: Assign scanner = hdr.get_affine(...)

```python
scanner = hdr.get_affine(origin='scanner')
```

**Verification:**
```python
assert not np.all(scanner[:3, 3] == fov[:3, 3])
```

### Step 4: Assign fov = hdr.get_affine(...)

```python
fov = hdr.get_affine(origin='fov')
```

**Verification:**
```python
assert_almost_equal(default, AN_OLD_AFFINE)
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(default, scanner)
```

**Verification:**
```python
assert_almost_equal(default[:3, :3], PHILIPS_AFFINE[:3, :3], 2)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(scanner[:3, :3], fov[:3, :3])
```

**Verification:**
```python
assert not np.all(scanner[:3, 3] == fov[:3, 3])
```

### Step 7: Call assert_almost_equal()

```python
assert_almost_equal(default, AN_OLD_AFFINE)
```

### Step 8: Call assert_almost_equal()

```python
assert_almost_equal(default[:3, :3], PHILIPS_AFFINE[:3, :3], 2)
```


## Complete Example

```python
# Workflow
hdr = PARRECHeader(HDR_INFO, HDR_DEFS)
default = hdr.get_affine()
scanner = hdr.get_affine(origin='scanner')
fov = hdr.get_affine(origin='fov')
assert_array_equal(default, scanner)
assert_array_equal(scanner[:3, :3], fov[:3, :3])
assert not np.all(scanner[:3, 3] == fov[:3, 3])
assert_almost_equal(default, AN_OLD_AFFINE)
assert_almost_equal(default[:3, :3], PHILIPS_AFFINE[:3, :3], 2)
```

## Next Steps


---

*Source: test_parrec.py:269 | Complexity: Advanced | Last updated: 2026-05-18*