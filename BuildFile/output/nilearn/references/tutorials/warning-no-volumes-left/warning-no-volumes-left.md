# How To: Warning No Volumes Left

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check warning is thrown when all volumes in a run are scrubbed.

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
# Fixtures: outlier_type
```

## Step-by-Step Guide

### Step 1: 'Check warning is thrown when all volumes in a run are scrubbed.'

```python
'Check warning is thrown when all volumes in a run are scrubbed.'
```

**Verification:**
```python
assert sample_mask.size == 0
```

### Step 2: Assign rng = np.random.default_rng(...)

```python
rng = np.random.default_rng()
```

### Step 3: Assign n_scans = 10

```python
n_scans = 10
```

### Step 4: Assign fake_confounds = pd.DataFrame(...)

```python
fake_confounds = pd.DataFrame(rng.random((n_scans, 1)), columns=['confound_regressor'])
```

### Step 5: Assign idx_scrubbed = np.arange(...)

```python
idx_scrubbed = np.arange(n_scans)
```

### Step 6: Assign scrub_vol = pd.DataFrame(...)

```python
scrub_vol = pd.DataFrame(np.eye(n_scans)[:, idx_scrubbed], columns=[f'{outlier_type}{i:02d}' for i in range(len(idx_scrubbed))])
```

### Step 7: Assign srub_conf = pd.concat(...)

```python
srub_conf = pd.concat([fake_confounds, scrub_vol], axis=1)
```

### Step 8: Assign unknown = extract_outlier_regressors(...)

```python
sample_mask, _, _ = extract_outlier_regressors(srub_conf)
```

**Verification:**
```python
assert sample_mask.size == 0
```


## Complete Example

```python
# Setup
# Fixtures: outlier_type

# Workflow
'Check warning is thrown when all volumes in a run are scrubbed.'
rng = np.random.default_rng()
n_scans = 10
fake_confounds = pd.DataFrame(rng.random((n_scans, 1)), columns=['confound_regressor'])
idx_scrubbed = np.arange(n_scans)
scrub_vol = pd.DataFrame(np.eye(n_scans)[:, idx_scrubbed], columns=[f'{outlier_type}{i:02d}' for i in range(len(idx_scrubbed))])
srub_conf = pd.concat([fake_confounds, scrub_vol], axis=1)
with pytest.warns(RuntimeWarning, match='All volumes were marked as motion outliers.'):
    sample_mask, _, _ = extract_outlier_regressors(srub_conf)
    assert sample_mask.size == 0
```

## Next Steps


---

*Source: test_load_confounds_scrub.py:105 | Complexity: Advanced | Last updated: 2026-05-18*