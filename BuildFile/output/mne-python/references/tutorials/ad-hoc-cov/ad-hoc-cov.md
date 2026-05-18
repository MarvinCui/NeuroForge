# How To: Ad Hoc Cov

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test ad hoc cov creation and I/O.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `sys`
- `inspect`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.pick`
- `mne.channels`
- `mne.cov`
- `mne.datasets`
- `mne.fixes`
- `mne.io`
- `mne.preprocessing`
- `mne.rank`
- `mne.utils`
- `sklearn`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test ad hoc cov creation and I/O.'

```python
'Test ad hoc cov creation and I/O.'
```

**Verification:**
```python
assert 'Covariance' in repr(cov)
```

### Step 2: Assign out_fname = value

```python
out_fname = tmp_path / 'test-cov.fif'
```

**Verification:**
```python
assert_array_almost_equal(cov['data'], cov2['data'])
```

### Step 3: Assign evoked = value

```python
evoked = read_evokeds(ave_fname)[0]
```

**Verification:**
```python
assert 'Covariance' in repr(cov)
```

### Step 4: Assign cov = make_ad_hoc_cov(...)

```python
cov = make_ad_hoc_cov(evoked.info)
```

**Verification:**
```python
assert_array_almost_equal(cov['data'], cov2['data'])
```

### Step 5: Call cov.save()

```python
cov.save(out_fname)
```

**Verification:**
```python
assert 'Covariance' in repr(cov)
```

### Step 6: Assign cov2 = read_cov(...)

```python
cov2 = read_cov(out_fname)
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(cov['data'], cov2['data'])
```

### Step 8: Assign std = dict(...)

```python
std = dict(grad=2e-13, mag=1e-14, eeg=1e-07)
```

### Step 9: Assign cov = make_ad_hoc_cov(...)

```python
cov = make_ad_hoc_cov(evoked.info, std)
```

### Step 10: Call cov.save()

```python
cov.save(out_fname, overwrite=True)
```

**Verification:**
```python
assert 'Covariance' in repr(cov)
```

### Step 11: Assign cov2 = read_cov(...)

```python
cov2 = read_cov(out_fname)
```

### Step 12: Call assert_array_almost_equal()

```python
assert_array_almost_equal(cov['data'], cov2['data'])
```

### Step 13: Assign unknown = np.diag(...)

```python
cov['data'] = np.diag(cov['data'])
```

### Step 14: Assign unknown = False

```python
cov['diag'] = False
```

### Step 15: Call cov._get_square()

```python
cov._get_square()
```

### Step 16: Assign unknown = np.diag(...)

```python
cov['data'] = np.diag(cov['data'])
```

### Step 17: Call cov._get_square()

```python
cov._get_square()
```

### Step 18: Call cov._get_square()

```python
cov._get_square()
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test ad hoc cov creation and I/O.'
out_fname = tmp_path / 'test-cov.fif'
evoked = read_evokeds(ave_fname)[0]
cov = make_ad_hoc_cov(evoked.info)
cov.save(out_fname)
assert 'Covariance' in repr(cov)
cov2 = read_cov(out_fname)
assert_array_almost_equal(cov['data'], cov2['data'])
std = dict(grad=2e-13, mag=1e-14, eeg=1e-07)
cov = make_ad_hoc_cov(evoked.info, std)
cov.save(out_fname, overwrite=True)
assert 'Covariance' in repr(cov)
cov2 = read_cov(out_fname)
assert_array_almost_equal(cov['data'], cov2['data'])
cov['data'] = np.diag(cov['data'])
with pytest.raises(RuntimeError, match='attributes inconsistent'):
    cov._get_square()
cov['diag'] = False
cov._get_square()
cov['data'] = np.diag(cov['data'])
with pytest.raises(RuntimeError, match='attributes inconsistent'):
    cov._get_square()
```

## Next Steps


---

*Source: test_cov.py:238 | Complexity: Advanced | Last updated: 2026-05-18*