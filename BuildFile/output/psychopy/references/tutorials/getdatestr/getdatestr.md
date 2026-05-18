# How To: Getdatestr

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test getDateStr

## Prerequisites

**Required Modules:**
- `os`
- `pathlib`
- `pytest`
- `numpy`
- `psychopy`
- `psychopy.data`
- `os.path`
- `numpy`
- `numpy`
- `time`


## Step-by-Step Guide

### Step 1: Assign millisecs_dateStr = utils.getDateStr(...)

```python
millisecs_dateStr = utils.getDateStr()
```

**Verification:**
```python
assert len(millisecs_dateStr) == len(microsecs_dateStr[:-3])
```

### Step 2: Assign microsecs_dateStr = utils.getDateStr(...)

```python
microsecs_dateStr = utils.getDateStr(fractionalSecondDigits=6)
```

**Verification:**
```python
assert customDateStr == time.strftime(shortFormat, time.localtime())
```

### Step 3: Assign shortFormat = '%Y_%b_%d_%H%M'

```python
shortFormat = '%Y_%b_%d_%H%M'
```

### Step 4: Assign customDateStr = utils.getDateStr(...)

```python
customDateStr = utils.getDateStr(shortFormat)
```

**Verification:**
```python
assert customDateStr == time.strftime(shortFormat, time.localtime())
```


## Complete Example

```python
# Workflow
import time
millisecs_dateStr = utils.getDateStr()
microsecs_dateStr = utils.getDateStr(fractionalSecondDigits=6)
assert len(millisecs_dateStr) == len(microsecs_dateStr[:-3])
shortFormat = '%Y_%b_%d_%H%M'
customDateStr = utils.getDateStr(shortFormat)
assert customDateStr == time.strftime(shortFormat, time.localtime())
```

## Next Steps


---

*Source: test_utils.py:143 | Complexity: Intermediate | Last updated: 2026-05-18*