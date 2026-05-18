# How To: Dict To Archive

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test dict to archive

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

### Step 1: Assign subdir = value

```python
subdir = tmp_path / 'tmp'
```

**Verification:**
```python
assert img.shape == (10, 11, 12, 17)
```

### Step 2: Call subdir.mkdir()

```python
subdir.mkdir()
```

**Verification:**
```python
assert int.from_bytes(f.read(), byteorder='big', signed=False) == 100
```

### Step 3: Call unknown.touch()

```python
(subdir / 'labels.csv').touch()
```

**Verification:**
```python
assert f.read() == ''
```

### Step 4: Call unknown.touch()

```python
(subdir / 'img.nii.gz').touch()
```

**Verification:**
```python
assert f.read() == targz
```

### Step 5: Assign archive_spec = value

```python
archive_spec = {'empty_data': subdir, 'empty_data_path.txt': str(subdir), Path('data', 'labels.csv'): 'a,b,c', Path('data', 'img.nii.gz'): generate_fake_fmri()[0], Path('a', 'b', 'c'): 100 .to_bytes(length=1, byteorder='big', signed=False)}
```

**Verification:**
```python
assert sorted(map(Path, tarf.getnames())) == sorted([*list(map(Path, archive_spec.keys())), Path(), Path('a'), Path('a', 'b'), Path('data')])
```

### Step 6: Assign targz = dict_to_archive(...)

```python
targz = dict_to_archive(archive_spec)
```

### Step 7: Assign extract_dir = value

```python
extract_dir = tmp_path / 'extract'
```

### Step 8: Call extract_dir.mkdir()

```python
extract_dir.mkdir()
```

### Step 9: Assign archive_path = value

```python
archive_path = tmp_path / 'archive'
```

### Step 10: Assign img = image.load_img(...)

```python
img = image.load_img(str(extract_dir / 'data' / 'img.nii.gz'))
```

**Verification:**
```python
assert img.shape == (10, 11, 12, 17)
```

### Step 11: Assign zip_archive = dict_to_archive(...)

```python
zip_archive = dict_to_archive({'readme.txt': 'hello', 'archive': targz}, 'zip')
```

### Step 12: Assign from_list = list_to_archive(...)

```python
from_list = list_to_archive(archive_spec.keys())
```

### Step 13: Call f.write()

```python
f.write(targz)
```

### Step 14: Call tarf.extractall()

```python
tarf.extractall(str(extract_dir))
```

**Verification:**
```python
assert int.from_bytes(f.read(), byteorder='big', signed=False) == 100
```

### Step 15: Call f.write()

```python
f.write(zip_archive)
```

**Verification:**
```python
assert f.read() == targz
```

### Step 16: Call f.write()

```python
f.write(from_list)
```

**Verification:**
```python
assert sorted(map(Path, tarf.getnames())) == sorted([*list(map(Path, archive_spec.keys())), Path(), Path('a'), Path('a', 'b'), Path('data')])
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
subdir = tmp_path / 'tmp'
subdir.mkdir()
(subdir / 'labels.csv').touch()
(subdir / 'img.nii.gz').touch()
archive_spec = {'empty_data': subdir, 'empty_data_path.txt': str(subdir), Path('data', 'labels.csv'): 'a,b,c', Path('data', 'img.nii.gz'): generate_fake_fmri()[0], Path('a', 'b', 'c'): 100 .to_bytes(length=1, byteorder='big', signed=False)}
targz = dict_to_archive(archive_spec)
extract_dir = tmp_path / 'extract'
extract_dir.mkdir()
archive_path = tmp_path / 'archive'
with archive_path.open('wb') as f:
    f.write(targz)
with tarfile.open(str(archive_path)) as tarf:
    tarf.extractall(str(extract_dir))
img = image.load_img(str(extract_dir / 'data' / 'img.nii.gz'))
assert img.shape == (10, 11, 12, 17)
with (extract_dir / 'a' / 'b' / 'c').open('rb') as f:
    assert int.from_bytes(f.read(), byteorder='big', signed=False) == 100
with (extract_dir / 'empty_data' / 'labels.csv').open() as f:
    assert f.read() == ''
zip_archive = dict_to_archive({'readme.txt': 'hello', 'archive': targz}, 'zip')
with archive_path.open('wb') as f:
    f.write(zip_archive)
with zipfile.ZipFile(str(archive_path)) as zipf, zipf.open('archive', 'r') as f:
    assert f.read() == targz
from_list = list_to_archive(archive_spec.keys())
with archive_path.open('wb') as f:
    f.write(from_list)
with tarfile.open(str(archive_path)) as tarf:
    assert sorted(map(Path, tarf.getnames())) == sorted([*list(map(Path, archive_spec.keys())), Path(), Path('a'), Path('a', 'b'), Path('data')])
```

## Next Steps


---

*Source: test_testing.py:184 | Complexity: Advanced | Last updated: 2026-05-18*