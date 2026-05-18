# How To: Reorder Channels

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test reordering of channels.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `hashlib`
- `contextlib`
- `copy`
- `functools`
- `pathlib`
- `numpy`
- `pooch`
- `pytest`
- `numpy.testing`
- `scipy.io`
- `mne`
- `mne._fiff.constants`
- `mne.channels`
- `mne.channels.channels`
- `mne.datasets`
- `mne.io`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: preload, proj
```

## Step-by-Step Guide

### Step 1: 'Test reordering of channels.'

```python
'Test reordering of channels.'
```

**Verification:**
```python
assert raw_new.ch_names == raw.ch_names[::-1]
```

### Step 2: Assign raw = read_raw_fif.crop.del_proj(...)

```python
raw = read_raw_fif(raw_fname).crop(0, 0.1).del_proj()
```

**Verification:**
```python
assert_allclose(raw_new._projector, raw._projector, atol=1e-12)
```

### Step 3: Assign raw_new = raw.copy.reorder_channels(...)

```python
raw_new = raw.copy().reorder_channels(raw.ch_names[::-1])
```

**Verification:**
```python
assert raw._projector is None
```

### Step 4: Call assert_array_equal()

```python
assert_array_equal(raw[:][0], raw_new[:][0][::-1])
```

**Verification:**
```python
assert raw_new._projector is None
```

### Step 5: Call raw_new.reorder_channels()

```python
raw_new.reorder_channels(raw_new.ch_names[::-1][1:-1])
```

**Verification:**
```python
assert_array_equal(raw[:][0], raw_new[:][0][::-1])
```

### Step 6: Call raw.drop_channels()

```python
raw.drop_channels(raw.ch_names[:1] + raw.ch_names[-1:])
```

**Verification:**
```python
assert_array_equal(raw[:][0], raw_new[:][0])
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(raw[:][0], raw_new[:][0])
```

**Verification:**
```python
assert_array_equal(raw[:][0], raw_new[rev][0])
```

### Step 8: Assign reord = value

```python
reord = [1, 0] + list(range(2, len(raw.ch_names)))
```

### Step 9: Assign rev = np.argsort(...)

```python
rev = np.argsort(reord)
```

### Step 10: Assign raw_new = raw.copy.pick(...)

```python
raw_new = raw.copy().pick(reord)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(raw[:][0], raw_new[rev][0])
```

### Step 12: Assign raw._projector = np.eye(...)

```python
raw._projector = np.eye(len(raw.ch_names))
```

### Step 13: Call raw.load_data()

```python
raw.load_data()
```

### Step 14: Call assert_allclose()

```python
assert_allclose(raw_new._projector, raw._projector, atol=1e-12)
```

**Verification:**
```python
assert raw._projector is None
```

### Step 15: Call raw.reorder_channels()

```python
raw.reorder_channels(raw.ch_names[:1] + raw.ch_names[:1])
```

### Step 16: Call raw.copy.reorder_channels()

```python
raw.copy().reorder_channels(raw.ch_names[::-1])
```


## Complete Example

```python
# Setup
# Fixtures: preload, proj

# Workflow
'Test reordering of channels.'
raw = read_raw_fif(raw_fname).crop(0, 0.1).del_proj()
if proj:
    raw._projector = np.eye(len(raw.ch_names))
if preload:
    raw.load_data()
if proj and (not preload):
    with pytest.raises(RuntimeError, match='load data'):
        raw.copy().reorder_channels(raw.ch_names[::-1])
    return
raw_new = raw.copy().reorder_channels(raw.ch_names[::-1])
assert raw_new.ch_names == raw.ch_names[::-1]
if proj:
    assert_allclose(raw_new._projector, raw._projector, atol=1e-12)
else:
    assert raw._projector is None
    assert raw_new._projector is None
assert_array_equal(raw[:][0], raw_new[:][0][::-1])
raw_new.reorder_channels(raw_new.ch_names[::-1][1:-1])
raw.drop_channels(raw.ch_names[:1] + raw.ch_names[-1:])
assert_array_equal(raw[:][0], raw_new[:][0])
with pytest.raises(ValueError, match='repeated'):
    raw.reorder_channels(raw.ch_names[:1] + raw.ch_names[:1])
reord = [1, 0] + list(range(2, len(raw.ch_names)))
rev = np.argsort(reord)
raw_new = raw.copy().pick(reord)
assert_array_equal(raw[:][0], raw_new[rev][0])
```

## Next Steps


---

*Source: test_channels.py:65 | Complexity: Advanced | Last updated: 2026-05-18*