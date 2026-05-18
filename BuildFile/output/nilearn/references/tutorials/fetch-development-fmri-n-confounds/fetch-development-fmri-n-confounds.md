# How To: Fetch Development Fmri N Confounds

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: Check number of confounds returned by fetch_development_fmri.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `json`
- `re`
- `shutil`
- `tempfile`
- `uuid`
- `collections`
- `pathlib`
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `sklearn.utils`
- `nilearn._utils.data_gen`
- `nilearn._utils.helpers`
- `nilearn.datasets`
- `nilearn.datasets._utils`
- `nilearn.datasets.tests._testing`
- `nilearn.image`

**Setup Required:**
```python
# Fixtures: request_mocker
```

## Step-by-Step Guide

### Step 1: 'Check number of confounds returned by fetch_development_fmri.'

```python
'Check number of confounds returned by fetch_development_fmri.'
```

**Verification:**
```python
assert len(confounds[0]) == 15
```

### Step 2: Assign mock_participants = _mock_participants_data(...)

```python
mock_participants = _mock_participants_data()
```

**Verification:**
```python
assert len(confounds[0]) == 28
```

### Step 3: Assign unknown = _mock_development_confounds.to_csv(...)

```python
request_mocker.url_mapping['*'] = _mock_development_confounds().to_csv(index=False, sep='\t')
```

### Step 4: Assign unknown = mock_participants.to_csv(...)

```python
request_mocker.url_mapping['https://osf.io/yr3av/download'] = mock_participants.to_csv(index=False, sep='\t')
```

### Step 5: Assign data = fetch_development_fmri(...)

```python
data = fetch_development_fmri(n_subjects=2)
```

### Step 6: Assign confounds = np.genfromtxt(...)

```python
confounds = np.genfromtxt(data.confounds[0], delimiter='\t')
```

**Verification:**
```python
assert len(confounds[0]) == 15
```

### Step 7: Assign data = fetch_development_fmri(...)

```python
data = fetch_development_fmri(n_subjects=2, reduce_confounds=False)
```

### Step 8: Assign confounds = np.genfromtxt(...)

```python
confounds = np.genfromtxt(data.confounds[0], delimiter='\t')
```

**Verification:**
```python
assert len(confounds[0]) == 28
```


## Complete Example

```python
# Setup
# Fixtures: request_mocker

# Workflow
'Check number of confounds returned by fetch_development_fmri.'
mock_participants = _mock_participants_data()
request_mocker.url_mapping['*'] = _mock_development_confounds().to_csv(index=False, sep='\t')
request_mocker.url_mapping['https://osf.io/yr3av/download'] = mock_participants.to_csv(index=False, sep='\t')
data = fetch_development_fmri(n_subjects=2)
confounds = np.genfromtxt(data.confounds[0], delimiter='\t')
assert len(confounds[0]) == 15
data = fetch_development_fmri(n_subjects=2, reduce_confounds=False)
confounds = np.genfromtxt(data.confounds[0], delimiter='\t')
assert len(confounds[0]) == 28
```

## Next Steps


---

*Source: test_func.py:748 | Complexity: Advanced | Last updated: 2026-05-18*