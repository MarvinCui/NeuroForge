# How To: Calccoregaffine Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test CalcCoregAffine inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(invmat=dict(extensions=None), mat=dict(extensions=None), matlab_cmd=dict(), mfile=dict(usedefault=True), moving=dict(copyfile=False, extensions=None, mandatory=True), paths=dict(), target=dict(extensions=None, mandatory=True), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(invmat=dict(extensions=None), mat=dict(extensions=None), matlab_cmd=dict(), mfile=dict(usedefault=True), moving=dict(copyfile=False, extensions=None, mandatory=True), paths=dict(), target=dict(extensions=None, mandatory=True), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True))
```

## Next Steps


---

*Source: test_auto_CalcCoregAffine.py:6 | Complexity: Beginner | Last updated: 2026-05-18*