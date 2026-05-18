# How To: Fetch Abide Pcp

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, mock, workflow, integration

## Overview

Workflow: test fetch abide pcp

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
# Fixtures: tmp_path, request_mocker, quality_checked, capsys
```

## Step-by-Step Guide

### Step 1: Assign n_subjects = 800

```python
n_subjects = 800
```

**Verification:**
```python
assert isinstance(dataset, Bunch)
```

### Step 2: Assign ids = list(...)

```python
ids = list(range(n_subjects))
```

**Verification:**
```python
assert len(dataset.func_preproc) == n_subjects / div
```

### Step 3: Assign filenames = value

```python
filenames = ['no_filename'] * n_subjects
```

### Step 4: Assign unknown = value

```python
filenames[::2] = ['filename'] * (n_subjects // 2)
```

### Step 5: Assign qc_rater_1 = value

```python
qc_rater_1 = ['OK'] * n_subjects
```

### Step 6: Assign unknown = value

```python
qc_rater_1[::4] = ['fail'] * (n_subjects // 4)
```

### Step 7: Assign pheno = pd.DataFrame(...)

```python
pheno = pd.DataFrame({'subject_id': ids, 'FILE_ID': filenames, 'qc_rater_1': qc_rater_1, 'qc_anat_rater_2': qc_rater_1, 'qc_func_rater_2': qc_rater_1, 'qc_anat_rater_3': qc_rater_1, 'qc_func_rater_3': qc_rater_1}, columns=['subject_id', 'FILE_ID', 'qc_rater_1', 'qc_anat_rater_2', 'qc_func_rater_2', 'qc_anat_rater_3', 'qc_func_rater_3'])
```

### Step 8: Assign unknown = pheno.to_csv(...)

```python
request_mocker.url_mapping['*rocessed1.csv'] = pheno.to_csv(index=False)
```

### Step 9: Assign dataset = func.fetch_abide_pcp(...)

```python
dataset = func.fetch_abide_pcp(data_dir=tmp_path, quality_checked=quality_checked, verbose=0)
```

### Step 10: Assign div = value

```python
div = 4 if quality_checked else 2
```

**Verification:**
```python
assert isinstance(dataset, Bunch)
```

### Step 11: Call check_type_fetcher()

```python
check_type_fetcher(dataset)
```

**Verification:**
```python
assert len(dataset.func_preproc) == n_subjects / div
```

### Step 12: Assign dataset = func.fetch_abide_pcp(...)

```python
dataset = func.fetch_abide_pcp(data_dir=tmp_path, quality_checked=quality_checked, verbose=0, derivatives='func_preproc')
```

### Step 13: Call check_fetcher_verbosity()

```python
check_fetcher_verbosity(func.fetch_abide_pcp, capsys, data_dir=tmp_path, quality_checked=quality_checked, derivatives='func_preproc')
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, request_mocker, quality_checked, capsys

# Workflow
n_subjects = 800
ids = list(range(n_subjects))
filenames = ['no_filename'] * n_subjects
filenames[::2] = ['filename'] * (n_subjects // 2)
qc_rater_1 = ['OK'] * n_subjects
qc_rater_1[::4] = ['fail'] * (n_subjects // 4)
pheno = pd.DataFrame({'subject_id': ids, 'FILE_ID': filenames, 'qc_rater_1': qc_rater_1, 'qc_anat_rater_2': qc_rater_1, 'qc_func_rater_2': qc_rater_1, 'qc_anat_rater_3': qc_rater_1, 'qc_func_rater_3': qc_rater_1}, columns=['subject_id', 'FILE_ID', 'qc_rater_1', 'qc_anat_rater_2', 'qc_func_rater_2', 'qc_anat_rater_3', 'qc_func_rater_3'])
request_mocker.url_mapping['*rocessed1.csv'] = pheno.to_csv(index=False)
dataset = func.fetch_abide_pcp(data_dir=tmp_path, quality_checked=quality_checked, verbose=0)
div = 4 if quality_checked else 2
assert isinstance(dataset, Bunch)
check_type_fetcher(dataset)
assert len(dataset.func_preproc) == n_subjects / div
dataset = func.fetch_abide_pcp(data_dir=tmp_path, quality_checked=quality_checked, verbose=0, derivatives='func_preproc')
check_fetcher_verbosity(func.fetch_abide_pcp, capsys, data_dir=tmp_path, quality_checked=quality_checked, derivatives='func_preproc')
```

## Next Steps


---

*Source: test_func.py:426 | Complexity: Advanced | Last updated: 2026-05-18*