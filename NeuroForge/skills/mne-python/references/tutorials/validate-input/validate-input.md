# How To: Validate Input

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test Report input validation.

## Prerequisites

**Required Modules:**
- `base64`
- `glob`
- `os`
- `pickle`
- `re`
- `shutil`
- `io`
- `pathlib`
- `numpy`
- `pytest`
- `matplotlib`
- `mne`
- `mne._fiff.write`
- `mne.datasets`
- `mne.epochs`
- `mne.fixes`
- `mne.io`
- `mne.preprocessing`
- `mne.report`
- `mne.report`
- `mne.report.report`
- `mne.utils`
- `mne.utils._testing`
- `mne.viz`
- `sklearn.exceptions`
- `PIL`
- `pyvista.plotting.plotter`
- `pyvista.plotting.plotting`


## Step-by-Step Guide

### Step 1: 'Test Report input validation.'

```python
'Test Report input validation.'
```

### Step 2: Assign report = Report(...)

```python
report = Report()
```

### Step 3: Assign items = value

```python
items = ['a', 'b', 'c']
```

### Step 4: Assign captions = value

```python
captions = ['Letter A', 'Letter B', 'Letter C']
```

### Step 5: Assign section = 'ABCs'

```python
section = 'ABCs'
```

### Step 6: Assign comments = value

```python
comments = ['First letter of the alphabet.', 'Second letter of the alphabet', 'Third letter of the alphabet']
```

### Step 7: Call pytest.raises()

```python
pytest.raises(ValueError, report._validate_input, items, captions[:-1], section, comments=None)
```

### Step 8: Call pytest.raises()

```python
pytest.raises(ValueError, report._validate_input, items, captions, section, comments=comments[:-1])
```

### Step 9: Assign values = report._validate_input(...)

```python
values = report._validate_input(items, captions, section, comments=None)
```

### Step 10: Assign unknown = values

```python
items_new, captions_new, comments_new = values
```


## Complete Example

```python
# Workflow
'Test Report input validation.'
report = Report()
items = ['a', 'b', 'c']
captions = ['Letter A', 'Letter B', 'Letter C']
section = 'ABCs'
comments = ['First letter of the alphabet.', 'Second letter of the alphabet', 'Third letter of the alphabet']
pytest.raises(ValueError, report._validate_input, items, captions[:-1], section, comments=None)
pytest.raises(ValueError, report._validate_input, items, captions, section, comments=comments[:-1])
values = report._validate_input(items, captions, section, comments=None)
items_new, captions_new, comments_new = values
```

## Next Steps


---

*Source: test_report.py:595 | Complexity: Advanced | Last updated: 2026-05-18*