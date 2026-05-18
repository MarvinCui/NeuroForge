# How To: Sorting Multiecho Asl

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sorting multiecho ASL

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

### Step 1: Assign asl_par = pjoin(...)

```python
asl_par = pjoin(DATA_PATH, 'ASL_3D_Multiecho.PAR')
```

**Verification:**
```python
assert nslices == 8
```

### Step 2: Call np.random.shuffle()

```python
np.random.shuffle(asl_hdr.image_defs)
```

**Verification:**
```python
assert nechos == 3
```

### Step 3: Assign sorted_indices = asl_hdr.get_sorted_slice_indices(...)

```python
sorted_indices = asl_hdr.get_sorted_slice_indices()
```

**Verification:**
```python
assert nlabels == 2
```

### Step 4: Assign sorted_slices = value

```python
sorted_slices = asl_hdr.image_defs['slice number'][sorted_indices]
```

**Verification:**
```python
assert ndynamics == 2
```

### Step 5: Assign sorted_echos = value

```python
sorted_echos = asl_hdr.image_defs['echo number'][sorted_indices]
```

**Verification:**
```python
assert_array_equal(np.all(sorted_dynamics[:ntotal // ndynamics] == 1), True)
```

### Step 6: Assign sorted_dynamics = value

```python
sorted_dynamics = asl_hdr.image_defs['dynamic scan number'][sorted_indices]
```

**Verification:**
```python
assert_array_equal(np.all(sorted_dynamics[ntotal // ndynamics:ntotal] == 2), True)
```

### Step 7: Assign sorted_labels = value

```python
sorted_labels = asl_hdr.image_defs['label type'][sorted_indices]
```

**Verification:**
```python
assert_array_equal(np.all(sorted_labels[:nslices * nechos] == 1), True)
```

### Step 8: Assign ntotal = len(...)

```python
ntotal = len(asl_hdr.image_defs)
```

**Verification:**
```python
assert_array_equal(np.all(sorted_labels[nslices * nechos:2 * nslices * nechos] == 2), True)
```

### Step 9: Assign nslices = sorted_slices.max(...)

```python
nslices = sorted_slices.max()
```

**Verification:**
```python
assert_array_equal(np.all(sorted_echos[:nslices] == 1), True)
```

### Step 10: Assign nechos = sorted_echos.max(...)

```python
nechos = sorted_echos.max()
```

**Verification:**
```python
assert_array_equal(np.all(sorted_echos[nslices:2 * nslices] == 2), True)
```

### Step 11: Assign nlabels = sorted_labels.max(...)

```python
nlabels = sorted_labels.max()
```

**Verification:**
```python
assert_array_equal(np.all(sorted_echos[2 * nslices:3 * nslices] == 3), True)
```

### Step 12: Assign ndynamics = sorted_dynamics.max(...)

```python
ndynamics = sorted_dynamics.max()
```

**Verification:**
```python
assert_array_equal(sorted_slices[:nslices], np.arange(1, nslices + 1))
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(np.all(sorted_dynamics[:ntotal // ndynamics] == 1), True)
```

**Verification:**
```python
assert list(vol_labels.keys()) == ['echo number', 'label type', 'dynamic scan number']
```

### Step 14: Call assert_array_equal()

```python
assert_array_equal(np.all(sorted_dynamics[ntotal // ndynamics:ntotal] == 2), True)
```

**Verification:**
```python
assert_array_equal(vol_labels['dynamic scan number'], [1] * 6 + [2] * 6)
```

### Step 15: Call assert_array_equal()

```python
assert_array_equal(np.all(sorted_labels[:nslices * nechos] == 1), True)
```

**Verification:**
```python
assert_array_equal(vol_labels['label type'], [1] * 3 + [2] * 3 + [1] * 3 + [2] * 3)
```

### Step 16: Call assert_array_equal()

```python
assert_array_equal(np.all(sorted_labels[nslices * nechos:2 * nslices * nechos] == 2), True)
```

**Verification:**
```python
assert_array_equal(vol_labels['echo number'], [1, 2, 3] * 4)
```

### Step 17: Call assert_array_equal()

```python
assert_array_equal(np.all(sorted_echos[:nslices] == 1), True)
```

### Step 18: Call assert_array_equal()

```python
assert_array_equal(np.all(sorted_echos[nslices:2 * nslices] == 2), True)
```

### Step 19: Call assert_array_equal()

```python
assert_array_equal(np.all(sorted_echos[2 * nslices:3 * nslices] == 3), True)
```

### Step 20: Call assert_array_equal()

```python
assert_array_equal(sorted_slices[:nslices], np.arange(1, nslices + 1))
```

### Step 21: Assign vol_labels = asl_hdr.get_volume_labels(...)

```python
vol_labels = asl_hdr.get_volume_labels()
```

**Verification:**
```python
assert list(vol_labels.keys()) == ['echo number', 'label type', 'dynamic scan number']
```

### Step 22: Call assert_array_equal()

```python
assert_array_equal(vol_labels['dynamic scan number'], [1] * 6 + [2] * 6)
```

### Step 23: Call assert_array_equal()

```python
assert_array_equal(vol_labels['label type'], [1] * 3 + [2] * 3 + [1] * 3 + [2] * 3)
```

### Step 24: Call assert_array_equal()

```python
assert_array_equal(vol_labels['echo number'], [1, 2, 3] * 4)
```

### Step 25: Assign asl_hdr = PARRECHeader.from_fileobj(...)

```python
asl_hdr = PARRECHeader.from_fileobj(fobj, strict_sort=True)
```


## Complete Example

```python
# Workflow
asl_par = pjoin(DATA_PATH, 'ASL_3D_Multiecho.PAR')
with open(asl_par) as fobj:
    asl_hdr = PARRECHeader.from_fileobj(fobj, strict_sort=True)
np.random.shuffle(asl_hdr.image_defs)
sorted_indices = asl_hdr.get_sorted_slice_indices()
sorted_slices = asl_hdr.image_defs['slice number'][sorted_indices]
sorted_echos = asl_hdr.image_defs['echo number'][sorted_indices]
sorted_dynamics = asl_hdr.image_defs['dynamic scan number'][sorted_indices]
sorted_labels = asl_hdr.image_defs['label type'][sorted_indices]
ntotal = len(asl_hdr.image_defs)
nslices = sorted_slices.max()
nechos = sorted_echos.max()
nlabels = sorted_labels.max()
ndynamics = sorted_dynamics.max()
assert nslices == 8
assert nechos == 3
assert nlabels == 2
assert ndynamics == 2
assert_array_equal(np.all(sorted_dynamics[:ntotal // ndynamics] == 1), True)
assert_array_equal(np.all(sorted_dynamics[ntotal // ndynamics:ntotal] == 2), True)
assert_array_equal(np.all(sorted_labels[:nslices * nechos] == 1), True)
assert_array_equal(np.all(sorted_labels[nslices * nechos:2 * nslices * nechos] == 2), True)
assert_array_equal(np.all(sorted_echos[:nslices] == 1), True)
assert_array_equal(np.all(sorted_echos[nslices:2 * nslices] == 2), True)
assert_array_equal(np.all(sorted_echos[2 * nslices:3 * nslices] == 3), True)
assert_array_equal(sorted_slices[:nslices], np.arange(1, nslices + 1))
vol_labels = asl_hdr.get_volume_labels()
assert list(vol_labels.keys()) == ['echo number', 'label type', 'dynamic scan number']
assert_array_equal(vol_labels['dynamic scan number'], [1] * 6 + [2] * 6)
assert_array_equal(vol_labels['label type'], [1] * 3 + [2] * 3 + [1] * 3 + [2] * 3)
assert_array_equal(vol_labels['echo number'], [1, 2, 3] * 4)
```

## Next Steps


---

*Source: test_parrec.py:389 | Complexity: Advanced | Last updated: 2026-05-18*