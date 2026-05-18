# How To: Hsp Elp

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test KIT usage of *.elp and *.hsp files against *.txt files.

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

### Step 1: 'Test KIT usage of *.elp and *.hsp files against *.txt files.'

```python
'Test KIT usage of *.elp and *.hsp files against *.txt files.'
```

**Verification:**
```python
assert_array_almost_equal(pts_elp, pts_txt, decimal=5)
```

### Step 2: Assign raw_txt = read_raw_kit(...)

```python
raw_txt = read_raw_kit(sqd_path, mrk_path, elp_txt_path, hsp_txt_path)
```

**Verification:**
```python
assert_array_almost_equal(trans_elp, trans_txt, decimal=5)
```

### Step 3: Assign raw_elp = read_raw_kit(...)

```python
raw_elp = read_raw_kit(sqd_path, mrk_path, elp_path, hsp_path)
```

**Verification:**
```python
assert_array_almost_equal(pts_elp_in_dev, pts_txt_in_dev, decimal=5)
```

### Step 4: Assign pts_txt = np.array(...)

```python
pts_txt = np.array([dig_point['r'] for dig_point in raw_txt.info['dig']])
```

### Step 5: Assign pts_elp = np.array(...)

```python
pts_elp = np.array([dig_point['r'] for dig_point in raw_elp.info['dig']])
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(pts_elp, pts_txt, decimal=5)
```

### Step 7: Assign trans_txt = value

```python
trans_txt = raw_txt.info['dev_head_t']['trans']
```

### Step 8: Assign trans_elp = value

```python
trans_elp = raw_elp.info['dev_head_t']['trans']
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(trans_elp, trans_txt, decimal=5)
```

### Step 10: Assign pts_txt_in_dev = apply_trans(...)

```python
pts_txt_in_dev = apply_trans(linalg.inv(trans_txt), pts_txt)
```

### Step 11: Assign pts_elp_in_dev = apply_trans(...)

```python
pts_elp_in_dev = apply_trans(linalg.inv(trans_elp), pts_elp)
```

### Step 12: Call assert_array_almost_equal()

```python
assert_array_almost_equal(pts_elp_in_dev, pts_txt_in_dev, decimal=5)
```


## Complete Example

```python
# Workflow
'Test KIT usage of *.elp and *.hsp files against *.txt files.'
raw_txt = read_raw_kit(sqd_path, mrk_path, elp_txt_path, hsp_txt_path)
raw_elp = read_raw_kit(sqd_path, mrk_path, elp_path, hsp_path)
pts_txt = np.array([dig_point['r'] for dig_point in raw_txt.info['dig']])
pts_elp = np.array([dig_point['r'] for dig_point in raw_elp.info['dig']])
assert_array_almost_equal(pts_elp, pts_txt, decimal=5)
trans_txt = raw_txt.info['dev_head_t']['trans']
trans_elp = raw_elp.info['dev_head_t']['trans']
assert_array_almost_equal(trans_elp, trans_txt, decimal=5)
pts_txt_in_dev = apply_trans(linalg.inv(trans_txt), pts_txt)
pts_elp_in_dev = apply_trans(linalg.inv(trans_elp), pts_elp)
assert_array_almost_equal(pts_elp_in_dev, pts_txt_in_dev, decimal=5)
```

## Next Steps


---

*Source: test_kit.py:361 | Complexity: Advanced | Last updated: 2026-05-18*