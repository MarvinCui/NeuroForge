# How To: Loading From Archive Contents

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test loading from archive contents

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `re`
- `tarfile`
- `zipfile`
- `pathlib`
- `pytest`
- `requests`
- `nilearn`
- `nilearn._utils.data_gen`
- `nilearn.datasets.tests._testing`
- `nilearn.datasets.tests.conftest`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: Assign expected_contents = sorted(...)

```python
expected_contents = sorted([Path('README.txt'), Path('data'), Path('data', 'img.nii.gz'), Path('data', 'labels.csv')])
```

**Verification:**
```python
assert sorted(map(Path, zipf.namelist())) == expected_contents
```

### Step 2: Assign resp = requests.get(...)

```python
resp = requests.get('https://example.org/example_zip')
```

**Verification:**
```python
assert labels_file.read_bytes() == b''
```

### Step 3: Assign file_path = value

```python
file_path = tmp_path / 'archive.zip'
```

**Verification:**
```python
assert sorted(map(Path, tarf.getnames())) == [Path(), *expected_contents]
```

### Step 4: Call file_path.write_bytes()

```python
file_path.write_bytes(resp.content)
```

**Verification:**
```python
assert labels_file.read_bytes() == b''
```

### Step 5: Assign zip_extract_dir = value

```python
zip_extract_dir = tmp_path / 'extract_zip'
```

### Step 6: Call zip_extract_dir.mkdir()

```python
zip_extract_dir.mkdir()
```

### Step 7: Assign labels_file = value

```python
labels_file = zip_extract_dir / 'data' / 'labels.csv'
```

**Verification:**
```python
assert labels_file.read_bytes() == b''
```

### Step 8: Call zipf.extractall()

```python
zipf.extractall(str(zip_extract_dir))
```

### Step 9: Assign resp = requests.get(...)

```python
resp = requests.get(f'https://example.org/example{url_end}')
```

### Step 10: Assign file_path = value

```python
file_path = tmp_path / 'archive.tar.gz'
```

### Step 11: Call file_path.write_bytes()

```python
file_path.write_bytes(resp.content)
```

### Step 12: Assign tar_extract_dir = value

```python
tar_extract_dir = tmp_path / f'extract_tar{url_end}'
```

### Step 13: Call tar_extract_dir.mkdir()

```python
tar_extract_dir.mkdir()
```

### Step 14: Assign labels_file = value

```python
labels_file = tar_extract_dir / 'data' / 'labels.csv'
```

**Verification:**
```python
assert labels_file.read_bytes() == b''
```

### Step 15: Call tarf.extractall()

```python
tarf.extractall(str(tar_extract_dir))
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
expected_contents = sorted([Path('README.txt'), Path('data'), Path('data', 'img.nii.gz'), Path('data', 'labels.csv')])
resp = requests.get('https://example.org/example_zip')
file_path = tmp_path / 'archive.zip'
file_path.write_bytes(resp.content)
zip_extract_dir = tmp_path / 'extract_zip'
zip_extract_dir.mkdir()
with zipfile.ZipFile(str(file_path)) as zipf:
    assert sorted(map(Path, zipf.namelist())) == expected_contents
    zipf.extractall(str(zip_extract_dir))
labels_file = zip_extract_dir / 'data' / 'labels.csv'
assert labels_file.read_bytes() == b''
for url_end in ['_default_format', '_tar_gz']:
    resp = requests.get(f'https://example.org/example{url_end}')
    file_path = tmp_path / 'archive.tar.gz'
    file_path.write_bytes(resp.content)
    tar_extract_dir = tmp_path / f'extract_tar{url_end}'
    tar_extract_dir.mkdir()
    with tarfile.open(str(file_path)) as tarf:
        assert sorted(map(Path, tarf.getnames())) == [Path(), *expected_contents]
        tarf.extractall(str(tar_extract_dir))
    labels_file = tar_extract_dir / 'data' / 'labels.csv'
    assert labels_file.read_bytes() == b''
```

## Next Steps


---

*Source: test_testing.py:33 | Complexity: Advanced | Last updated: 2026-05-18*