# How To: Coregister Fiducials

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test coreg.coregister_fiducials().

## Prerequisites

**Required Modules:**
- `os`
- `functools`
- `glob`
- `shutil`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.channels`
- `mne.coreg`
- `mne.datasets`
- `mne.io`
- `mne.source_space`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test coreg.coregister_fiducials().'

```python
'Test coreg.coregister_fiducials().'
```

**Verification:**
```python
assert trans_est.from_str == trans.from_str
```

### Step 2: Assign trans = Transform(...)

```python
trans = Transform('head', 'mri', rotation(0.4, 0.1, 0).dot(translation(0.1, -0.1, 0.1)))
```

**Verification:**
```python
assert trans_est.to_str == trans.to_str
```

### Step 3: Assign coords_orig = np.array(...)

```python
coords_orig = np.array([[-0.08061612, -0.02908875, -0.04131077], [0.00146763, 0.08506715, -0.03483611], [0.08436285, -0.02850276, -0.04127743]])
```

**Verification:**
```python
assert_array_almost_equal(trans_est['trans'], trans['trans'])
```

### Step 4: Assign coords_trans = apply_trans(...)

```python
coords_trans = apply_trans(trans, coords_orig)
```

### Step 5: Assign mri_fiducials = make_dig(...)

```python
mri_fiducials = make_dig(coords_trans, FIFF.FIFFV_COORD_MRI)
```

### Step 6: Assign info = value

```python
info = {'dig': make_dig(coords_orig, FIFF.FIFFV_COORD_HEAD)}
```

### Step 7: Assign trans_est = coregister_fiducials(...)

```python
trans_est = coregister_fiducials(info, mri_fiducials)
```

**Verification:**
```python
assert trans_est.from_str == trans.from_str
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(trans_est['trans'], trans['trans'])
```


## Complete Example

```python
# Workflow
'Test coreg.coregister_fiducials().'
trans = Transform('head', 'mri', rotation(0.4, 0.1, 0).dot(translation(0.1, -0.1, 0.1)))
coords_orig = np.array([[-0.08061612, -0.02908875, -0.04131077], [0.00146763, 0.08506715, -0.03483611], [0.08436285, -0.02850276, -0.04127743]])
coords_trans = apply_trans(trans, coords_orig)

def make_dig(coords, cf):
    return ({'coord_frame': cf, 'ident': 1, 'kind': 1, 'r': coords[0]}, {'coord_frame': cf, 'ident': 2, 'kind': 1, 'r': coords[1]}, {'coord_frame': cf, 'ident': 3, 'kind': 1, 'r': coords[2]})
mri_fiducials = make_dig(coords_trans, FIFF.FIFFV_COORD_MRI)
info = {'dig': make_dig(coords_orig, FIFF.FIFFV_COORD_HEAD)}
trans_est = coregister_fiducials(info, mri_fiducials)
assert trans_est.from_str == trans.from_str
assert trans_est.to_str == trans.to_str
assert_array_almost_equal(trans_est['trans'], trans['trans'])
```

## Next Steps


---

*Source: test_coreg.py:63 | Complexity: Advanced | Last updated: 2026-05-18*