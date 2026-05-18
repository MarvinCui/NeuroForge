# How To: Fnirs Spread Bads

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

**Verification:**
```python
assert info['bads'] == raw.ch_names[:nfreqs]
```

### Step 2: Assign raw = readerfn(...)

```python
raw = readerfn(fname)
```

**Verification:**
```python
assert info['bads'] == sorted(expected_bads)
```

### Step 3: Assign nfreqs = len(...)

```python
nfreqs = len(set(_channel_frequencies(raw.info)))
```

**Verification:**
```python
assert info['bads'] == [info.ch_names[x] for x in [0, 1, 8, 9]]
```

### Step 4: Assign unknown = value

```python
raw.info['bads'] = [raw.ch_names[0]]
```

### Step 5: Assign info = _fnirs_spread_bads(...)

```python
info = _fnirs_spread_bads(raw.info)
```

**Verification:**
```python
assert info['bads'] == raw.ch_names[:nfreqs]
```

### Step 6: Assign raw_od = optical_density(...)

```python
raw_od = optical_density(raw)
```

### Step 7: Assign bads = value

```python
bads = [raw_od.ch_names[nfreqs * ii + ii] for ii in range(nfreqs)]
```

### Step 8: Assign expected_bads = value

```python
expected_bads = raw_od.ch_names[:nfreqs ** 2]
```

### Step 9: Assign unknown = bads

```python
raw_od.info['bads'] = bads
```

### Step 10: Assign info = _fnirs_spread_bads(...)

```python
info = _fnirs_spread_bads(raw_od.info)
```

**Verification:**
```python
assert info['bads'] == sorted(expected_bads)
```

### Step 11: Assign raw_hb = beer_lambert_law(...)

```python
raw_hb = beer_lambert_law(raw_od)
```

### Step 12: Assign unknown = value

```python
raw_hb.info['bads'] = [raw_hb.ch_names[x] for x in [1, 8]]
```

### Step 13: Assign info = _fnirs_spread_bads(...)

```python
info = _fnirs_spread_bads(raw_hb.info)
```

**Verification:**
```python
assert info['bads'] == [info.ch_names[x] for x in [0, 1, 8, 9]]
```


## Complete Example

```python
# Setup
# Fixtures: fname, readerfn

# Workflow
'Test checking of bad markings.'
raw = readerfn(fname)
nfreqs = len(set(_channel_frequencies(raw.info)))
raw.info['bads'] = [raw.ch_names[0]]
info = _fnirs_spread_bads(raw.info)
assert info['bads'] == raw.ch_names[:nfreqs]
raw_od = optical_density(raw)
bads = [raw_od.ch_names[nfreqs * ii + ii] for ii in range(nfreqs)]
expected_bads = raw_od.ch_names[:nfreqs ** 2]
raw_od.info['bads'] = bads
info = _fnirs_spread_bads(raw_od.info)
assert info['bads'] == sorted(expected_bads)
raw_hb = beer_lambert_law(raw_od)
raw_hb.info['bads'] = [raw_hb.ch_names[x] for x in [1, 8]]
info = _fnirs_spread_bads(raw_hb.info)
assert info['bads'] == [info.ch_names[x] for x in [0, 1, 8, 9]]
```

## Next Steps


---

*Source: test_nirs.py:179 | Complexity: Advanced | Last updated: 2026-05-18*