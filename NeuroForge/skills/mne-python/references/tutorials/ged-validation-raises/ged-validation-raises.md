# How To: Ged Validation Raises

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: Test GEDTransofmer validation raises correct errors.

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

### Step 1: 'Test GEDTransofmer validation raises correct errors.'

```python
'Test GEDTransofmer validation raises correct errors.'
```

### Step 2: Assign event_id = dict(...)

```python
event_id = dict(aud_l=1, vis_l=3)
```

### Step 3: Assign unknown = _get_X_y(...)

```python
X, y = _get_X_y(event_id)
```

### Step 4: Assign ged = _GEDTransformer(...)

```python
ged = _GEDTransformer(n_components=-1, cov_callable=_mock_cov_callable, mod_ged_callable=_mock_mod_ged_callable, restr_type='restricting')
```

### Step 5: Assign ged = _GEDTransformer(...)

```python
ged = _GEDTransformer(n_components=1, cov_callable=_bad_cov_callable, mod_ged_callable=_mock_mod_ged_callable, restr_type='restricting')
```

### Step 6: Call ged.fit()

```python
ged.fit(X, y)
```

### Step 7: Call ged.fit()

```python
ged.fit(X, y)
```


## Complete Example

```python
# Workflow
'Test GEDTransofmer validation raises correct errors.'
event_id = dict(aud_l=1, vis_l=3)
X, y = _get_X_y(event_id)
ged = _GEDTransformer(n_components=-1, cov_callable=_mock_cov_callable, mod_ged_callable=_mock_mod_ged_callable, restr_type='restricting')
with pytest.raises(ValueError):
    ged.fit(X, y)

def _bad_cov_callable(X, y, foo):
    return (X, y, foo)
ged = _GEDTransformer(n_components=1, cov_callable=_bad_cov_callable, mod_ged_callable=_mock_mod_ged_callable, restr_type='restricting')
with pytest.raises(ValueError):
    ged.fit(X, y)
```

## Next Steps


---

*Source: test_ged.py:295 | Complexity: Intermediate | Last updated: 2026-05-18*