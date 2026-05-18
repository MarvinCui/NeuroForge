# How To: Labeltable

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: workflow, integration

## Overview

Workflow: test labeltable

## Prerequisites

**Required Modules:**
- `itertools`
- `sys`
- `io`
- `numpy`
- `pytest`
- `numpy.testing`
- `nibabel.tmpdirs`
- `fileholders`
- `nifti1`
- `testing`
- `test_parse_gifti_fast`
- `gifti`


## Step-by-Step Guide

### Step 1: Assign img = GiftiImage(...)

```python
img = GiftiImage()
```

**Verification:**
```python
assert len(img.labeltable.labels) == 0
```

### Step 2: Assign new_table = GiftiLabelTable(...)

```python
new_table = GiftiLabelTable()
```

**Verification:**
```python
assert len(img.labeltable.labels) == 2
```

### Step 3: Assign img.labeltable = new_table

```python
img.labeltable = new_table
```

**Verification:**
```python
assert len(img.labeltable.labels) == 2
```


## Complete Example

```python
# Workflow
img = GiftiImage()
assert len(img.labeltable.labels) == 0
new_table = GiftiLabelTable()
new_table.labels += ['test', 'me']
img.labeltable = new_table
assert len(img.labeltable.labels) == 2
```

## Next Steps


---

*Source: test_gifti.py:267 | Complexity: Beginner | Last updated: 2026-05-18*