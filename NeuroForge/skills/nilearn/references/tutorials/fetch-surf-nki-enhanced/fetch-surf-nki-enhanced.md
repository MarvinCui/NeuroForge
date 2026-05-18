# How To: Fetch Surf Nki Enhanced

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test fetch surf nki enhanced

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

### Step 1: Assign ids = np.asarray(...)

```python
ids = np.asarray(['A00028185', 'A00035827', 'A00037511', 'A00039431', 'A00033747', 'A00035840', 'A00038998', 'A00035072', 'A00037112', 'A00039391'], dtype='U9')
```

**Verification:**
```python
assert isinstance(nki_data, Bunch)
```

### Step 2: Assign age = np.ones(...)

```python
age = np.ones(len(ids), dtype='<f8')
```

**Verification:**
```python
assert len(nki_data.func_left) == 10
```

### Step 3: Assign hand = np.asarray(...)

```python
hand = np.asarray(len(ids) * ['x'], dtype='U1')
```

**Verification:**
```python
assert len(nki_data.func_right) == 10
```

### Step 4: Assign sex = np.asarray(...)

```python
sex = np.asarray(len(ids) * ['x'], dtype='U1')
```

**Verification:**
```python
assert isinstance(nki_data.phenotypic, pd.DataFrame)
```

### Step 5: Assign pheno_data = pd.DataFrame(...)

```python
pheno_data = pd.DataFrame(OrderedDict([('id', ids), ('age', age), ('hand', hand), ('sex', sex)]))
```

**Verification:**
```python
assert nki_data.phenotypic.shape == (9, 4)
```

### Step 6: Assign unknown = pheno_data.to_csv(...)

```python
request_mocker.url_mapping['*pheno_nki_nilearn.csv'] = pheno_data.to_csv(index=False)
```

### Step 7: Assign nki_data = func.fetch_surf_nki_enhanced(...)

```python
nki_data = func.fetch_surf_nki_enhanced(data_dir=tmp_path)
```

**Verification:**
```python
assert isinstance(nki_data, Bunch)
```

### Step 8: Call check_type_fetcher()

```python
check_type_fetcher(nki_data)
```

**Verification:**
```python
assert len(nki_data.func_left) == 10
```

### Step 9: Call check_fetcher_verbosity()

```python
check_fetcher_verbosity(func.fetch_surf_nki_enhanced, capsys, data_dir=tmp_path)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, request_mocker, capsys

# Workflow
ids = np.asarray(['A00028185', 'A00035827', 'A00037511', 'A00039431', 'A00033747', 'A00035840', 'A00038998', 'A00035072', 'A00037112', 'A00039391'], dtype='U9')
age = np.ones(len(ids), dtype='<f8')
hand = np.asarray(len(ids) * ['x'], dtype='U1')
sex = np.asarray(len(ids) * ['x'], dtype='U1')
pheno_data = pd.DataFrame(OrderedDict([('id', ids), ('age', age), ('hand', hand), ('sex', sex)]))
request_mocker.url_mapping['*pheno_nki_nilearn.csv'] = pheno_data.to_csv(index=False)
nki_data = func.fetch_surf_nki_enhanced(data_dir=tmp_path)
assert isinstance(nki_data, Bunch)
check_type_fetcher(nki_data)
assert len(nki_data.func_left) == 10
assert len(nki_data.func_right) == 10
assert isinstance(nki_data.phenotypic, pd.DataFrame)
assert nki_data.phenotypic.shape == (9, 4)
check_fetcher_verbosity(func.fetch_surf_nki_enhanced, capsys, data_dir=tmp_path)
```

## Next Steps


---

*Source: test_func.py:601 | Complexity: Advanced | Last updated: 2026-05-18*