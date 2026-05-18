# How To: Io Set Raw

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test importing EEGLAB .set files.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `shutil`
- `time`
- `copy`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne`
- `mne.annotations`
- `mne.channels`
- `mne.datasets`
- `mne.io`
- `mne.io.eeglab._eeglab`
- `mne.io.eeglab.eeglab`
- `mne.io.tests.test_raw`
- `mne.utils`
- `eeglabio.raw`

**Setup Required:**
```python
# Fixtures: fname
```

## Step-by-Step Guide

### Step 1: 'Test importing EEGLAB .set files.'

```python
'Test importing EEGLAB .set files.'
```

**Verification:**
```python
assert len(raw0.annotations) == 154
```

### Step 2: Assign montage = read_custom_montage(...)

```python
montage = read_custom_montage(montage_path)
```

**Verification:**
```python
assert set(raw0.annotations.description) == {'rt', 'square'}
```

### Step 3: Assign montage.ch_names = value

```python
montage.ch_names = [f'EEG {ii:03d}' for ii in range(len(montage.ch_names))]
```

**Verification:**
```python
assert_array_equal(raw0.annotations.duration, 0.0)
```

### Step 4: Assign kws = dict(...)

```python
kws = dict(reader=read_raw_eeglab, input_fname=fname)
```

### Step 5: Assign read_raw_kws = dict(...)

```python
read_raw_kws = dict(input_fname=fname, preload=False, uint16_codec='ascii')
```

### Step 6: Call raw0.set_montage()

```python
raw0.set_montage(montage, on_missing='ignore')
```

### Step 7: Call raw0.crop()

```python
raw0.crop(0, 1)
```

### Step 8: Call raw0.set_montage()

```python
raw0.set_montage(montage)
```

### Step 9: Call raw0.filter()

```python
raw0.filter(1, None, l_trans_bandwidth='auto', filter_length='auto', phase='zero')
```

### Step 10: Assign raw0 = read_raw_eeglab(...)

```python
raw0 = read_raw_eeglab(**read_raw_kws)
```

### Step 11: Call raw0.set_montage()

```python
raw0.set_montage(montage)
```

**Verification:**
```python
assert len(raw0.annotations) == 154
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(raw0.annotations.duration, 0.0)
```

### Step 13: Assign raw0 = _test_raw_reader(...)

```python
raw0 = _test_raw_reader(**kws)
```

### Step 14: Assign raw0 = read_raw_eeglab(...)

```python
raw0 = read_raw_eeglab(fname, preload=True)
```

### Step 15: Assign raw0 = _test_raw_reader(...)

```python
raw0 = _test_raw_reader(**kws)
```

### Step 16: Assign raw0 = read_raw_eeglab(...)

```python
raw0 = read_raw_eeglab(**read_raw_kws)
```

### Step 17: Call raw0.set_montage()

```python
raw0.set_montage(montage, on_missing='ignore')
```


## Complete Example

```python
# Setup
# Fixtures: fname

# Workflow
'Test importing EEGLAB .set files.'
montage = read_custom_montage(montage_path)
montage.ch_names = [f'EEG {ii:03d}' for ii in range(len(montage.ch_names))]
kws = dict(reader=read_raw_eeglab, input_fname=fname)
if fname.name == 'test_raw_chanloc.set':
    with pytest.warns(RuntimeWarning, match="The data contains 'boundary' events"):
        raw0 = _test_raw_reader(**kws)
elif '_h5' in fname.name:
    raw0 = read_raw_eeglab(fname, preload=True)
else:
    raw0 = _test_raw_reader(**kws)
if fname.name == 'test_raw_chanloc.set':
    raw0.set_montage(montage, on_missing='ignore')
    raw0.crop(0, 1)
else:
    raw0.set_montage(montage)
    raw0.filter(1, None, l_trans_bandwidth='auto', filter_length='auto', phase='zero')
read_raw_kws = dict(input_fname=fname, preload=False, uint16_codec='ascii')
if fname.name == 'test_raw_chanloc.set':
    with pytest.warns(RuntimeWarning, match="The data contains 'boundary' events"):
        raw0 = read_raw_eeglab(**read_raw_kws)
        raw0.set_montage(montage, on_missing='ignore')
else:
    raw0 = read_raw_eeglab(**read_raw_kws)
    raw0.set_montage(montage)
if fname != raw_fname_chanloc:
    assert len(raw0.annotations) == 154
    assert set(raw0.annotations.description) == {'rt', 'square'}
    assert_array_equal(raw0.annotations.duration, 0.0)
```

## Next Steps


---

*Source: test_eeglab.py:66 | Complexity: Advanced | Last updated: 2026-05-18*