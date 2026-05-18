# How To: Rawctf Clean Names

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test RawCTF _clean_names method.

## Prerequisites

**Required Modules:**
- `copy`
- `os`
- `shutil`
- `datetime`
- `os`
- `numpy`
- `pytest`
- `numpy`
- `numpy.testing`
- `mne`
- `mne.io.ctf.info`
- `mne`
- `mne._fiff.compensator`
- `mne._fiff.constants`
- `mne._fiff.pick`
- `mne.datasets`
- `mne.io`
- `mne.io.ctf.constants`
- `mne.io.ctf.info`
- `mne.io.tests.test_raw`
- `mne.tests.test_annotations`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test RawCTF _clean_names method.'

```python
'Test RawCTF _clean_names method.'
```

**Verification:**
```python
assert raw.ch_names != test_channel_names
```

### Step 2: Assign test_channel_names = _clean_names(...)

```python
test_channel_names = _clean_names(raw.ch_names)
```

**Verification:**
```python
assert chs_ch_names != test_channel_names
```

### Step 3: Assign test_info_comps = copy.deepcopy(...)

```python
test_info_comps = copy.deepcopy(raw.info['comps'])
```

**Verification:**
```python
assert not array_equal(_clean_names(test_comp['data'][key]), comp['data'][key])
```

### Step 4: Assign chs_ch_names = value

```python
chs_ch_names = [ch['ch_name'] for ch in raw.info['chs']]
```

**Verification:**
```python
assert raw_cleaned.ch_names == test_channel_names
```

### Step 5: Assign raw = read_raw_ctf(...)

```python
raw = read_raw_ctf(op.join(ctf_dir, ctf_fname_catch))
```

**Verification:**
```python
assert ch['ch_name'] == test_ch_name
```

### Step 6: Assign raw_cleaned = read_raw_ctf(...)

```python
raw_cleaned = read_raw_ctf(op.join(ctf_dir, ctf_fname_catch), clean_names=True)
```

**Verification:**
```python
assert _clean_names(test_comp['data'][key]) == comp['data'][key]
```


## Complete Example

```python
# Workflow
'Test RawCTF _clean_names method.'
with pytest.warns(RuntimeWarning, match='ref channel RMSP did not'):
    raw = read_raw_ctf(op.join(ctf_dir, ctf_fname_catch))
    raw_cleaned = read_raw_ctf(op.join(ctf_dir, ctf_fname_catch), clean_names=True)
test_channel_names = _clean_names(raw.ch_names)
test_info_comps = copy.deepcopy(raw.info['comps'])
assert raw.ch_names != test_channel_names
chs_ch_names = [ch['ch_name'] for ch in raw.info['chs']]
assert chs_ch_names != test_channel_names
for test_comp, comp in zip(test_info_comps, raw.info['comps']):
    for key in ('row_names', 'col_names'):
        assert not array_equal(_clean_names(test_comp['data'][key]), comp['data'][key])
assert raw_cleaned.ch_names == test_channel_names
for ch, test_ch_name in zip(raw_cleaned.info['chs'], test_channel_names):
    assert ch['ch_name'] == test_ch_name
for test_comp, comp in zip(test_info_comps, raw_cleaned.info['comps']):
    for key in ('row_names', 'col_names'):
        assert _clean_names(test_comp['data'][key]) == comp['data'][key]
```

## Next Steps


---

*Source: test_ctf.py:310 | Complexity: Intermediate | Last updated: 2026-05-18*