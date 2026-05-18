# How To: Concatenate Raws Bads Order

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test concatenation of raws when the order of *bad* channels varies.

## Prerequisites

**Required Modules:**
- `datetime`
- `os`
- `pathlib`
- `pickle`
- `platform`
- `shutil`
- `contextlib`
- `copy`
- `functools`
- `io`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.tag`
- `mne.annotations`
- `mne.datasets`
- `mne.filter`
- `mne.io`
- `mne.io.tests.test_raw`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test concatenation of raws when the order of *bad* channels varies.'

```python
'Test concatenation of raws when the order of *bad* channels varies.'
```

**Verification:**
```python
assert np.all(raw_concat.get_data() == data_concat)
```

### Step 2: Assign raw0 = _create_toy_data(...)

```python
raw0 = _create_toy_data()
```

**Verification:**
```python
assert set(raw_concat.info['bads']) == {'0', '1'}
```

### Step 3: Assign raw1 = _create_toy_data(...)

```python
raw1 = _create_toy_data()
```

### Step 4: Assign unknown = value

```python
raw0.info['bads'] = ['0', '1']
```

### Step 5: Assign unknown = value

```python
raw1.info['bads'] = ['1', '0']
```

### Step 6: Assign raw_concat = concatenate_raws(...)

```python
raw_concat = concatenate_raws([raw0.copy(), raw1])
```

### Step 7: Assign data_concat = np.concatenate(...)

```python
data_concat = np.concatenate([raw0.get_data(), raw1.get_data()], 1)
```

**Verification:**
```python
assert np.all(raw_concat.get_data() == data_concat)
```

### Step 8: Assign raw2 = raw1.copy(...)

```python
raw2 = raw1.copy()
```

### Step 9: Assign unknown = value

```python
raw2.info['bads'] = ['0', '2']
```

### Step 10: Assign epochs1 = make_fixed_length_epochs(...)

```python
epochs1 = make_fixed_length_epochs(raw1)
```

### Step 11: Assign raw3 = _create_toy_data(...)

```python
raw3 = _create_toy_data(sfreq=500)
```

### Step 12: Assign unknown = value

```python
raw3.info['bads'] = ['0', '1']
```

### Step 13: Assign raw4 = _create_toy_data(...)

```python
raw4 = _create_toy_data(n_channels=4)
```

### Step 14: Call concatenate_raws()

```python
concatenate_raws([raw0, raw2])
```

### Step 15: Call concatenate_raws()

```python
concatenate_raws([raw0, epochs1.load_data()])
```

### Step 16: Call concatenate_raws()

```python
concatenate_raws([raw0, raw3])
```

### Step 17: Call concatenate_raws()

```python
concatenate_raws([raw0, raw4])
```


## Complete Example

```python
# Workflow
'Test concatenation of raws when the order of *bad* channels varies.'
raw0 = _create_toy_data()
raw1 = _create_toy_data()
raw0.info['bads'] = ['0', '1']
raw1.info['bads'] = ['1', '0']
raw_concat = concatenate_raws([raw0.copy(), raw1])
data_concat = np.concatenate([raw0.get_data(), raw1.get_data()], 1)
assert np.all(raw_concat.get_data() == data_concat)
assert set(raw_concat.info['bads']) == {'0', '1'}
raw2 = raw1.copy()
raw2.info['bads'] = ['0', '2']
with pytest.raises(ValueError, match='bads.*must match'):
    concatenate_raws([raw0, raw2])
epochs1 = make_fixed_length_epochs(raw1)
with pytest.raises(ValueError, match='type.*must match'):
    concatenate_raws([raw0, epochs1.load_data()])
raw3 = _create_toy_data(sfreq=500)
raw3.info['bads'] = ['0', '1']
with pytest.raises(ValueError, match='info.*must match'):
    concatenate_raws([raw0, raw3])
raw4 = _create_toy_data(n_channels=4)
with pytest.raises(ValueError, match='nchan.*must match'):
    concatenate_raws([raw0, raw4])
```

## Next Steps


---

*Source: test_raw_fiff.py:417 | Complexity: Advanced | Last updated: 2026-05-18*