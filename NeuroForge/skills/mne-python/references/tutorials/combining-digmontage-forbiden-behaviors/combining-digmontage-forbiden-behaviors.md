# How To: Combining Digmontage Forbiden Behaviors

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test combining different DigMontage objects with repeated names.

## Prerequisites

**Required Modules:**
- `shutil`
- `contextlib`
- `functools`
- `itertools`
- `pathlib`
- `string`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.channels.montage`
- `mne`
- `mne`
- `mne._fiff._digitization`
- `mne._fiff.constants`
- `mne.bem`
- `mne.channels`
- `mne.channels.montage`
- `mne.coreg`
- `mne.datasets`
- `mne.io`
- `mne.io.kit`
- `mne.preprocessing`
- `mne.transforms`
- `mne.utils`
- `mne.utils._testing`
- `mne.viz._3d`


## Step-by-Step Guide

### Step 1: 'Test combining different DigMontage objects with repeated names.'

```python
'Test combining different DigMontage objects with repeated names.'
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

### Step 3: Assign fiducials = dict(...)

```python
fiducials = dict(zip(('nasion', 'lpa', 'rpa'), rng.rand(3, 3)))
```

### Step 4: Assign dig1 = make_dig_montage(...)

```python
dig1 = make_dig_montage(**fiducials, ch_pos=dict(zip(list('abc'), rng.rand(3, 3))))
```

### Step 5: Assign dig2 = make_dig_montage(...)

```python
dig2 = make_dig_montage(**fiducials, ch_pos=dict(zip(list('bcd'), rng.rand(3, 3))))
```

### Step 6: Assign dig2_wrong_fid = make_dig_montage(...)

```python
dig2_wrong_fid = make_dig_montage(nasion=rng.rand(3), lpa=rng.rand(3), rpa=rng.rand(3), ch_pos=dict(zip(list('ghi'), rng.rand(3, 3))))
```

### Step 7: Assign dig2_wrong_coordframe = make_dig_montage(...)

```python
dig2_wrong_coordframe = make_dig_montage(**fiducials, ch_pos=dict(zip(list('ghi'), rng.rand(3, 3))), coord_frame='meg')
```

### Step 8: Assign EXPECTED_ERR_MSG = "Cannot.*duplicated channel.*found: 'b', 'c'."

```python
EXPECTED_ERR_MSG = "Cannot.*duplicated channel.*found: 'b', 'c'."
```

### Step 9: Assign _ = value

```python
_ = dig1 + dig2
```

### Step 10: Assign _ = value

```python
_ = dig1 + dig2_wrong_fid
```

### Step 11: Assign _ = value

```python
_ = dig1 + dig2_wrong_coordframe
```


## Complete Example

```python
# Workflow
'Test combining different DigMontage objects with repeated names.'
rng = np.random.RandomState(0)
fiducials = dict(zip(('nasion', 'lpa', 'rpa'), rng.rand(3, 3)))
dig1 = make_dig_montage(**fiducials, ch_pos=dict(zip(list('abc'), rng.rand(3, 3))))
dig2 = make_dig_montage(**fiducials, ch_pos=dict(zip(list('bcd'), rng.rand(3, 3))))
dig2_wrong_fid = make_dig_montage(nasion=rng.rand(3), lpa=rng.rand(3), rpa=rng.rand(3), ch_pos=dict(zip(list('ghi'), rng.rand(3, 3))))
dig2_wrong_coordframe = make_dig_montage(**fiducials, ch_pos=dict(zip(list('ghi'), rng.rand(3, 3))), coord_frame='meg')
EXPECTED_ERR_MSG = "Cannot.*duplicated channel.*found: 'b', 'c'."
with pytest.raises(RuntimeError, match=EXPECTED_ERR_MSG):
    _ = dig1 + dig2
with pytest.raises(RuntimeError, match='fiducial locations do not match'):
    _ = dig1 + dig2_wrong_fid
with pytest.raises(RuntimeError, match='not in the same coordinate '):
    _ = dig1 + dig2_wrong_coordframe
```

## Next Steps


---

*Source: test_montage.py:951 | Complexity: Advanced | Last updated: 2026-05-18*