# How To: Persyst Moved File

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test reader - Persyst files need to be in same directory.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `shutil`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.tests.test_raw`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test reader - Persyst files need to be in same directory.'

```python
'Test reader - Persyst files need to be in same directory.'
```

### Step 2: Assign new_fname_lay = value

```python
new_fname_lay = tmp_path / fname_lay.name
```

### Step 3: Assign new_fname_dat = value

```python
new_fname_dat = tmp_path / fname_dat.name
```

### Step 4: Call shutil.copy()

```python
shutil.copy(fname_lay, new_fname_lay)
```

### Step 5: Call _chmod_rw_R()

```python
_chmod_rw_R(tmp_path)
```

### Step 6: Call read_raw_persyst()

```python
read_raw_persyst(fname_lay)
```

### Step 7: Assign desired_err_msg = 'The data path you specified does not exist for the lay path, sub-pt1_ses-02_task-monitor_acq-ecog_run-01_clip2.lay'

```python
desired_err_msg = 'The data path you specified does not exist for the lay path, sub-pt1_ses-02_task-monitor_acq-ecog_run-01_clip2.lay'
```

### Step 8: Call shutil.copy()

```python
shutil.copy(fname_dat, new_fname_dat)
```

### Step 9: Call read_raw_persyst()

```python
read_raw_persyst(new_fname_lay, preload=True)
```

### Step 10: Call read_raw_persyst()

```python
read_raw_persyst(new_fname_lay, preload=True)
```

### Step 11: Call read_raw_persyst()

```python
read_raw_persyst(new_fname_lay, preload=True)
```

### Step 12: Call fout.write()

```python
fout.write(line)
```

### Step 13: Assign test_fpath = value

```python
test_fpath = fname_dat.parent / line.split('=')[1]
```

### Step 14: Assign line = value

```python
line = f'File={test_fpath}\n'
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test reader - Persyst files need to be in same directory.'
new_fname_lay = tmp_path / fname_lay.name
new_fname_dat = tmp_path / fname_dat.name
shutil.copy(fname_lay, new_fname_lay)
_chmod_rw_R(tmp_path)
read_raw_persyst(fname_lay)
desired_err_msg = 'The data path you specified does not exist for the lay path, sub-pt1_ses-02_task-monitor_acq-ecog_run-01_clip2.lay'
with pytest.raises(FileNotFoundError, match=desired_err_msg):
    read_raw_persyst(new_fname_lay, preload=True)
with open(fname_lay) as fin:
    with open(new_fname_lay, 'w') as fout:
        for idx, line in enumerate(fin):
            if line.startswith('File='):
                test_fpath = fname_dat.parent / line.split('=')[1]
                line = f'File={test_fpath}\n'
            fout.write(line)
with pytest.raises(FileNotFoundError, match=desired_err_msg):
    read_raw_persyst(new_fname_lay, preload=True)
shutil.copy(fname_dat, new_fname_dat)
read_raw_persyst(new_fname_lay, preload=True)
```

## Next Steps


---

*Source: test_persyst.py:143 | Complexity: Advanced | Last updated: 2026-05-18*