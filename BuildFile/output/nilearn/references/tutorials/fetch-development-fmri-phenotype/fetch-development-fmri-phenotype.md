# How To: Fetch Development Fmri Phenotype

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: Check phenotype returned by fetch_development_fmri.

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

### Step 1: 'Check phenotype returned by fetch_development_fmri.'

```python
'Check phenotype returned by fetch_development_fmri.'
```

**Verification:**
```python
assert age_group == 'adult'
```

### Step 2: Assign mock_participants = _mock_participants_data(...)

```python
mock_participants = _mock_participants_data()
```

**Verification:**
```python
assert all(age_group == ['adult', 'child'])
```

### Step 3: Assign unknown = _mock_development_confounds.to_csv(...)

```python
request_mocker.url_mapping['*'] = _mock_development_confounds().to_csv(index=False, sep='\t')
```

**Verification:**
```python
assert age_group == 'child'
```

### Step 4: Assign unknown = mock_participants.to_csv(...)

```python
request_mocker.url_mapping['https://osf.io/yr3av/download'] = mock_participants.to_csv(index=False, sep='\t')
```

**Verification:**
```python
assert all((x == 'child' for x in data.phenotypic['Child_Adult']))
```

### Step 5: Assign data = fetch_development_fmri(...)

```python
data = fetch_development_fmri(n_subjects=1)
```

### Step 6: Assign age_group = value

```python
age_group = data.phenotypic['Child_Adult'].to_list()[0]
```

**Verification:**
```python
assert age_group == 'adult'
```

### Step 7: Assign data = fetch_development_fmri(...)

```python
data = fetch_development_fmri(n_subjects=2, age_group='both')
```

### Step 8: Assign age_group = value

```python
age_group = data.phenotypic['Child_Adult']
```

**Verification:**
```python
assert all(age_group == ['adult', 'child'])
```

### Step 9: Assign data = fetch_development_fmri(...)

```python
data = fetch_development_fmri(n_subjects=1, age_group='child')
```

### Step 10: Assign age_group = value

```python
age_group = data.phenotypic['Child_Adult'][0]
```

**Verification:**
```python
assert age_group == 'child'
```

### Step 11: Assign data = fetch_development_fmri(...)

```python
data = fetch_development_fmri(n_subjects=2, age_group='child')
```

**Verification:**
```python
assert all((x == 'child' for x in data.phenotypic['Child_Adult']))
```


## Complete Example

```python
# Setup
# Fixtures: request_mocker

# Workflow
'Check phenotype returned by fetch_development_fmri.'
mock_participants = _mock_participants_data()
request_mocker.url_mapping['*'] = _mock_development_confounds().to_csv(index=False, sep='\t')
request_mocker.url_mapping['https://osf.io/yr3av/download'] = mock_participants.to_csv(index=False, sep='\t')
data = fetch_development_fmri(n_subjects=1)
age_group = data.phenotypic['Child_Adult'].to_list()[0]
assert age_group == 'adult'
data = fetch_development_fmri(n_subjects=2, age_group='both')
age_group = data.phenotypic['Child_Adult']
assert all(age_group == ['adult', 'child'])
data = fetch_development_fmri(n_subjects=1, age_group='child')
age_group = data.phenotypic['Child_Adult'][0]
assert age_group == 'child'
data = fetch_development_fmri(n_subjects=2, age_group='child')
assert all((x == 'child' for x in data.phenotypic['Child_Adult']))
```

## Next Steps


---

*Source: test_func.py:772 | Complexity: Advanced | Last updated: 2026-05-18*