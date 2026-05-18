# How To: Overlaps

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test overlaps

## Prerequisites

**Required Modules:**
- `pathlib`
- `psychopy`
- `psychopy.tests`
- `psychopy.visual`
- `numpy`
- `matplotlib`
- `matplotlib`


## Step-by-Step Guide

### Step 1: Call contains_overlaps()

```python
contains_overlaps('overlaps')
```

### Step 2: Assign matplotlib.__version__ = '0.0'

```python
matplotlib.__version__ = '0.0'
```

### Step 3: Call contains_overlaps()

```python
contains_overlaps('overlaps')
```

### Step 4: Assign matplotlib.__version__ = mpl_version

```python
matplotlib.__version__ = mpl_version
```

### Step 5: Assign helpers.nxutils = nxutils

```python
helpers.nxutils = nxutils
```

### Step 6: Assign matplotlib.__version__ = '1.1'

```python
matplotlib.__version__ = '1.1'
```

### Step 7: Call contains_overlaps()

```python
contains_overlaps('overlaps')
```


## Complete Example

```python
# Workflow
contains_overlaps('overlaps')
if have_nxutils:
    helpers.nxutils = nxutils
    matplotlib.__version__ = '1.1'
    contains_overlaps('overlaps')
    del helpers.nxutils
matplotlib.__version__ = '0.0'
contains_overlaps('overlaps')
matplotlib.__version__ = mpl_version
```

## Next Steps


---

*Source: test_contains_overlaps.py:168 | Complexity: Intermediate | Last updated: 2026-05-18*