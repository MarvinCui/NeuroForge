# How To: Fetch Language Localizer Demo Dataset

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test fetch language localizer demo dataset

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
# Fixtures: tmp_path, capsys
```

## Step-by-Step Guide

### Step 1: Assign data_dir = tmp_path

```python
data_dir = tmp_path
```

**Verification:**
```python
assert isinstance(bunch, Bunch)
```

### Step 2: Assign expected_data_dir = value

```python
expected_data_dir = tmp_path / 'fMRI-language-localizer-demo-dataset'
```

**Verification:**
```python
assert bunch.data_dir == str(expected_data_dir)
```

### Step 3: Assign contents_dir = value

```python
contents_dir = Path(__file__).parent / 'data' / 'archive_contents'
```

**Verification:**
```python
assert bunch.func == sorted(expected_files)
```

### Step 4: Assign contents_list_file = value

```python
contents_list_file = contents_dir / 'language_localizer.txt'
```

### Step 5: Assign bunch = func.fetch_language_localizer_demo_dataset(...)

```python
bunch = func.fetch_language_localizer_demo_dataset(data_dir)
```

**Verification:**
```python
assert isinstance(bunch, Bunch)
```

### Step 6: Call check_type_fetcher()

```python
check_type_fetcher(bunch)
```

**Verification:**
```python
assert bunch.data_dir == str(expected_data_dir)
```

### Step 7: Call check_fetcher_verbosity()

```python
check_fetcher_verbosity(func.fetch_language_localizer_demo_dataset, capsys, data_dir=tmp_path)
```

### Step 8: Assign expected_files = value

```python
expected_files = [str(expected_data_dir / file_path.strip()) for file_path in f.readlines()[1:]]
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, capsys

# Workflow
data_dir = tmp_path
expected_data_dir = tmp_path / 'fMRI-language-localizer-demo-dataset'
contents_dir = Path(__file__).parent / 'data' / 'archive_contents'
contents_list_file = contents_dir / 'language_localizer.txt'
with contents_list_file.open() as f:
    expected_files = [str(expected_data_dir / file_path.strip()) for file_path in f.readlines()[1:]]
bunch = func.fetch_language_localizer_demo_dataset(data_dir)
assert isinstance(bunch, Bunch)
check_type_fetcher(bunch)
assert bunch.data_dir == str(expected_data_dir)
assert bunch.func == sorted(expected_files)
check_fetcher_verbosity(func.fetch_language_localizer_demo_dataset, capsys, data_dir=tmp_path)
```

## Next Steps


---

*Source: test_func.py:976 | Complexity: Advanced | Last updated: 2026-05-18*