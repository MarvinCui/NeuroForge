# How To: Snirf Against Nirx

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test Homer generated against file snirf was created from.

## Prerequisites

**Required Modules:**
- `datetime`
- `shutil`
- `contextlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne._fiff.constants`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.tests.test_raw`
- `mne.preprocessing.nirs`
- `mne.transforms`
- `mne.utils`
- `shutil`


## Step-by-Step Guide

### Step 1: 'Test Homer generated against file snirf was created from.'

```python
'Test Homer generated against file snirf was created from.'
```

**Verification:**
```python
assert_allclose(raw_homer.annotations.onset, raw_orig.annotations.onset)
```

### Step 2: Assign raw_homer = read_raw_snirf(...)

```python
raw_homer = read_raw_snirf(sfnirs_homer_103_wShort, preload=True)
```

**Verification:**
```python
assert_allclose([float(d) for d in raw_homer.annotations.description], [float(d) for d in raw_orig.annotations.description])
```

### Step 3: Call _reorder_nirx()

```python
_reorder_nirx(raw_homer)
```

**Verification:**
```python
assert raw_homer.info['ch_names'] == raw_orig.info['ch_names']
```

### Step 4: Assign raw_orig = read_raw_nirx(...)

```python
raw_orig = read_raw_nirx(sfnirs_homer_103_wShort_original, preload=True)
```

**Verification:**
```python
assert_allclose([new_chs[idx]['loc'][9] for idx in range(num_chans)], [ori_chs[idx]['loc'][9] for idx in range(num_chans)])
```

### Step 5: Call assert_allclose()

```python
assert_allclose(raw_homer.annotations.onset, raw_orig.annotations.onset)
```

**Verification:**
```python
assert_allclose(raw_homer.get_data(), raw_orig.get_data())
```

### Step 6: Call assert_allclose()

```python
assert_allclose([float(d) for d in raw_homer.annotations.description], [float(d) for d in raw_orig.annotations.description])
```

**Verification:**
```python
assert raw_homer.info['ch_names'] == raw_orig.info['ch_names']
```

### Step 7: Assign num_chans = len(...)

```python
num_chans = len(raw_homer.ch_names)
```

### Step 8: Assign new_chs = value

```python
new_chs = raw_homer.info['chs']
```

### Step 9: Assign ori_chs = value

```python
ori_chs = raw_orig.info['chs']
```

### Step 10: Call assert_allclose()

```python
assert_allclose([new_chs[idx]['loc'][9] for idx in range(num_chans)], [ori_chs[idx]['loc'][9] for idx in range(num_chans)])
```

### Step 11: Call assert_allclose()

```python
assert_allclose(raw_homer.get_data(), raw_orig.get_data())
```


## Complete Example

```python
# Workflow
'Test Homer generated against file snirf was created from.'
raw_homer = read_raw_snirf(sfnirs_homer_103_wShort, preload=True)
_reorder_nirx(raw_homer)
raw_orig = read_raw_nirx(sfnirs_homer_103_wShort_original, preload=True)
assert_allclose(raw_homer.annotations.onset, raw_orig.annotations.onset)
assert_allclose([float(d) for d in raw_homer.annotations.description], [float(d) for d in raw_orig.annotations.description])
assert raw_homer.info['ch_names'] == raw_orig.info['ch_names']
num_chans = len(raw_homer.ch_names)
new_chs = raw_homer.info['chs']
ori_chs = raw_orig.info['chs']
assert_allclose([new_chs[idx]['loc'][9] for idx in range(num_chans)], [ori_chs[idx]['loc'][9] for idx in range(num_chans)])
assert_allclose(raw_homer.get_data(), raw_orig.get_data())
```

## Next Steps


---

*Source: test_snirf.py:220 | Complexity: Advanced | Last updated: 2026-05-18*