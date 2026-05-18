# How To: To Data Frame

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test EDF/BDF Raw Pandas exporter.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `datetime`
- `contextlib`
- `functools`
- `io`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy.io`
- `mne`
- `mne._fiff.pick`
- `mne.annotations`
- `mne.datasets`
- `mne.io`
- `mne.io.edf.edf`
- `mne.io.tests.test_raw`
- `mne.tests.test_annotations`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: fname
```

## Step-by-Step Guide

### Step 1: 'Test EDF/BDF Raw Pandas exporter.'

```python
'Test EDF/BDF Raw Pandas exporter.'
```

**Verification:**
```python
assert (df.columns == raw.ch_names).all()
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('pandas')
```

**Verification:**
```python
assert_array_equal(times, df.index.values[:10])
```

### Step 3: Assign ext = value

```python
ext = fname.suffix
```

**Verification:**
```python
assert 'time' in df.columns
```

### Step 4: Assign unknown = value

```python
_, times = raw[0, :10]
```

**Verification:**
```python
assert_array_equal(df.values[:, 1], raw._data[0] * 10000000000000.0)
```

### Step 5: Assign df = raw.to_data_frame(...)

```python
df = raw.to_data_frame(index='time')
```

**Verification:**
```python
assert (df.columns == raw.ch_names).all()
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(times, df.index.values[:10])
```

### Step 7: Assign df = raw.to_data_frame(...)

```python
df = raw.to_data_frame(index=None, scalings={'eeg': 10000000000000.0})
```

**Verification:**
```python
assert 'time' in df.columns
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(df.values[:, 1], raw._data[0] * 10000000000000.0)
```

### Step 9: Assign raw = read_raw_edf(...)

```python
raw = read_raw_edf(fname, preload=True, verbose='error')
```

### Step 10: Assign raw = read_raw_bdf(...)

```python
raw = read_raw_bdf(fname, preload=True, verbose='error')
```


## Complete Example

```python
# Setup
# Fixtures: fname

# Workflow
'Test EDF/BDF Raw Pandas exporter.'
pytest.importorskip('pandas')
ext = fname.suffix
if ext == '.edf':
    raw = read_raw_edf(fname, preload=True, verbose='error')
elif ext == '.bdf':
    raw = read_raw_bdf(fname, preload=True, verbose='error')
_, times = raw[0, :10]
df = raw.to_data_frame(index='time')
assert (df.columns == raw.ch_names).all()
assert_array_equal(times, df.index.values[:10])
df = raw.to_data_frame(index=None, scalings={'eeg': 10000000000000.0})
assert 'time' in df.columns
assert_array_equal(df.values[:, 1], raw._data[0] * 10000000000000.0)
```

## Next Steps


---

*Source: test_edf.py:418 | Complexity: Advanced | Last updated: 2026-05-18*