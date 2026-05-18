# How To: Dot Names

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test that dots are parsed properly (e.g., in paths).

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
# Fixtures: fname, others, tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test that dots are parsed properly (e.g., in paths).'

```python
'Test that dots are parsed properly (e.g., in paths).'
```

### Step 2: Assign my_path = value

```python
my_path = tmp_path / 'dot.dot.dot'
```

### Step 3: Call my_path.mkdir()

```python
my_path.mkdir()
```

### Step 4: Assign my_path = value

```python
my_path = my_path / Path(fname).parts[-1]
```

### Step 5: Assign fname = Path(...)

```python
fname = Path(fname)
```

### Step 6: Call copyfile()

```python
copyfile(fname, my_path)
```

### Step 7: Call read_raw_curry()

```python
read_raw_curry(my_path)
```

### Step 8: Assign this_fname = fname.with_suffix(...)

```python
this_fname = fname.with_suffix(ext)
```

### Step 9: Assign to_fname = my_path.with_suffix(...)

```python
to_fname = my_path.with_suffix(ext)
```

### Step 10: Call copyfile()

```python
copyfile(this_fname, to_fname)
```


## Complete Example

```python
# Setup
# Fixtures: fname, others, tmp_path

# Workflow
'Test that dots are parsed properly (e.g., in paths).'
my_path = tmp_path / 'dot.dot.dot'
my_path.mkdir()
my_path = my_path / Path(fname).parts[-1]
fname = Path(fname)
copyfile(fname, my_path)
for ext in others:
    this_fname = fname.with_suffix(ext)
    to_fname = my_path.with_suffix(ext)
    copyfile(this_fname, to_fname)
read_raw_curry(my_path)
```

## Next Steps


---

*Source: test_curry.py:663 | Complexity: Advanced | Last updated: 2026-05-18*