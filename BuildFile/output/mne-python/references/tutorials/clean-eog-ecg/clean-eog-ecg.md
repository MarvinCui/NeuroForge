# How To: Clean Eog Ecg

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test mne clean_eog_ecg.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `glob`
- `os`
- `platform`
- `shutil`
- `os`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne.bem`
- `mne.commands`
- `mne.datasets`
- `mne.io`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test mne clean_eog_ecg.'

```python
'Test mne clean_eog_ecg.'
```

**Verification:**
```python
assert len(fnames) == count
```

### Step 2: Call check_usage()

```python
check_usage(mne_clean_eog_ecg)
```

### Step 3: Assign tempdir = str(...)

```python
tempdir = str(tmp_path)
```

### Step 4: Assign raw = concatenate_raws(...)

```python
raw = concatenate_raws([read_raw_fif(f) for f in [raw_fname, raw_fname, raw_fname]])
```

### Step 5: Assign unknown = value

```python
raw.info['bads'] = ['MEG 2443']
```

### Step 6: Assign use_fname = op.join(...)

```python
use_fname = op.join(tempdir, op.basename(raw_fname))
```

### Step 7: Call raw.save()

```python
raw.save(use_fname)
```

### Step 8: Call mne_clean_eog_ecg.run()

```python
mne_clean_eog_ecg.run()
```

### Step 9: Assign fnames = glob.glob(...)

```python
fnames = glob.glob(op.join(tempdir, f'*{key}.fif'))
```

**Verification:**
```python
assert len(fnames) == count
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test mne clean_eog_ecg.'
check_usage(mne_clean_eog_ecg)
tempdir = str(tmp_path)
raw = concatenate_raws([read_raw_fif(f) for f in [raw_fname, raw_fname, raw_fname]])
raw.info['bads'] = ['MEG 2443']
use_fname = op.join(tempdir, op.basename(raw_fname))
raw.save(use_fname)
with ArgvSetter(('-i', use_fname, '--quiet')):
    mne_clean_eog_ecg.run()
for key, count in (('proj', 2), ('-eve', 3)):
    fnames = glob.glob(op.join(tempdir, f'*{key}.fif'))
    assert len(fnames) == count
```

## Next Steps


---

*Source: test_commands.py:128 | Complexity: Advanced | Last updated: 2026-05-18*