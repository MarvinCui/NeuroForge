# How To: Get Sd Distances

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test source-detector distance selection and validation.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne.datasets`
- `mne.datasets.testing`
- `mne.io`
- `mne.preprocessing.nirs`
- `mne.preprocessing.nirs._beer_lambert_law`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test source-detector distance selection and validation.'

```python
'Test source-detector distance selection and validation.'
```

**Verification:**
```python
assert_allclose(_get_sd_distances(raw, None), expected, rtol=1e-12, atol=0)
```

### Step 2: Assign raw = RawArray(...)

```python
raw = RawArray(np.zeros((4, 3)), create_info(['S1_D1 760', 'S1_D1 850', 'S2_D2 760', 'S2_D2 850'], 1.0, 'fnirs_od'))
```

**Verification:**
```python
assert_allclose(_get_sd_distances(raw, expected), expected, rtol=1e-12, atol=0)
```

### Step 3: Assign expected = np.array(...)

```python
expected = np.array([0.03, 0.03, 0.04, 0.04])
```

**Verification:**
```python
assert_allclose(_get_sd_distances(raw, 0.05), np.full(4, 0.05), rtol=1e-12, atol=0)
```

### Step 4: Call assert_allclose()

```python
assert_allclose(_get_sd_distances(raw, None), expected, rtol=1e-12, atol=0)
```

**Verification:**
```python
assert_allclose(_get_sd_distances(raw, expected), expected, rtol=1e-12, atol=0)
```

### Step 5: Call assert_allclose()

```python
assert_allclose(_get_sd_distances(raw, expected), expected, rtol=1e-12, atol=0)
```

### Step 6: Assign unknown = value

```python
raw.info['chs'][idx]['loc'][3:6] = [0.0, 0.0, 0.0]
```

### Step 7: Assign unknown = value

```python
raw.info['chs'][idx]['loc'][6:9] = [distance, 0.0, 0.0]
```

### Step 8: Assign unknown = freq

```python
raw.info['chs'][idx]['loc'][9] = freq
```

### Step 9: Call assert_allclose()

```python
assert_allclose(_get_sd_distances(raw, expected), expected, rtol=1e-12, atol=0)
```

### Step 10: Call assert_allclose()

```python
assert_allclose(_get_sd_distances(raw, 0.05), np.full(4, 0.05), rtol=1e-12, atol=0)
```

### Step 11: Assign unknown = value

```python
raw.info['chs'][idx]['loc'][3:9] = np.nan
```

### Step 12: Call _get_sd_distances()

```python
_get_sd_distances(raw, np.ones((2, 2)))
```

### Step 13: Call _get_sd_distances()

```python
_get_sd_distances(raw, [0.03, 0.03])
```

### Step 14: Call _get_sd_distances()

```python
_get_sd_distances(raw, 'foo')
```


## Complete Example

```python
# Workflow
'Test source-detector distance selection and validation.'
raw = RawArray(np.zeros((4, 3)), create_info(['S1_D1 760', 'S1_D1 850', 'S2_D2 760', 'S2_D2 850'], 1.0, 'fnirs_od'))
expected = np.array([0.03, 0.03, 0.04, 0.04])
for idx, (freq, distance) in enumerate(zip([760, 850, 760, 850], expected)):
    raw.info['chs'][idx]['loc'][3:6] = [0.0, 0.0, 0.0]
    raw.info['chs'][idx]['loc'][6:9] = [distance, 0.0, 0.0]
    raw.info['chs'][idx]['loc'][9] = freq
assert_allclose(_get_sd_distances(raw, None), expected, rtol=1e-12, atol=0)
with pytest.warns(RuntimeWarning, match='(?i)will be overridden'):
    assert_allclose(_get_sd_distances(raw, expected), expected, rtol=1e-12, atol=0)
with pytest.warns(RuntimeWarning, match='(?i)will be overridden'):
    assert_allclose(_get_sd_distances(raw, 0.05), np.full(4, 0.05), rtol=1e-12, atol=0)
for idx in range(len(raw.info['chs'])):
    raw.info['chs'][idx]['loc'][3:9] = np.nan
assert_allclose(_get_sd_distances(raw, expected), expected, rtol=1e-12, atol=0)
with pytest.raises(ValueError, match='1D array-like'):
    _get_sd_distances(raw, np.ones((2, 2)))
with pytest.raises(ValueError, match='length matching'):
    _get_sd_distances(raw, [0.03, 0.03])
with pytest.raises(TypeError, match='sd_distances'):
    _get_sd_distances(raw, 'foo')
```

## Next Steps


---

*Source: test_beer_lambert_law.py:165 | Complexity: Advanced | Last updated: 2026-05-18*