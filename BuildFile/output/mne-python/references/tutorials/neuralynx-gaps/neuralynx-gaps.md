# How To: Neuralynx Gaps

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test gap detection.

## Prerequisites

**Required Modules:**
- `os`
- `ast`
- `datetime`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy.io`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.neuralynx.neuralynx`
- `mne.io.tests.test_raw`
- `neo.io`


## Step-by-Step Guide

### Step 1: 'Test gap detection.'

```python
'Test gap detection.'
```

**Verification:**
```python
assert len(raw.annotations) == n_expected_gaps, 'Wrong number of gaps detected'
```

### Step 2: Assign ignored_ncs_files = value

```python
ignored_ncs_files = ['LAHC1.ncs', 'LAHC2.ncs', 'LAHC3.ncs', 'xAIR1.ncs', 'xEKG1.ncs', 'LAHCu1.ncs']
```

**Verification:**
```python
assert (mne_y[0, :] == 0).sum() == n_expected_missing_samples, 'Number of true and inferred missing samples differ'
```

### Step 3: Assign raw = read_raw_neuralynx(...)

```python
raw = read_raw_neuralynx(fname=testing_path, preload=True, exclude_fname_patterns=ignored_ncs_files)
```

**Verification:**
```python
assert_allclose(mne_y, mat_y, rtol=1e-06, err_msg='MNE and Nlx2MatCSC.m not all close')
```

### Step 4: Assign unknown = raw.get_data(...)

```python
mne_y, _ = raw.get_data(return_times=True)
```

**Verification:**
```python
assert raw.ch_names == ['LAHC2']
```

### Step 5: Assign n_expected_gaps = 3

```python
n_expected_gaps = 3
```

### Step 6: Assign n_expected_missing_samples = 130

```python
n_expected_missing_samples = 130
```

**Verification:**
```python
assert len(raw.annotations) == n_expected_gaps, 'Wrong number of gaps detected'
```

### Step 7: Assign matchans = value

```python
matchans = ['LAHC1_3_gaps.mat', 'LAHC2_3_gaps.mat']
```

### Step 8: Assign mat_y = np.stack(...)

```python
mat_y = np.stack([_read_nlx_mat_chan_keep_gaps(os.path.join(testing_path, ch)) for ch in matchans])
```

### Step 9: Call assert_allclose()

```python
assert_allclose(mne_y, mat_y, rtol=1e-06, err_msg='MNE and Nlx2MatCSC.m not all close')
```

### Step 10: Assign raw = read_raw_neuralynx(...)

```python
raw = read_raw_neuralynx(fname=testing_path, preload=False, exclude_fname_patterns=ignored_ncs_files)
```

### Step 11: Call raw.pick()

```python
raw.pick('LAHC2')
```

**Verification:**
```python
assert raw.ch_names == ['LAHC2']
```

### Step 12: Call raw.load_data()

```python
raw.load_data()
```


## Complete Example

```python
# Workflow
'Test gap detection.'
ignored_ncs_files = ['LAHC1.ncs', 'LAHC2.ncs', 'LAHC3.ncs', 'xAIR1.ncs', 'xEKG1.ncs', 'LAHCu1.ncs']
raw = read_raw_neuralynx(fname=testing_path, preload=True, exclude_fname_patterns=ignored_ncs_files)
mne_y, _ = raw.get_data(return_times=True)
n_expected_gaps = 3
n_expected_missing_samples = 130
assert len(raw.annotations) == n_expected_gaps, 'Wrong number of gaps detected'
assert (mne_y[0, :] == 0).sum() == n_expected_missing_samples, 'Number of true and inferred missing samples differ'
matchans = ['LAHC1_3_gaps.mat', 'LAHC2_3_gaps.mat']
mat_y = np.stack([_read_nlx_mat_chan_keep_gaps(os.path.join(testing_path, ch)) for ch in matchans])
assert_allclose(mne_y, mat_y, rtol=1e-06, err_msg='MNE and Nlx2MatCSC.m not all close')
raw = read_raw_neuralynx(fname=testing_path, preload=False, exclude_fname_patterns=ignored_ncs_files)
raw.pick('LAHC2')
assert raw.ch_names == ['LAHC2']
raw.load_data()
```

## Next Steps


---

*Source: test_neuralynx.py:197 | Complexity: Advanced | Last updated: 2026-05-18*