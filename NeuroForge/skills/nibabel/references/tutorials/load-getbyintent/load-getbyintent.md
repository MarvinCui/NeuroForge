# How To: Load Getbyintent

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test load getbyintent

## Prerequisites

**Required Modules:**
- `shutil`
- `sys`
- `warnings`
- `os.path`
- `os.path`
- `unittest`
- `numpy`
- `pytest`
- `numpy.testing`
- `loadsave`
- `nifti1`
- `testing`
- `tmpdirs`
- `parse_gifti_fast`
- `util`


## Step-by-Step Guide

### Step 1: Assign img = load(...)

```python
img = load(DATA_FILE1)
```

**Verification:**
```python
assert len(da) == 1
```

### Step 2: Assign da = img.get_arrays_from_intent(...)

```python
da = img.get_arrays_from_intent('NIFTI_INTENT_POINTSET')
```

**Verification:**
```python
assert len(da) == 1
```

### Step 3: Assign da = img.get_arrays_from_intent(...)

```python
da = img.get_arrays_from_intent('NIFTI_INTENT_TRIANGLE')
```

**Verification:**
```python
assert len(da) == 0
```

### Step 4: Assign da = img.get_arrays_from_intent(...)

```python
da = img.get_arrays_from_intent('NIFTI_INTENT_CORREL')
```

**Verification:**
```python
assert da == []
```


## Complete Example

```python
# Workflow
img = load(DATA_FILE1)
da = img.get_arrays_from_intent('NIFTI_INTENT_POINTSET')
assert len(da) == 1
da = img.get_arrays_from_intent('NIFTI_INTENT_TRIANGLE')
assert len(da) == 1
da = img.get_arrays_from_intent('NIFTI_INTENT_CORREL')
assert len(da) == 0
assert da == []
```

## Next Steps


---

*Source: test_parse_gifti_fast.py:353 | Complexity: Intermediate | Last updated: 2026-05-18*