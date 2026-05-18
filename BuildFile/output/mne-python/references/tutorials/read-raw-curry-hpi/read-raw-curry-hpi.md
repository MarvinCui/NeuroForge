# How To: Read Raw Curry Hpi

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test reading hpi file.

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
# Fixtures: good_match, tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test reading hpi file.'

```python
'Test reading hpi file.'
```

### Step 2: Assign fname = curry_hpi_file

```python
fname = curry_hpi_file
```

### Step 3: Call read_raw_curry()

```python
read_raw_curry(fname, on_bad_hpi_match='ignore')
```

### Step 4: Assign fname = value

```python
fname = tmp_path / fname.name
```

### Step 5: Call read_raw_curry()

```python
read_raw_curry(fname, on_bad_hpi_match='ignore')
```

### Step 6: Call read_raw_curry()

```python
read_raw_curry(fname, on_bad_hpi_match='warn')
```

### Step 7: Call read_raw_curry()

```python
read_raw_curry(fname, on_bad_hpi_match='raise')
```

### Step 8: Call read_raw_curry()

```python
read_raw_curry(fname, on_bad_hpi_match='warn')
```

### Step 9: Call read_raw_curry()

```python
read_raw_curry(fname, on_bad_hpi_match='raise')
```

### Step 10: Assign src = fname.with_suffix(...)

```python
src = fname.with_suffix(ext)
```

### Step 11: Assign dst = value

```python
dst = tmp_path / fname.with_suffix(ext).name
```

### Step 12: Call copyfile()

```python
copyfile(src, dst)
```

### Step 13: Call fid.write()

```python
fid.write(GOOD_HPI_MATCH)
```


## Complete Example

```python
# Setup
# Fixtures: good_match, tmp_path

# Workflow
'Test reading hpi file.'
fname = curry_hpi_file
if not good_match:
    read_raw_curry(fname, on_bad_hpi_match='ignore')
    with pytest.warns(match='Poor HPI matching'):
        read_raw_curry(fname, on_bad_hpi_match='warn')
    with pytest.raises(ValueError, match='Poor HPI matching'):
        read_raw_curry(fname, on_bad_hpi_match='raise')
else:
    for ext in ('.cdt', '.cdt.dpa'):
        src = fname.with_suffix(ext)
        dst = tmp_path / fname.with_suffix(ext).name
        copyfile(src, dst)
    fname = tmp_path / fname.name
    with open(fname.with_suffix(fname.suffix + '.hpi'), 'w') as fid:
        fid.write(GOOD_HPI_MATCH)
    read_raw_curry(fname, on_bad_hpi_match='ignore')
    read_raw_curry(fname, on_bad_hpi_match='warn')
    read_raw_curry(fname, on_bad_hpi_match='raise')
```

## Next Steps


---

*Source: test_curry.py:115 | Complexity: Advanced | Last updated: 2026-05-18*