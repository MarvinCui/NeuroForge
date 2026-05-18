# How To: Fetch Development Fmri

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: Test for fetch_development_fmri.

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
# Fixtures: tmp_path, request_mocker, capsys
```

## Step-by-Step Guide

### Step 1: 'Test for fetch_development_fmri.'

```python
'Test for fetch_development_fmri.'
```

**Verification:**
```python
assert isinstance(data, Bunch)
```

### Step 2: Assign mock_participants = _mock_participants_data(...)

```python
mock_participants = _mock_participants_data()
```

**Verification:**
```python
assert len(data.func) == 2
```

### Step 3: Assign unknown = _mock_development_confounds.to_csv(...)

```python
request_mocker.url_mapping['*'] = _mock_development_confounds().to_csv(index=False, sep='\t')
```

**Verification:**
```python
assert len(data.confounds) == 2
```

### Step 4: Assign unknown = mock_participants.to_csv(...)

```python
request_mocker.url_mapping['https://osf.io/yr3av/download'] = mock_participants.to_csv(index=False, sep='\t')
```

**Verification:**
```python
assert isinstance(data.phenotypic, pd.DataFrame)
```

### Step 5: Assign data = fetch_development_fmri(...)

```python
data = fetch_development_fmri(n_subjects=2, data_dir=tmp_path)
```

**Verification:**
```python
assert data.phenotypic.shape == (2, 6)
```

### Step 6: Call check_type_fetcher()

```python
check_type_fetcher(data)
```

**Verification:**
```python
assert len(data.func) == 2
```

### Step 7: Call check_fetcher_verbosity()

```python
check_fetcher_verbosity(func.fetch_development_fmri, capsys, n_subjects=1, data_dir=tmp_path)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, request_mocker, capsys

# Workflow
'Test for fetch_development_fmri.'
mock_participants = _mock_participants_data()
request_mocker.url_mapping['*'] = _mock_development_confounds().to_csv(index=False, sep='\t')
request_mocker.url_mapping['https://osf.io/yr3av/download'] = mock_participants.to_csv(index=False, sep='\t')
data = fetch_development_fmri(n_subjects=2, data_dir=tmp_path)
assert isinstance(data, Bunch)
check_type_fetcher(data)
assert len(data.func) == 2
assert len(data.confounds) == 2
assert isinstance(data.phenotypic, pd.DataFrame)
assert data.phenotypic.shape == (2, 6)
check_fetcher_verbosity(func.fetch_development_fmri, capsys, n_subjects=1, data_dir=tmp_path)
```

## Next Steps


---

*Source: test_func.py:724 | Complexity: Intermediate | Last updated: 2026-05-18*