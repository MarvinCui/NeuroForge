# How To: Concatenate Raws Order

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test concatenation of raws when the order of *good* channels varies.

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

### Step 1: 'Test concatenation of raws when the order of *good* channels varies.'

```python
'Test concatenation of raws when the order of *good* channels varies.'
```

**Verification:**
```python
assert raw0.ch_names == raw1.ch_names == raw_concat.ch_names == ['0', '1']
```

### Step 2: Assign raw0 = _create_toy_data(...)

```python
raw0 = _create_toy_data(n_channels=2)
```

**Verification:**
```python
assert np.all(ch0 == 0)
```

### Step 3: Assign unknown = np.zeros_like(...)

```python
raw0._data[0] = np.zeros_like(raw0._data[0])
```

**Verification:**
```python
assert raw1.ch_names == ['1', '0']
```

### Step 4: Assign raw1 = raw0.copy(...)

```python
raw1 = raw0.copy()
```

**Verification:**
```python
assert np.all(ch0 == 0)
```

### Step 5: Assign raw_concat = concatenate_raws(...)

```python
raw_concat = concatenate_raws([raw0.copy(), raw1])
```

**Verification:**
```python
assert raw0.ch_names == raw1.ch_names == raw_concat.ch_names == ['0', '1']
```

### Step 6: Assign ch0 = raw_concat.get_data(...)

```python
ch0 = raw_concat.get_data(picks=['0'])
```

**Verification:**
```python
assert np.all(ch0 == 0)
```

### Step 7: Call raw1.reorder_channels()

```python
raw1.reorder_channels(['1', '0'])
```

**Verification:**
```python
assert raw1.ch_names == ['1', '0']
```

### Step 8: Assign raws = value

```python
raws = [raw0.copy(), raw1]
```

### Step 9: Call match_channel_orders()

```python
match_channel_orders(insts=raws, copy=False)
```

### Step 10: Assign raw_concat = concatenate_raws(...)

```python
raw_concat = concatenate_raws(raws)
```

### Step 11: Assign ch0 = raw_concat.get_data(...)

```python
ch0 = raw_concat.get_data(picks=['0'])
```

**Verification:**
```python
assert np.all(ch0 == 0)
```

### Step 12: Assign raw_concat = concatenate_raws(...)

```python
raw_concat = concatenate_raws(raws)
```

### Step 13: Call match_channel_orders()

```python
match_channel_orders(insts=raws, copy=True)
```

### Step 14: Assign raw_concat = concatenate_raws(...)

```python
raw_concat = concatenate_raws(raws)
```


## Complete Example

```python
# Workflow
'Test concatenation of raws when the order of *good* channels varies.'
raw0 = _create_toy_data(n_channels=2)
raw0._data[0] = np.zeros_like(raw0._data[0])
raw1 = raw0.copy()
raw_concat = concatenate_raws([raw0.copy(), raw1])
assert raw0.ch_names == raw1.ch_names == raw_concat.ch_names == ['0', '1']
ch0 = raw_concat.get_data(picks=['0'])
assert np.all(ch0 == 0)
raw1.reorder_channels(['1', '0'])
assert raw1.ch_names == ['1', '0']
raws = [raw0.copy(), raw1]
with pytest.raises(ValueError, match='Channel order must match.'):
    raw_concat = concatenate_raws(raws)
with pytest.raises(ValueError, match='Channel order must match.'):
    match_channel_orders(insts=raws, copy=True)
    raw_concat = concatenate_raws(raws)
match_channel_orders(insts=raws, copy=False)
raw_concat = concatenate_raws(raws)
ch0 = raw_concat.get_data(picks=['0'])
assert np.all(ch0 == 0)
```

## Next Steps


---

*Source: test_raw_fiff.py:459 | Complexity: Advanced | Last updated: 2026-05-18*