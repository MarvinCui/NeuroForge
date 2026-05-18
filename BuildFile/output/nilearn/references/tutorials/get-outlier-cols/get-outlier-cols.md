# How To: Get Outlier Cols

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check the non-steady state columns are detached.

## Prerequisites

**Required Modules:**
- `numpy`
- `pandas`
- `pytest`
- `pandas.testing`
- `nilearn.interfaces.fmriprep.load_confounds_scrub`


## Step-by-Step Guide

### Step 1: 'Check the non-steady state columns are detached.'

```python
'Check the non-steady state columns are detached.'
```

**Verification:**
```python
assert confounds_cols == ['confound_regressor']
```

### Step 2: Assign col_names = value

```python
col_names = ['confound_regressor']
```

**Verification:**
```python
assert outlier_cols == non_steady_state
```

### Step 3: Assign non_steady_state = value

```python
non_steady_state = [f'non_steady_state_outlier{i:02d}' for i in range(3)]
```

### Step 4: Assign col_names = pd.Index(...)

```python
col_names = pd.Index(col_names)
```

### Step 5: Assign unknown = _get_outlier_cols(...)

```python
outlier_cols, confounds_cols = _get_outlier_cols(col_names)
```

**Verification:**
```python
assert confounds_cols == ['confound_regressor']
```


## Complete Example

```python
# Workflow
'Check the non-steady state columns are detached.'
col_names = ['confound_regressor']
non_steady_state = [f'non_steady_state_outlier{i:02d}' for i in range(3)]
col_names += non_steady_state
col_names = pd.Index(col_names)
outlier_cols, confounds_cols = _get_outlier_cols(col_names)
assert confounds_cols == ['confound_regressor']
assert outlier_cols == non_steady_state
```

## Next Steps


---

*Source: test_load_confounds_scrub.py:37 | Complexity: Intermediate | Last updated: 2026-05-18*