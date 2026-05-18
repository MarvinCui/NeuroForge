# How To: All Reader Documented In Docstring

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that all the readers are documented in read_raw docstring.

## Prerequisites

**Required Modules:**
- `pathlib`
- `shutil`
- `pytest`
- `mne.datasets`
- `mne.io`
- `mne.io._read_raw`


## Step-by-Step Guide

### Step 1: 'Test that all the readers are documented in read_raw docstring.'

```python
'Test that all the readers are documented in read_raw docstring.'
```

### Step 2: Assign readers = _get_supported(...)

```python
readers = _get_supported()
```

### Step 3: Assign functions = value

```python
functions = [foo.__name__ for value in readers.values() for foo in value.values()]
```

### Step 4: Assign doc = value

```python
doc = read_raw.__doc__.split('Parameters')[0]
```

### Step 5: Assign documented = value

```python
documented = [elt.strip().split('`')[0] for elt in doc.split('mne.io.')[1:]]
```

### Step 6: Assign missing_from_docstring = value

```python
missing_from_docstring = set(functions) - set(documented)
```


## Complete Example

```python
# Workflow
'Test that all the readers are documented in read_raw docstring.'
readers = _get_supported()
functions = [foo.__name__ for value in readers.values() for foo in value.values()]
doc = read_raw.__doc__.split('Parameters')[0]
documented = [elt.strip().split('`')[0] for elt in doc.split('mne.io.')[1:]]
missing_from_docstring = set(functions) - set(documented)
if len(missing_from_docstring) != 0:
    raise AssertionError('Functions missing from docstring:\n\t' + '\n\t'.join(missing_from_docstring))
if sorted(documented) != documented:
    raise AssertionError('Functions in docstring are not sorted.')
```

## Next Steps


---

*Source: test_read_raw.py:145 | Complexity: Intermediate | Last updated: 2026-05-18*