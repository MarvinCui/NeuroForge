# How To: Beer Lambert Sd Distances

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test Beer-Lambert conversion with explicit source-detector distances.

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

### Step 1: 'Test Beer-Lambert conversion with explicit source-detector distances.'

```python
'Test Beer-Lambert conversion with explicit source-detector distances.'
```

**Verification:**
```python
assert actual.ch_names == expected.ch_names
```

### Step 2: Assign data = np.array(...)

```python
data = np.array([[0.1, 0.2, 0.3], [0.15, 0.25, 0.35], [0.4, 0.5, 0.6], [0.45, 0.55, 0.65]])
```

**Verification:**
```python
assert_allclose(actual.get_data(), expected.get_data(), rtol=1e-12, atol=0)
```

### Step 3: Assign ch_names = value

```python
ch_names = ['S1_D1 760', 'S1_D1 850', 'S10_D10 760', 'S10_D10 850']
```

**Verification:**
```python
assert np.isnan(source_detector_distances(raw.info)).all()
```

### Step 4: Assign raw = RawArray(...)

```python
raw = RawArray(data, create_info(ch_names, sfreq=1.0, ch_types='fnirs_od'))
```

**Verification:**
```python
assert actual.ch_names == expected.ch_names
```

### Step 5: Assign sd_distances = value

```python
sd_distances = [0.03, 0.03, 0.03, 0.03]
```

**Verification:**
```python
assert_allclose(actual.get_data(), expected.get_data(), rtol=1e-12, atol=0)
```

### Step 6: Assign expected = beer_lambert_law(...)

```python
expected = beer_lambert_law(raw)
```

**Verification:**
```python
assert actual.ch_names == expected.ch_names
```

### Step 7: Call assert_allclose()

```python
assert_allclose(actual.get_data(), expected.get_data(), rtol=1e-12, atol=0)
```

**Verification:**
```python
assert_allclose(actual.get_data(), expected.get_data(), rtol=1e-12, atol=0)
```

### Step 8: Assign actual = beer_lambert_law(...)

```python
actual = beer_lambert_law(raw, sd_distances=sd_distances)
```

**Verification:**
```python
assert actual.ch_names == expected.ch_names
```

### Step 9: Call assert_allclose()

```python
assert_allclose(actual.get_data(), expected.get_data(), rtol=1e-12, atol=0)
```

### Step 10: Assign actual = beer_lambert_law(...)

```python
actual = beer_lambert_law(raw, sd_distances=sd_distances[0])
```

**Verification:**
```python
assert actual.ch_names == expected.ch_names
```

### Step 11: Call assert_allclose()

```python
assert_allclose(actual.get_data(), expected.get_data(), rtol=1e-12, atol=0)
```

### Step 12: Assign unknown = value

```python
raw.info['chs'][idx]['loc'][3:6] = [0.0, 0.0, 0.0]
```

### Step 13: Assign unknown = value

```python
raw.info['chs'][idx]['loc'][6:9] = [distance, 0.0, 0.0]
```

### Step 14: Assign unknown = freq

```python
raw.info['chs'][idx]['loc'][9] = freq
```

### Step 15: Assign actual = beer_lambert_law(...)

```python
actual = beer_lambert_law(raw, sd_distances=sd_distances)
```

### Step 16: Assign unknown = value

```python
raw.info['chs'][idx]['loc'][3:9] = np.nan
```

### Step 17: Call beer_lambert_law()

```python
beer_lambert_law(raw)
```


## Complete Example

```python
# Workflow
'Test Beer-Lambert conversion with explicit source-detector distances.'
data = np.array([[0.1, 0.2, 0.3], [0.15, 0.25, 0.35], [0.4, 0.5, 0.6], [0.45, 0.55, 0.65]])
ch_names = ['S1_D1 760', 'S1_D1 850', 'S10_D10 760', 'S10_D10 850']
raw = RawArray(data, create_info(ch_names, sfreq=1.0, ch_types='fnirs_od'))
sd_distances = [0.03, 0.03, 0.03, 0.03]
for idx, (freq, distance) in enumerate(zip([760, 850, 760, 850], sd_distances)):
    raw.info['chs'][idx]['loc'][3:6] = [0.0, 0.0, 0.0]
    raw.info['chs'][idx]['loc'][6:9] = [distance, 0.0, 0.0]
    raw.info['chs'][idx]['loc'][9] = freq
expected = beer_lambert_law(raw)
with pytest.warns(RuntimeWarning, match='(?i)will be overridden'):
    actual = beer_lambert_law(raw, sd_distances=sd_distances)
assert actual.ch_names == expected.ch_names
assert_allclose(actual.get_data(), expected.get_data(), rtol=1e-12, atol=0)
for idx in range(len(raw.info['chs'])):
    raw.info['chs'][idx]['loc'][3:9] = np.nan
assert np.isnan(source_detector_distances(raw.info)).all()
with pytest.raises(ValueError, match='(?i)source-detector distances are all zero or NaN'):
    beer_lambert_law(raw)
actual = beer_lambert_law(raw, sd_distances=sd_distances)
assert actual.ch_names == expected.ch_names
assert_allclose(actual.get_data(), expected.get_data(), rtol=1e-12, atol=0)
actual = beer_lambert_law(raw, sd_distances=sd_distances[0])
assert actual.ch_names == expected.ch_names
assert_allclose(actual.get_data(), expected.get_data(), rtol=1e-12, atol=0)
```

## Next Steps


---

*Source: test_beer_lambert_law.py:122 | Complexity: Advanced | Last updated: 2026-05-18*