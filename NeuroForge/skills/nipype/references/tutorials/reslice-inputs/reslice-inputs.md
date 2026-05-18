# How To: Reslice Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Reslice inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(in_file=dict(extensions=None, mandatory=True), interp=dict(usedefault=True), matlab_cmd=dict(), mfile=dict(usedefault=True), out_file=dict(extensions=None), paths=dict(), space_defining=dict(extensions=None, mandatory=True), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(in_file=dict(extensions=None, mandatory=True), interp=dict(usedefault=True), matlab_cmd=dict(), mfile=dict(usedefault=True), out_file=dict(extensions=None), paths=dict(), space_defining=dict(extensions=None, mandatory=True), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True))
```

## Next Steps


---

*Source: test_auto_Reslice.py:6 | Complexity: Beginner | Last updated: 2026-05-18*