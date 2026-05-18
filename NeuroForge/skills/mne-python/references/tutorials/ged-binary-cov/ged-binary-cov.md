# How To: Ged Binary Cov

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: Test GEDTransformer on audvis dataset with two covariances.

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

### Step 1: 'Test GEDTransformer on audvis dataset with two covariances.'

```python
'Test GEDTransformer on audvis dataset with two covariances.'
```

**Verification:**
```python
assert_allclose(actual_evals, desired_evals)
```

### Step 2: Assign event_id = dict(...)

```python
event_id = dict(aud_l=1, vis_l=3)
```

**Verification:**
```python
assert_allclose(actual_filters, desired_filters)
```

### Step 3: Assign unknown = _get_X_y(...)

```python
X, y = _get_X_y(event_id)
```

**Verification:**
```python
assert_allclose(actual_evals, desired_evals)
```

### Step 4: Assign unknown = _mock_cov_callable(...)

```python
covs, C_ref, info, rank, kwargs = _mock_cov_callable(X, y)
```

**Verification:**
```python
assert_allclose(actual_filters, desired_filters)
```

### Step 5: Assign unknown = value

```python
S, R = (covs[0], covs[1])
```

**Verification:**
```python
assert ged._subset_multi_components(name='foo') is None
```

### Step 6: Assign restr_mat = _get_restr_mat(...)

```python
restr_mat = _get_restr_mat(C_ref, info, rank)
```

### Step 7: Assign unknown = _smart_ged(...)

```python
evals, evecs = _smart_ged(S, R, restr_mat=restr_mat, R_func=None)
```

### Step 8: Assign unknown = _mock_mod_ged_callable(...)

```python
actual_evals, actual_evecs, sorter = _mock_mod_ged_callable(evals, evecs, [S, R], **kwargs)
```

### Step 9: Assign actual_filters = value

```python
actual_filters = actual_evecs.T
```

### Step 10: Assign ged = _GEDTransformer(...)

```python
ged = _GEDTransformer(n_components=4, cov_callable=_mock_cov_callable, mod_ged_callable=_mock_mod_ged_callable, restr_type='restricting')
```

### Step 11: Call ged.fit()

```python
ged.fit(X, y)
```

### Step 12: Assign desired_evals = value

```python
desired_evals = ged.evals_
```

### Step 13: Assign desired_filters = value

```python
desired_filters = ged.filters_
```

### Step 14: Call assert_allclose()

```python
assert_allclose(actual_evals, desired_evals)
```

### Step 15: Call assert_allclose()

```python
assert_allclose(actual_filters, desired_filters)
```

### Step 16: Assign unknown = value

```python
all_evals, all_evecs = (list(), list())
```

### Step 17: Assign actual_evals = np.array(...)

```python
actual_evals = np.array(all_evals)
```

### Step 18: Assign actual_filters = np.array(...)

```python
actual_filters = np.array(all_evecs)
```

### Step 19: Assign ged = _GEDTransformer(...)

```python
ged = _GEDTransformer(n_components=4, cov_callable=_mock_cov_callable, mod_ged_callable=_mock_mod_ged_callable, dec_type='multi', restr_type='restricting')
```

### Step 20: Call ged.fit()

```python
ged.fit(X, y)
```

### Step 21: Assign desired_evals = value

```python
desired_evals = ged.evals_
```

### Step 22: Assign desired_filters = value

```python
desired_filters = ged.filters_
```

### Step 23: Call assert_allclose()

```python
assert_allclose(actual_evals, desired_evals)
```

### Step 24: Call assert_allclose()

```python
assert_allclose(actual_filters, desired_filters)
```

**Verification:**
```python
assert ged._subset_multi_components(name='foo') is None
```

### Step 25: Assign S = value

```python
S = covs[i]
```

### Step 26: Assign unknown = _smart_ged(...)

```python
evals, evecs = _smart_ged(S, R, restr_mat)
```

### Step 27: Assign unknown = _mock_mod_ged_callable(...)

```python
evals, evecs, sorter = _mock_mod_ged_callable(evals, evecs, covs)
```

### Step 28: Call all_evals.append()

```python
all_evals.append(evals)
```

### Step 29: Call all_evecs.append()

```python
all_evecs.append(evecs.T)
```


## Complete Example

```python
# Workflow
'Test GEDTransformer on audvis dataset with two covariances.'
event_id = dict(aud_l=1, vis_l=3)
X, y = _get_X_y(event_id)
covs, C_ref, info, rank, kwargs = _mock_cov_callable(X, y)
S, R = (covs[0], covs[1])
restr_mat = _get_restr_mat(C_ref, info, rank)
evals, evecs = _smart_ged(S, R, restr_mat=restr_mat, R_func=None)
actual_evals, actual_evecs, sorter = _mock_mod_ged_callable(evals, evecs, [S, R], **kwargs)
actual_filters = actual_evecs.T
ged = _GEDTransformer(n_components=4, cov_callable=_mock_cov_callable, mod_ged_callable=_mock_mod_ged_callable, restr_type='restricting')
ged.fit(X, y)
desired_evals = ged.evals_
desired_filters = ged.filters_
assert_allclose(actual_evals, desired_evals)
assert_allclose(actual_filters, desired_filters)
all_evals, all_evecs = (list(), list())
for i in range(len(covs)):
    S = covs[i]
    evals, evecs = _smart_ged(S, R, restr_mat)
    evals, evecs, sorter = _mock_mod_ged_callable(evals, evecs, covs)
    all_evals.append(evals)
    all_evecs.append(evecs.T)
actual_evals = np.array(all_evals)
actual_filters = np.array(all_evecs)
ged = _GEDTransformer(n_components=4, cov_callable=_mock_cov_callable, mod_ged_callable=_mock_mod_ged_callable, dec_type='multi', restr_type='restricting')
ged.fit(X, y)
desired_evals = ged.evals_
desired_filters = ged.filters_
assert_allclose(actual_evals, desired_evals)
assert_allclose(actual_filters, desired_filters)
assert ged._subset_multi_components(name='foo') is None
```

## Next Steps


---

*Source: test_ged.py:167 | Complexity: Advanced | Last updated: 2026-05-18*