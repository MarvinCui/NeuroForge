# How To: Sender Img

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test sender img

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
# Fixtures: request_mocker, tmp_path
```

## Step-by-Step Guide

### Step 1: Assign unknown = value

```python
request_mocker.url_mapping['*'] = generate_fake_fmri()[0]
```

**Verification:**
```python
assert img.shape == (10, 11, 12, 17)
```

### Step 2: Assign resp = requests.get(...)

```python
resp = requests.get('ftp:example.org/download')
```

### Step 3: Assign file_path = value

```python
file_path = tmp_path / 'img.nii.gz'
```

### Step 4: Call file_path.write_bytes()

```python
file_path.write_bytes(resp.content)
```

### Step 5: Assign img = image.load_img(...)

```python
img = image.load_img(str(file_path))
```

**Verification:**
```python
assert img.shape == (10, 11, 12, 17)
```


## Complete Example

```python
# Setup
# Fixtures: request_mocker, tmp_path

# Workflow
request_mocker.url_mapping['*'] = generate_fake_fmri()[0]
resp = requests.get('ftp:example.org/download')
file_path = tmp_path / 'img.nii.gz'
file_path.write_bytes(resp.content)
img = image.load_img(str(file_path))
assert img.shape == (10, 11, 12, 17)
```

## Next Steps


---

*Source: test_testing.py:129 | Complexity: Intermediate | Last updated: 2026-05-18*