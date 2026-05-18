# How To: Fiducials Io

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test fiducials i/o.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `json`
- `pickle`
- `string`
- `datetime`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne._fiff`
- `mne._fiff._digitization`
- `mne._fiff.constants`
- `mne._fiff.meas_info`
- `mne._fiff.proj`
- `mne._fiff.tag`
- `mne._fiff.write`
- `mne.channels`
- `mne.datasets`
- `mne.event`
- `mne.io`
- `mne.minimum_norm`
- `mne.transforms`
- `mne.utils`
- `mne.utils._bunch`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test fiducials i/o.'

```python
'Test fiducials i/o.'
```

**Verification:**
```python
assert pts[0]['coord_frame'] == FIFF.FIFFV_COORD_MRI
```

### Step 2: Assign unknown = read_fiducials(...)

```python
pts, coord_frame = read_fiducials(fiducials_fname)
```

**Verification:**
```python
assert pts[0]['ident'] == FIFF.FIFFV_POINT_CARDINAL
```

### Step 3: Assign temp_fname = value

```python
temp_fname = tmp_path / 'test.fif'
```

**Verification:**
```python
assert coord_frame == coord_frame_1
```

### Step 4: Call write_fiducials()

```python
write_fiducials(temp_fname, pts, coord_frame)
```

**Verification:**
```python
assert pt['kind'] == pt_1['kind']
```

### Step 5: Assign unknown = read_fiducials(...)

```python
pts_1, coord_frame_1 = read_fiducials(temp_fname)
```

**Verification:**
```python
assert pt['ident'] == pt_1['ident']
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(pt['r'], pt_1['r'])
```

**Verification:**
```python
assert pt['coord_frame'] == pt_1['coord_frame']
```

### Step 7: Call write_fiducials()

```python
write_fiducials(temp_fname, pts, coord_frame, overwrite=True)
```

**Verification:**
```python
assert_array_equal(pt['r'], pt_1['r'])
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test fiducials i/o.'
pts, coord_frame = read_fiducials(fiducials_fname)
assert pts[0]['coord_frame'] == FIFF.FIFFV_COORD_MRI
assert pts[0]['ident'] == FIFF.FIFFV_POINT_CARDINAL
temp_fname = tmp_path / 'test.fif'
write_fiducials(temp_fname, pts, coord_frame)
pts_1, coord_frame_1 = read_fiducials(temp_fname)
assert coord_frame == coord_frame_1
for pt, pt_1 in zip(pts, pts_1):
    assert pt['kind'] == pt_1['kind']
    assert pt['ident'] == pt_1['ident']
    assert pt['coord_frame'] == pt_1['coord_frame']
    assert_array_equal(pt['r'], pt_1['r'])
    assert isinstance(pt, DigPoint)
    assert isinstance(pt_1, DigPoint)
pts[0]['coord_frame'] += 1
with pytest.raises(ValueError, match='coord_frame entries that are incom'):
    write_fiducials(temp_fname, pts, coord_frame, overwrite=True)
```

## Next Steps


---

*Source: test_meas_info.py:203 | Complexity: Intermediate | Last updated: 2026-05-18*