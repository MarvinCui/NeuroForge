# How To: Repr Niimgs Force Long Names

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test repr_niimgs without shortening.

## Prerequisites

**Required Modules:**
- `os`
- `warnings`
- `pathlib`
- `tempfile`
- `joblib`
- `numpy`
- `pytest`
- `nibabel`
- `nilearn._utils.niimg`
- `nilearn._utils.testing`
- `nilearn.image`


## Step-by-Step Guide

### Step 1: 'Test repr_niimgs without shortening.'

```python
'Test repr_niimgs without shortening.'
```

**Verification:**
```python
assert repr_niimgs(long_name, shorten=False) == long_name
```

### Step 2: Assign long_name = 'this-is-a-very-long-name-for-a-nifti-file.nii'

```python
long_name = 'this-is-a-very-long-name-for-a-nifti-file.nii'
```

**Verification:**
```python
assert repr_niimgs(['test', 'retest']) == '[test, retest]'
```

### Step 3: Assign list_of_size_3 = value

```python
list_of_size_3 = ['this-is-a-very-long-name-for-a-nifti-file.nii', 'this-is-another-very-long-name-for-a-nifti-file.nii', 'this-is-again-another-very-long-name-for-a-nifti-file.nii']
```

**Verification:**
```python
assert repr_niimgs(['test', 'retest'], shorten=False) == '[test, retest]'
```

### Step 4: Assign long_rep_list_of_size_3 = '[this-is-a-very-long-name-for-a-nifti-file.nii, this-is-another-very-long-name-for-a-nifti-file.nii, this-is-again-another-very-long-name-for-a-nifti-file.nii]'

```python
long_rep_list_of_size_3 = '[this-is-a-very-long-name-for-a-nifti-file.nii, this-is-another-very-long-name-for-a-nifti-file.nii, this-is-again-another-very-long-name-for-a-nifti-file.nii]'
```

**Verification:**
```python
assert repr_niimgs(list_of_size_3, shorten=False) == long_rep_list_of_size_3
```

### Step 5: Assign long_list_small_names = value

```python
long_list_small_names = ['test', 'retest', 'reretest', 'rereretest']
```

**Verification:**
```python
assert repr_niimgs(long_list_small_names, shorten=False) == long_rep_long_list_small_names
```

### Step 6: Assign long_rep_long_list_small_names = '[test,\n retest,\n reretest,\n rereretest]'

```python
long_rep_long_list_small_names = '[test,\n retest,\n reretest,\n rereretest]'
```

**Verification:**
```python
assert repr_niimgs(list_of_size_4, shorten=False) == long_rep_long_list_long_names
```

### Step 7: Assign list_of_size_4 = value

```python
list_of_size_4 = [*list_of_size_3, 'this-is-again-another-super-very-long-name-for-a-nifti-file.nii']
```

### Step 8: Assign long_rep_long_list_long_names = value

```python
long_rep_long_list_long_names = long_rep_list_of_size_3[:-1].replace(',', ',\n') + ',\n ' + 'this-is-again-another-super-very-long-name-for-a-nifti-file.nii]'
```

**Verification:**
```python
assert repr_niimgs(list_of_size_4, shorten=False) == long_rep_long_list_long_names
```


## Complete Example

```python
# Workflow
'Test repr_niimgs without shortening.'
long_name = 'this-is-a-very-long-name-for-a-nifti-file.nii'
assert repr_niimgs(long_name, shorten=False) == long_name
assert repr_niimgs(['test', 'retest']) == '[test, retest]'
assert repr_niimgs(['test', 'retest'], shorten=False) == '[test, retest]'
list_of_size_3 = ['this-is-a-very-long-name-for-a-nifti-file.nii', 'this-is-another-very-long-name-for-a-nifti-file.nii', 'this-is-again-another-very-long-name-for-a-nifti-file.nii']
long_rep_list_of_size_3 = '[this-is-a-very-long-name-for-a-nifti-file.nii, this-is-another-very-long-name-for-a-nifti-file.nii, this-is-again-another-very-long-name-for-a-nifti-file.nii]'
assert repr_niimgs(list_of_size_3, shorten=False) == long_rep_list_of_size_3
long_list_small_names = ['test', 'retest', 'reretest', 'rereretest']
long_rep_long_list_small_names = '[test,\n retest,\n reretest,\n rereretest]'
assert repr_niimgs(long_list_small_names, shorten=False) == long_rep_long_list_small_names
list_of_size_4 = [*list_of_size_3, 'this-is-again-another-super-very-long-name-for-a-nifti-file.nii']
long_rep_long_list_long_names = long_rep_list_of_size_3[:-1].replace(',', ',\n') + ',\n ' + 'this-is-again-another-super-very-long-name-for-a-nifti-file.nii]'
assert repr_niimgs(list_of_size_4, shorten=False) == long_rep_long_list_long_names
```

## Next Steps


---

*Source: test_niimg.py:177 | Complexity: Advanced | Last updated: 2026-05-18*