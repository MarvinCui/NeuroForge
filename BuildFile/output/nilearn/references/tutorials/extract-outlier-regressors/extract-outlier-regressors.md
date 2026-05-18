# How To: Extract Outlier Regressors

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check outlier regressors of different types.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pandas`
- `pytest`
- `pandas.testing`
- `nilearn.interfaces.fmriprep.load_confounds_scrub`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: 'Check outlier regressors of different types.'

```python
'Check outlier regressors of different types.'
```

**Verification:**
```python
assert np.array_equal(sample_mask, np.arange(n_scans)[3:]) is True
```

### Step 2: Assign n_scans = 50

```python
n_scans = 50
```

**Verification:**
```python
assert_frame_equal(outliers, non_steady_vol)
```

### Step 3: Assign fake_confounds = pd.DataFrame(...)

```python
fake_confounds = pd.DataFrame(rng.random((n_scans, 1)), columns=['confound_regressor'])
```

**Verification:**
```python
assert_frame_equal(confounds, fake_confounds)
```

### Step 4: Assign idx_scrubbed = value

```python
idx_scrubbed = [2, 4, 34, 44]
```

**Verification:**
```python
assert np.array_equal(sample_mask, make_mask) is True
```

### Step 5: Assign scrub_vol = pd.DataFrame(...)

```python
scrub_vol = pd.DataFrame(np.eye(n_scans)[:, idx_scrubbed], columns=[f'motion_outlier{i:02d}' for i in range(len(idx_scrubbed))])
```

**Verification:**
```python
assert_frame_equal(outliers, scrub_vol)
```

### Step 6: Assign non_steady_vol = pd.DataFrame(...)

```python
non_steady_vol = pd.DataFrame(np.eye(n_scans)[:, :3], columns=[f'non_steady_state_outlier{i:02d}' for i in range(3)])
```

**Verification:**
```python
assert_frame_equal(confounds, fake_confounds)
```

### Step 7: Assign non_steady_conf = pd.concat(...)

```python
non_steady_conf = pd.concat([fake_confounds, non_steady_vol], axis=1)
```

**Verification:**
```python
assert len(sample_mask) == 44
```

### Step 8: Assign unknown = extract_outlier_regressors(...)

```python
sample_mask, confounds, outliers = extract_outlier_regressors(non_steady_conf)
```

**Verification:**
```python
assert np.array_equal(sample_mask, make_mask) is True
```

### Step 9: Call assert_frame_equal()

```python
assert_frame_equal(outliers, non_steady_vol)
```

**Verification:**
```python
assert_frame_equal(outliers, make_outliers)
```

### Step 10: Call assert_frame_equal()

```python
assert_frame_equal(confounds, fake_confounds)
```

**Verification:**
```python
assert_frame_equal(confounds, fake_confounds)
```

### Step 11: Assign srub_conf = pd.concat(...)

```python
srub_conf = pd.concat([fake_confounds, scrub_vol], axis=1)
```

### Step 12: Assign make_mask = np.delete(...)

```python
make_mask = np.delete(np.arange(n_scans), idx_scrubbed)
```

### Step 13: Assign unknown = extract_outlier_regressors(...)

```python
sample_mask, confounds, outliers = extract_outlier_regressors(srub_conf)
```

**Verification:**
```python
assert np.array_equal(sample_mask, make_mask) is True
```

### Step 14: Call assert_frame_equal()

```python
assert_frame_equal(outliers, scrub_vol)
```

### Step 15: Call assert_frame_equal()

```python
assert_frame_equal(confounds, fake_confounds)
```

### Step 16: Assign all_conf = pd.concat(...)

```python
all_conf = pd.concat([fake_confounds, non_steady_vol, scrub_vol], axis=1)
```

### Step 17: Assign make_mask = value

```python
make_mask = np.delete(np.arange(n_scans), idx_scrubbed)[2:]
```

### Step 18: Assign make_outliers = pd.concat(...)

```python
make_outliers = pd.concat([non_steady_vol, scrub_vol], axis=1)
```

### Step 19: Assign make_outliers = make_outliers.reindex(...)

```python
make_outliers = make_outliers.reindex(sorted(make_outliers.columns), axis=1)
```

### Step 20: Assign make_outliers = make_outliers.drop(...)

```python
make_outliers = make_outliers.drop(columns='non_steady_state_outlier02')
```

### Step 21: Assign unknown = extract_outlier_regressors(...)

```python
sample_mask, confounds, outliers = extract_outlier_regressors(all_conf)
```

**Verification:**
```python
assert len(sample_mask) == 44
```

### Step 22: Call assert_frame_equal()

```python
assert_frame_equal(outliers, make_outliers)
```

### Step 23: Call assert_frame_equal()

```python
assert_frame_equal(confounds, fake_confounds)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'Check outlier regressors of different types.'
n_scans = 50
fake_confounds = pd.DataFrame(rng.random((n_scans, 1)), columns=['confound_regressor'])
idx_scrubbed = [2, 4, 34, 44]
scrub_vol = pd.DataFrame(np.eye(n_scans)[:, idx_scrubbed], columns=[f'motion_outlier{i:02d}' for i in range(len(idx_scrubbed))])
non_steady_vol = pd.DataFrame(np.eye(n_scans)[:, :3], columns=[f'non_steady_state_outlier{i:02d}' for i in range(3)])
non_steady_conf = pd.concat([fake_confounds, non_steady_vol], axis=1)
sample_mask, confounds, outliers = extract_outlier_regressors(non_steady_conf)
assert np.array_equal(sample_mask, np.arange(n_scans)[3:]) is True
assert_frame_equal(outliers, non_steady_vol)
assert_frame_equal(confounds, fake_confounds)
srub_conf = pd.concat([fake_confounds, scrub_vol], axis=1)
make_mask = np.delete(np.arange(n_scans), idx_scrubbed)
sample_mask, confounds, outliers = extract_outlier_regressors(srub_conf)
assert np.array_equal(sample_mask, make_mask) is True
assert_frame_equal(outliers, scrub_vol)
assert_frame_equal(confounds, fake_confounds)
all_conf = pd.concat([fake_confounds, non_steady_vol, scrub_vol], axis=1)
make_mask = np.delete(np.arange(n_scans), idx_scrubbed)[2:]
make_outliers = pd.concat([non_steady_vol, scrub_vol], axis=1)
make_outliers = make_outliers.reindex(sorted(make_outliers.columns), axis=1)
make_outliers = make_outliers.drop(columns='non_steady_state_outlier02')
sample_mask, confounds, outliers = extract_outlier_regressors(all_conf)
assert len(sample_mask) == 44
assert np.array_equal(sample_mask, make_mask) is True
assert_frame_equal(outliers, make_outliers)
assert_frame_equal(confounds, fake_confounds)
```

## Next Steps


---

*Source: test_load_confounds_scrub.py:48 | Complexity: Advanced | Last updated: 2026-05-18*