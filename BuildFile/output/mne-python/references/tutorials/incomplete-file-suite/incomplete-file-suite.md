# How To: Incomplete File Suite

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test reading incomplete Curry filesets.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `datetime`
- `pathlib`
- `shutil`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne._fiff.constants`
- `mne._fiff.tag`
- `mne.annotations`
- `mne.bem`
- `mne.channels`
- `mne.datasets`
- `mne.epochs`
- `mne.event`
- `mne.io.bti`
- `mne.io.curry`
- `mne.io.curry.curry`
- `mne.io.edf`
- `mne.io.tests.test_raw`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path, fname
```

## Step-by-Step Guide

### Step 1: 'Test reading incomplete Curry filesets.'

```python
'Test reading incomplete Curry filesets.'
```

### Step 2: Assign unknown = value

```python
original, modified = (dict(), dict())
```

### Step 3: Assign version = _get_curry_version(...)

```python
version = _get_curry_version(fname)
```

### Step 4: Assign unknown = fname.with_suffix(...)

```python
original['base'] = fname.with_suffix('')
```

### Step 5: Assign unknown = fname.with_suffix(...)

```python
original['event'] = fname.with_suffix(FILE_EXTENSIONS[version]['events_cef'])
```

### Step 6: Assign unknown = fname.with_suffix(...)

```python
original['info'] = fname.with_suffix(FILE_EXTENSIONS[version]['info'])
```

### Step 7: Assign unknown = fname.with_suffix(...)

```python
original['data'] = fname.with_suffix(FILE_EXTENSIONS[version]['data'])
```

### Step 8: Assign unknown = fname.with_suffix(...)

```python
original['labels'] = fname.with_suffix(FILE_EXTENSIONS[version]['labels'])
```

### Step 9: Assign unknown = value

```python
modified['base'] = tmp_path / 'curry'
```

### Step 10: Assign unknown = unknown.with_suffix(...)

```python
modified['event'] = modified['base'].with_suffix(FILE_EXTENSIONS[version]['events_cef'])
```

### Step 11: Assign unknown = unknown.with_suffix(...)

```python
modified['info'] = modified['base'].with_suffix(FILE_EXTENSIONS[version]['info'])
```

### Step 12: Assign unknown = unknown.with_suffix(...)

```python
modified['data'] = modified['base'].with_suffix(FILE_EXTENSIONS[version]['data'])
```

### Step 13: Assign unknown = unknown.with_suffix(...)

```python
modified['labels'] = modified['base'].with_suffix(FILE_EXTENSIONS[version]['labels'])
```

### Step 14: Call copyfile()

```python
copyfile(src=original['data'], dst=modified['data'])
```

### Step 15: Assign _msg = value

```python
_msg = f"does not exist: .*{modified['event'].name}.*"
```

### Step 16: Call copyfile()

```python
copyfile(src=original['info'], dst=modified['info'])
```

### Step 17: Call copyfile()

```python
copyfile(src=original['event'], dst=modified['event'])
```

### Step 18: Call read_raw_curry()

```python
read_raw_curry(modified['data'])
```

### Step 19: Call read_annotations()

```python
read_annotations(modified['event'], sfreq='auto')
```

### Step 20: Call read_annotations()

```python
read_annotations(modified['event'], sfreq='auto')
```

### Step 21: Call copyfile()

```python
copyfile(src=original['labels'], dst=modified['labels'])
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, fname

# Workflow
'Test reading incomplete Curry filesets.'
original, modified = (dict(), dict())
version = _get_curry_version(fname)
original['base'] = fname.with_suffix('')
original['event'] = fname.with_suffix(FILE_EXTENSIONS[version]['events_cef'])
original['info'] = fname.with_suffix(FILE_EXTENSIONS[version]['info'])
original['data'] = fname.with_suffix(FILE_EXTENSIONS[version]['data'])
original['labels'] = fname.with_suffix(FILE_EXTENSIONS[version]['labels'])
modified['base'] = tmp_path / 'curry'
modified['event'] = modified['base'].with_suffix(FILE_EXTENSIONS[version]['events_cef'])
modified['info'] = modified['base'].with_suffix(FILE_EXTENSIONS[version]['info'])
modified['data'] = modified['base'].with_suffix(FILE_EXTENSIONS[version]['data'])
modified['labels'] = modified['base'].with_suffix(FILE_EXTENSIONS[version]['labels'])
copyfile(src=original['data'], dst=modified['data'])
_msg = f"does not exist: .*{modified['event'].name}.*"
with pytest.raises(FileNotFoundError, match=_msg):
    read_annotations(modified['event'], sfreq='auto')
copyfile(src=original['info'], dst=modified['info'])
with pytest.raises(FileNotFoundError, match=_msg):
    read_annotations(modified['event'], sfreq='auto')
copyfile(src=original['event'], dst=modified['event'])
if not modified['labels'].exists():
    copyfile(src=original['labels'], dst=modified['labels'])
read_raw_curry(modified['data'])
```

## Next Steps


---

*Source: test_curry.py:559 | Complexity: Advanced | Last updated: 2026-05-18*