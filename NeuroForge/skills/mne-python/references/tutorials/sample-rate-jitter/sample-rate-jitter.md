# How To: Sample Rate Jitter

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test handling of jittered sample times.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `datetime`
- `shutil`
- `contextlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne._fiff.constants`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.tests.test_raw`
- `mne.preprocessing.nirs`
- `mne.transforms`
- `mne.utils`
- `shutil`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test handling of jittered sample times.'

```python
'Test handling of jittered sample times.'
```

**Verification:**
```python
assert 'Found jitter of 0.9' in lines
```

### Step 2: Assign new_file = value

```python
new_file = tmp_path / 'snirf_nirsport2_2019.snirf'
```

### Step 3: Call copy2()

```python
copy2(snirf_nirsport2_20219, new_file)
```

### Step 4: Call _chmod_rw_R()

```python
_chmod_rw_R(tmp_path)
```

### Step 5: Call read_raw_snirf()

```python
read_raw_snirf(new_file)
```

### Step 6: Assign lines = unknown.join(...)

```python
lines = '\n'.join((line for line in log.getvalue().splitlines() if 'jitter' in line))
```

**Verification:**
```python
assert 'Found jitter of 0.9' in lines
```

### Step 7: Assign orig_time = np.array(...)

```python
orig_time = np.array(f.get('nirs/data1/time'))
```

### Step 8: Assign acceptable_time_jitter = orig_time.copy(...)

```python
acceptable_time_jitter = orig_time.copy()
```

### Step 9: Assign mean_period = np.mean(...)

```python
mean_period = np.mean(np.diff(orig_time))
```

### Step 10: Call f.flush()

```python
f.flush()
```

### Step 11: Call f.create_dataset()

```python
f.create_dataset('nirs/data1/time', data=acceptable_time_jitter)
```

### Step 12: Call read_raw_snirf()

```python
read_raw_snirf(new_file)
```

### Step 13: Assign unacceptable_time_jitter = orig_time

```python
unacceptable_time_jitter = orig_time
```

### Step 14: Assign unknown = value

```python
unacceptable_time_jitter[-1] = unacceptable_time_jitter[-1] + 0.0102 * mean_period
```

### Step 15: Call f.flush()

```python
f.flush()
```

### Step 16: Call f.create_dataset()

```python
f.create_dataset('nirs/data1/time', data=unacceptable_time_jitter)
```

### Step 17: Call read_raw_snirf()

```python
read_raw_snirf(new_file, verbose=True)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test handling of jittered sample times.'
from shutil import copy2
new_file = tmp_path / 'snirf_nirsport2_2019.snirf'
copy2(snirf_nirsport2_20219, new_file)
_chmod_rw_R(tmp_path)
read_raw_snirf(new_file)
with h5py.File(new_file, 'r+') as f:
    orig_time = np.array(f.get('nirs/data1/time'))
    acceptable_time_jitter = orig_time.copy()
    mean_period = np.mean(np.diff(orig_time))
    acceptable_time_jitter[-1] += 0.0099 * mean_period
    del f['nirs/data1/time']
    f.flush()
    f.create_dataset('nirs/data1/time', data=acceptable_time_jitter)
with catch_logging('info') as log:
    read_raw_snirf(new_file)
lines = '\n'.join((line for line in log.getvalue().splitlines() if 'jitter' in line))
assert 'Found jitter of 0.9' in lines
with h5py.File(new_file, 'r+') as f:
    unacceptable_time_jitter = orig_time
    unacceptable_time_jitter[-1] = unacceptable_time_jitter[-1] + 0.0102 * mean_period
    del f['nirs/data1/time']
    f.flush()
    f.create_dataset('nirs/data1/time', data=unacceptable_time_jitter)
with pytest.warns(RuntimeWarning, match='non-uniformly-sampled data'):
    read_raw_snirf(new_file, verbose=True)
```

## Next Steps


---

*Source: test_snirf.py:584 | Complexity: Advanced | Last updated: 2026-05-18*