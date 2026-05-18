# How To: Sorting Multiple Echos And Contrasts

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sorting multiple echos and contrasts

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

### Step 1: Assign t1_par = pjoin(...)

```python
t1_par = pjoin(DATA_PATH, 'T1_3echo_mag_real_imag_phase.PAR')
```

**Verification:**
```python
assert_array_equal(sorted_slices[istart:iend], np.arange(1, nslices + 1))
```

### Step 2: Call np.random.shuffle()

```python
np.random.shuffle(t1_hdr.image_defs)
```

**Verification:**
```python
assert np.all(sorted_echos[istart:iend] == current_echo)
```

### Step 3: Assign sorted_indices = t1_hdr.get_sorted_slice_indices(...)

```python
sorted_indices = t1_hdr.get_sorted_slice_indices()
```

**Verification:**
```python
assert np.all(sorted_types[:ntotal // 4] == 0)
```

### Step 4: Assign sorted_slices = value

```python
sorted_slices = t1_hdr.image_defs['slice number'][sorted_indices]
```

**Verification:**
```python
assert np.all(sorted_types[ntotal // 4:ntotal // 2] == 1)
```

### Step 5: Assign sorted_echos = value

```python
sorted_echos = t1_hdr.image_defs['echo number'][sorted_indices]
```

**Verification:**
```python
assert np.all(sorted_types[ntotal // 2:3 * ntotal // 4] == 2)
```

### Step 6: Assign sorted_types = value

```python
sorted_types = t1_hdr.image_defs['image_type_mr'][sorted_indices]
```

**Verification:**
```python
assert np.all(sorted_types[3 * ntotal // 4:ntotal] == 3)
```

### Step 7: Assign ntotal = len(...)

```python
ntotal = len(t1_hdr.image_defs)
```

**Verification:**
```python
assert list(vol_labels.keys()) == ['echo number', 'image_type_mr']
```

### Step 8: Assign nslices = sorted_slices.max(...)

```python
nslices = sorted_slices.max()
```

**Verification:**
```python
assert_array_equal(vol_labels['echo number'], [1, 2, 3] * 4)
```

### Step 9: Assign nechos = sorted_echos.max(...)

```python
nechos = sorted_echos.max()
```

**Verification:**
```python
assert_array_equal(vol_labels['image_type_mr'], [0, 0, 0, 1, 1, 1, 2, 2, 2, 3, 3, 3])
```

### Step 10: Assign vol_labels = t1_hdr.get_volume_labels(...)

```python
vol_labels = t1_hdr.get_volume_labels()
```

**Verification:**
```python
assert list(vol_labels.keys()) == ['echo number', 'image_type_mr']
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(vol_labels['echo number'], [1, 2, 3] * 4)
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(vol_labels['image_type_mr'], [0, 0, 0, 1, 1, 1, 2, 2, 2, 3, 3, 3])
```

### Step 13: Assign t1_hdr = PARRECHeader.from_fileobj(...)

```python
t1_hdr = PARRECHeader.from_fileobj(fobj, strict_sort=True)
```

### Step 14: Assign istart = value

```python
istart = slice_offset * nslices
```

### Step 15: Assign iend = value

```python
iend = (slice_offset + 1) * nslices
```

### Step 16: Call assert_array_equal()

```python
assert_array_equal(sorted_slices[istart:iend], np.arange(1, nslices + 1))
```

### Step 17: Assign current_echo = value

```python
current_echo = slice_offset % nechos + 1
```

**Verification:**
```python
assert np.all(sorted_echos[istart:iend] == current_echo)
```


## Complete Example

```python
# Workflow
t1_par = pjoin(DATA_PATH, 'T1_3echo_mag_real_imag_phase.PAR')
with open(t1_par) as fobj:
    t1_hdr = PARRECHeader.from_fileobj(fobj, strict_sort=True)
np.random.shuffle(t1_hdr.image_defs)
sorted_indices = t1_hdr.get_sorted_slice_indices()
sorted_slices = t1_hdr.image_defs['slice number'][sorted_indices]
sorted_echos = t1_hdr.image_defs['echo number'][sorted_indices]
sorted_types = t1_hdr.image_defs['image_type_mr'][sorted_indices]
ntotal = len(t1_hdr.image_defs)
nslices = sorted_slices.max()
nechos = sorted_echos.max()
for slice_offset in range(ntotal // nslices):
    istart = slice_offset * nslices
    iend = (slice_offset + 1) * nslices
    assert_array_equal(sorted_slices[istart:iend], np.arange(1, nslices + 1))
    current_echo = slice_offset % nechos + 1
    assert np.all(sorted_echos[istart:iend] == current_echo)
assert np.all(sorted_types[:ntotal // 4] == 0)
assert np.all(sorted_types[ntotal // 4:ntotal // 2] == 1)
assert np.all(sorted_types[ntotal // 2:3 * ntotal // 4] == 2)
assert np.all(sorted_types[3 * ntotal // 4:ntotal] == 3)
vol_labels = t1_hdr.get_volume_labels()
assert list(vol_labels.keys()) == ['echo number', 'image_type_mr']
assert_array_equal(vol_labels['echo number'], [1, 2, 3] * 4)
assert_array_equal(vol_labels['image_type_mr'], [0, 0, 0, 1, 1, 1, 2, 2, 2, 3, 3, 3])
```

## Next Steps


---

*Source: test_parrec.py:343 | Complexity: Advanced | Last updated: 2026-05-18*