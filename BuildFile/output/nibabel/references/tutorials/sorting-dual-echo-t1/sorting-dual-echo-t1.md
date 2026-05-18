# How To: Sorting Dual Echo T1

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sorting dual echo T1

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
t1_par = pjoin(DATA_PATH, 'T1_dual_echo.PAR')
```

**Verification:**
```python
assert np.all(sorted_echos[:n_half] == 1)
```

### Step 2: Call np.random.shuffle()

```python
np.random.shuffle(t1_hdr.image_defs)
```

**Verification:**
```python
assert np.all(sorted_echos[n_half:] == 2)
```

### Step 3: Assign sorted_indices = t1_hdr.get_sorted_slice_indices(...)

```python
sorted_indices = t1_hdr.get_sorted_slice_indices()
```

**Verification:**
```python
assert list(vol_labels.keys()) == ['echo number']
```

### Step 4: Assign sorted_echos = value

```python
sorted_echos = t1_hdr.image_defs['echo number'][sorted_indices]
```

**Verification:**
```python
assert_array_equal(vol_labels['echo number'], [1, 2])
```

### Step 5: Assign n_half = value

```python
n_half = len(t1_hdr.image_defs) // 2
```

**Verification:**
```python
assert np.all(sorted_echos[:n_half] == 1)
```

### Step 6: Assign vol_labels = t1_hdr.get_volume_labels(...)

```python
vol_labels = t1_hdr.get_volume_labels()
```

**Verification:**
```python
assert list(vol_labels.keys()) == ['echo number']
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(vol_labels['echo number'], [1, 2])
```

### Step 8: Assign t1_hdr = PARRECHeader.from_fileobj(...)

```python
t1_hdr = PARRECHeader.from_fileobj(fobj, strict_sort=True)
```


## Complete Example

```python
# Workflow
t1_par = pjoin(DATA_PATH, 'T1_dual_echo.PAR')
with open(t1_par) as fobj:
    t1_hdr = PARRECHeader.from_fileobj(fobj, strict_sort=True)
np.random.shuffle(t1_hdr.image_defs)
sorted_indices = t1_hdr.get_sorted_slice_indices()
sorted_echos = t1_hdr.image_defs['echo number'][sorted_indices]
n_half = len(t1_hdr.image_defs) // 2
assert np.all(sorted_echos[:n_half] == 1)
assert np.all(sorted_echos[n_half:] == 2)
vol_labels = t1_hdr.get_volume_labels()
assert list(vol_labels.keys()) == ['echo number']
assert_array_equal(vol_labels['echo number'], [1, 2])
```

## Next Steps


---

*Source: test_parrec.py:319 | Complexity: Advanced | Last updated: 2026-05-18*