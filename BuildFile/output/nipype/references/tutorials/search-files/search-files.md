# How To: Search Files

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test search files

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pytest`
- `nipype.interfaces`

**Setup Required:**
```python
# Fixtures: tmp_path, fname, extension, search_crop
```

## Step-by-Step Guide

### Step 1: Assign tmp_fname = value

```python
tmp_fname = fname + extension
```

**Verification:**
```python
assert f in (str(test_cropped_file), str(test_file))
```

### Step 2: Assign test_file = value

```python
test_file = tmp_path / tmp_fname
```

**Verification:**
```python
assert str(test_file) == f
```

### Step 3: Call test_file.touch()

```python
test_file.touch()
```

### Step 4: Assign actual_files_list = dcm2nii.search_files(...)

```python
actual_files_list = dcm2nii.search_files(str(tmp_path / fname), [extension], search_crop)
```

### Step 5: Assign tmp_cropped_fname = value

```python
tmp_cropped_fname = fname + '_Crop_1' + extension
```

### Step 6: Assign test_cropped_file = value

```python
test_cropped_file = tmp_path / tmp_cropped_fname
```

### Step 7: Call test_cropped_file.touch()

```python
test_cropped_file.touch()
```

**Verification:**
```python
assert f in (str(test_cropped_file), str(test_file))
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, fname, extension, search_crop

# Workflow
tmp_fname = fname + extension
test_file = tmp_path / tmp_fname
test_file.touch()
if search_crop:
    tmp_cropped_fname = fname + '_Crop_1' + extension
    test_cropped_file = tmp_path / tmp_cropped_fname
    test_cropped_file.touch()
actual_files_list = dcm2nii.search_files(str(tmp_path / fname), [extension], search_crop)
for f in actual_files_list:
    if search_crop:
        assert f in (str(test_cropped_file), str(test_file))
    else:
        assert str(test_file) == f
```

## Next Steps


---

*Source: test_dcm2nii.py:16 | Complexity: Intermediate | Last updated: 2026-05-18*