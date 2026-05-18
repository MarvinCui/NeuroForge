# How To: Invalid Filetype

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Invalid file types/associated files for load method.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `re`
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `scipy.stats`
- `sklearn.preprocessing`
- `nilearn._utils.data_gen`
- `nilearn._utils.fmriprep_confounds`
- `nilearn.conftest`
- `nilearn.interfaces.bids`
- `nilearn.interfaces.fmriprep`
- `nilearn.interfaces.fmriprep.load_confounds`
- `nilearn.interfaces.fmriprep.tests._testing`
- `nilearn.maskers`
- `nilearn.tests.test_signal`
- `inspect`

**Setup Required:**
```python
# Fixtures: tmp_path, rng
```

## Step-by-Step Guide

### Step 1: 'Invalid file types/associated files for load method.'

```python
'Invalid file types/associated files for load method.'
```

**Verification:**
```python
assert 'more than one' in str(info.value)
```

### Step 2: Assign unknown = create_tmp_filepath(...)

```python
bad_nii, bad_conf = create_tmp_filepath(tmp_path, copy_confounds=True, fmriprep_version='1.4.x')
```

**Verification:**
```python
assert 'The confound file contains no header.' in str(error_log.value)
```

### Step 3: Assign unknown = load_confounds(...)

```python
_, _ = load_confounds(bad_nii)
```

**Verification:**
```python
assert 'contains header in camel case.' in str(error_log.value)
```

### Step 4: Assign add_conf = 'sub-14x_task-test_desc-confounds_regressors.tsv'

```python
add_conf = 'sub-14x_task-test_desc-confounds_regressors.tsv'
```

### Step 5: Assign unknown = get_legal_confound(...)

```python
legal_confounds, _ = get_legal_confound()
```

### Step 6: Call legal_confounds.to_csv()

```python
legal_confounds.to_csv(tmp_path / add_conf, sep='\t', index=False)
```

**Verification:**
```python
assert 'more than one' in str(info.value)
```

### Step 7: Call unknown.unlink()

```python
(tmp_path / add_conf).unlink()
```

### Step 8: Assign fake_confounds = rng.random(...)

```python
fake_confounds = rng.random((30, 20))
```

### Step 9: Call np.savetxt()

```python
np.savetxt(bad_conf, fake_confounds, delimiter='\t')
```

**Verification:**
```python
assert 'The confound file contains no header.' in str(error_log.value)
```

### Step 10: Assign unknown = get_legal_confound(...)

```python
legal_confounds, _ = get_legal_confound()
```

### Step 11: Assign camel_confounds = legal_confounds.copy(...)

```python
camel_confounds = legal_confounds.copy()
```

### Step 12: Assign camel_confounds.columns = value

```python
camel_confounds.columns = [to_camel_case(col_name) for col_name in legal_confounds.columns]
```

### Step 13: Call camel_confounds.to_csv()

```python
camel_confounds.to_csv(bad_conf, sep='\t', index=False)
```

**Verification:**
```python
assert 'contains header in camel case.' in str(error_log.value)
```

### Step 14: Assign no_conf = 'no_confound_space-MNI152NLin2009cAsym_desc-preproc_bold.nii.gz'

```python
no_conf = 'no_confound_space-MNI152NLin2009cAsym_desc-preproc_bold.nii.gz'
```

### Step 15: Assign no_confound = value

```python
no_confound = tmp_path / no_conf
```

### Step 16: Call no_confound.touch()

```python
no_confound.touch()
```

### Step 17: Call load_confounds()

```python
load_confounds(bad_nii)
```

### Step 18: Call load_confounds()

```python
load_confounds(bad_nii)
```

### Step 19: Call load_confounds()

```python
load_confounds(bad_nii)
```

### Step 20: Call load_confounds()

```python
load_confounds(bad_nii)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, rng

# Workflow
'Invalid file types/associated files for load method.'
bad_nii, bad_conf = create_tmp_filepath(tmp_path, copy_confounds=True, fmriprep_version='1.4.x')
_, _ = load_confounds(bad_nii)
add_conf = 'sub-14x_task-test_desc-confounds_regressors.tsv'
legal_confounds, _ = get_legal_confound()
legal_confounds.to_csv(tmp_path / add_conf, sep='\t', index=False)
with pytest.raises(ValueError) as info:
    load_confounds(bad_nii)
assert 'more than one' in str(info.value)
(tmp_path / add_conf).unlink()
fake_confounds = rng.random((30, 20))
np.savetxt(bad_conf, fake_confounds, delimiter='\t')
with pytest.raises(ValueError) as error_log:
    load_confounds(bad_nii)
assert 'The confound file contains no header.' in str(error_log.value)
legal_confounds, _ = get_legal_confound()
camel_confounds = legal_confounds.copy()
camel_confounds.columns = [to_camel_case(col_name) for col_name in legal_confounds.columns]
camel_confounds.to_csv(bad_conf, sep='\t', index=False)
with pytest.raises(ValueError) as error_log:
    load_confounds(bad_nii)
assert 'contains header in camel case.' in str(error_log.value)
no_conf = 'no_confound_space-MNI152NLin2009cAsym_desc-preproc_bold.nii.gz'
no_confound = tmp_path / no_conf
no_confound.touch()
with pytest.raises(ValueError):
    load_confounds(bad_nii)
```

## Next Steps


---

*Source: test_load_confounds.py:578 | Complexity: Advanced | Last updated: 2026-05-18*