# How To: Fnirs Check Bads

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test checking of bad markings.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.pick`
- `mne.datasets`
- `mne.datasets.testing`
- `mne.io`
- `mne.preprocessing.nirs`

**Setup Required:**
```python
# Fixtures: fname, readerfn
```

## Step-by-Step Guide

### Step 1: 'Test checking of bad markings.'

```python
'Test checking of bad markings.'
```

### Step 2: Assign raw = readerfn(...)

```python
raw = readerfn(fname)
```

### Step 3: Call _fnirs_check_bads()

```python
_fnirs_check_bads(raw.info)
```

### Step 4: Assign raw = optical_density(...)

```python
raw = optical_density(raw)
```

### Step 5: Call _fnirs_check_bads()

```python
_fnirs_check_bads(raw.info)
```

### Step 6: Assign raw = beer_lambert_law(...)

```python
raw = beer_lambert_law(raw)
```

### Step 7: Call _fnirs_check_bads()

```python
_fnirs_check_bads(raw.info)
```

### Step 8: Assign raw = readerfn(...)

```python
raw = readerfn(fname)
```

### Step 9: Assign nfreqs = len(...)

```python
nfreqs = len(set(_channel_frequencies(raw.info)))
```

### Step 10: Assign unknown = value

```python
raw.info['bads'] = raw.ch_names[0:nfreqs]
```

### Step 11: Call _fnirs_check_bads()

```python
_fnirs_check_bads(raw.info)
```

### Step 12: Assign raw = optical_density(...)

```python
raw = optical_density(raw)
```

### Step 13: Call _fnirs_check_bads()

```python
_fnirs_check_bads(raw.info)
```

### Step 14: Assign raw = beer_lambert_law(...)

```python
raw = beer_lambert_law(raw)
```

### Step 15: Call _fnirs_check_bads()

```python
_fnirs_check_bads(raw.info)
```

### Step 16: Assign raw = readerfn(...)

```python
raw = readerfn(fname)
```

### Step 17: Assign unknown = value

```python
raw.info['bads'] = raw.ch_names[0:1]
```

### Step 18: Call pytest.raises()

```python
pytest.raises(RuntimeError, _fnirs_check_bads, raw.info)
```

### Step 19: Assign unknown = value

```python
raw.info['bads'] = []
```

### Step 20: Assign raw = optical_density(...)

```python
raw = optical_density(raw)
```

### Step 21: Assign unknown = value

```python
raw.info['bads'] = raw.ch_names[0:1]
```

### Step 22: Call pytest.raises()

```python
pytest.raises(RuntimeError, _fnirs_check_bads, raw.info)
```

### Step 23: Call pytest.raises()

```python
pytest.raises(RuntimeError, _fnirs_check_bads, raw.info)
```

### Step 24: Assign raw = optical_density(...)

```python
raw = optical_density(raw)
```

### Step 25: Assign raw = beer_lambert_law(...)

```python
raw = beer_lambert_law(raw)
```


## Complete Example

```python
# Setup
# Fixtures: fname, readerfn

# Workflow
'Test checking of bad markings.'
raw = readerfn(fname)
_fnirs_check_bads(raw.info)
raw = optical_density(raw)
_fnirs_check_bads(raw.info)
raw = beer_lambert_law(raw)
_fnirs_check_bads(raw.info)
raw = readerfn(fname)
nfreqs = len(set(_channel_frequencies(raw.info)))
raw.info['bads'] = raw.ch_names[0:nfreqs]
_fnirs_check_bads(raw.info)
raw = optical_density(raw)
_fnirs_check_bads(raw.info)
raw = beer_lambert_law(raw)
_fnirs_check_bads(raw.info)
raw = readerfn(fname)
raw.info['bads'] = raw.ch_names[0:1]
pytest.raises(RuntimeError, _fnirs_check_bads, raw.info)
with pytest.raises(RuntimeError, match='bad labelling'):
    raw = optical_density(raw)
raw.info['bads'] = []
raw = optical_density(raw)
raw.info['bads'] = raw.ch_names[0:1]
pytest.raises(RuntimeError, _fnirs_check_bads, raw.info)
with pytest.raises(RuntimeError, match='bad labelling'):
    raw = beer_lambert_law(raw)
pytest.raises(RuntimeError, _fnirs_check_bads, raw.info)
```

## Next Steps


---

*Source: test_nirs.py:134 | Complexity: Advanced | Last updated: 2026-05-18*