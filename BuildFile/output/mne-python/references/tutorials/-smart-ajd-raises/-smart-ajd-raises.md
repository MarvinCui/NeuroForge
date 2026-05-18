# How To:  Smart Ajd Raises

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test _smart_ajd raises proper ValueErrors.

## Prerequisites

**Required Modules:**
- `functools`
- `pathlib`
- `numpy`
- `pytest`
- `sklearn.model_selection`
- `sklearn.utils._testing`
- `sklearn.utils.estimator_checks`
- `mne`
- `mne._fiff.proj`
- `mne.cov`
- `mne.decoding._ged`
- `mne.decoding._mod_ged`
- `mne.decoding.base`
- `mne.io`


## Step-by-Step Guide

### Step 1: 'Test _smart_ajd raises proper ValueErrors.'

```python
'Test _smart_ajd raises proper ValueErrors.'
```

### Step 2: Assign asymm_indef = np.array(...)

```python
asymm_indef = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
```

### Step 3: Assign sing_pos_semidef = np.array(...)

```python
sing_pos_semidef = np.array([[1, 2, 3], [2, 4, 6], [3, 6, 9]])
```

### Step 4: Assign pos_def1 = np.array(...)

```python
pos_def1 = np.array([[5, 1, 1], [1, 6, 2], [1, 2, 7]])
```

### Step 5: Assign pos_def2 = np.array(...)

```python
pos_def2 = np.array([[10, 1, 2], [1, 12, 3], [2, 3, 15]])
```

### Step 6: Assign bad_covs = np.stack(...)

```python
bad_covs = np.stack([sing_pos_semidef, asymm_indef, pos_def1])
```

### Step 7: Assign bad_covs = np.stack(...)

```python
bad_covs = np.stack([sing_pos_semidef, pos_def1, pos_def2])
```

### Step 8: Call _smart_ajd()

```python
_smart_ajd(bad_covs, restr_mat=pos_def2, weights=None)
```

### Step 9: Call _smart_ajd()

```python
_smart_ajd(bad_covs, restr_mat=None, weights=None)
```


## Complete Example

```python
# Workflow
'Test _smart_ajd raises proper ValueErrors.'
asymm_indef = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
sing_pos_semidef = np.array([[1, 2, 3], [2, 4, 6], [3, 6, 9]])
pos_def1 = np.array([[5, 1, 1], [1, 6, 2], [1, 2, 7]])
pos_def2 = np.array([[10, 1, 2], [1, 12, 3], [2, 3, 15]])
bad_covs = np.stack([sing_pos_semidef, asymm_indef, pos_def1])
with pytest.raises(ValueError, match='positive semi-definite'):
    _smart_ajd(bad_covs, restr_mat=pos_def2, weights=None)
bad_covs = np.stack([sing_pos_semidef, pos_def1, pos_def2])
with pytest.raises(ValueError, match='positive definite'):
    _smart_ajd(bad_covs, restr_mat=None, weights=None)
```

## Next Steps


---

*Source: test_ged.py:353 | Complexity: Advanced | Last updated: 2026-05-18*