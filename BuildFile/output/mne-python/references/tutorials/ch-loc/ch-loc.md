# How To: Ch Loc

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test raw kit loc.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `scipy.io`
- `numpy.testing`
- `scipy`
- `mne`
- `mne`
- `mne._fiff.constants`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.kit.constants`
- `mne.io.kit.coreg`
- `mne.io.kit.kit`
- `mne.io.tests.test_raw`
- `mne.surface`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test raw kit loc.'

```python
'Test raw kit loc.'
```

**Verification:**
```python
assert_array_almost_equal(ch_py, ch_sns, 2)
```

### Step 2: Assign raw_py = read_raw_kit(...)

```python
raw_py = read_raw_kit(sqd_path, mrk_path, elp_txt_path, hsp_txt_path, stim='<')
```

**Verification:**
```python
assert_array_almost_equal(raw_py.info['dev_head_t']['trans'], raw_bin.info['dev_head_t']['trans'], 4)
```

### Step 3: Assign raw_bin = read_raw_fif(...)

```python
raw_bin = read_raw_fif(data_dir / 'test_bin_raw.fif')
```

**Verification:**
```python
assert_array_almost_equal(py_ch['loc'], bin_ch['loc'], decimal=2)
```

### Step 4: Assign ch_py = np.array(...)

```python
ch_py = np.array([ch['loc'] for ch in raw_py._raw_extras[0]['channels'][:160]])
```

**Verification:**
```python
assert_dig_allclose(raw_py.info, raw_bin.info)
```

### Step 5: Assign ch_sns = read_sns(...)

```python
ch_sns = read_sns(data_dir / 'sns.txt')
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(ch_py, ch_sns, 2)
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(raw_py.info['dev_head_t']['trans'], raw_bin.info['dev_head_t']['trans'], 4)
```

### Step 8: Assign mrks = value

```python
mrks = [mrk_path, mrk2_path, mrk3_path]
```

### Step 9: Call read_raw_kit()

```python
read_raw_kit(sqd_path, mrks, elp_txt_path, hsp_txt_path, preload=False)
```

### Step 10: Call assert_dig_allclose()

```python
assert_dig_allclose(raw_py.info, raw_bin.info)
```

### Step 11: Assign unknown = value

```python
raw_bin.info['dig'] = raw_bin.info['dig'][:8]
```

### Step 12: Assign unknown = value

```python
raw_py.info['dig'] = raw_py.info['dig'][:8]
```

### Step 13: Call assert_array_almost_equal()

```python
assert_array_almost_equal(py_ch['loc'], bin_ch['loc'], decimal=2)
```


## Complete Example

```python
# Workflow
'Test raw kit loc.'
raw_py = read_raw_kit(sqd_path, mrk_path, elp_txt_path, hsp_txt_path, stim='<')
raw_bin = read_raw_fif(data_dir / 'test_bin_raw.fif')
ch_py = np.array([ch['loc'] for ch in raw_py._raw_extras[0]['channels'][:160]])
ch_py[:, :3] *= 1000.0
ch_sns = read_sns(data_dir / 'sns.txt')
assert_array_almost_equal(ch_py, ch_sns, 2)
assert_array_almost_equal(raw_py.info['dev_head_t']['trans'], raw_bin.info['dev_head_t']['trans'], 4)
for py_ch, bin_ch in zip(raw_py.info['chs'], raw_bin.info['chs']):
    if bin_ch['ch_name'].startswith('MEG'):
        assert_array_almost_equal(py_ch['loc'], bin_ch['loc'], decimal=2)
mrks = [mrk_path, mrk2_path, mrk3_path]
read_raw_kit(sqd_path, mrks, elp_txt_path, hsp_txt_path, preload=False)
with raw_bin.info._unlock():
    raw_bin.info['dig'] = raw_bin.info['dig'][:8]
with raw_py.info._unlock():
    raw_py.info['dig'] = raw_py.info['dig'][:8]
assert_dig_allclose(raw_py.info, raw_bin.info)
```

## Next Steps


---

*Source: test_kit.py:331 | Complexity: Advanced | Last updated: 2026-05-18*