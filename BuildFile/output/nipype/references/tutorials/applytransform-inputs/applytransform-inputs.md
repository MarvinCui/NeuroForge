# How To: Applytransform Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ApplyTransform inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(in_file=dict(copyfile=True, extensions=None, mandatory=True), mat=dict(extensions=None, mandatory=True), matlab_cmd=dict(), mfile=dict(usedefault=True), out_file=dict(extensions=None, genfile=True), paths=dict(), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(in_file=dict(copyfile=True, extensions=None, mandatory=True), mat=dict(extensions=None, mandatory=True), matlab_cmd=dict(), mfile=dict(usedefault=True), out_file=dict(extensions=None, genfile=True), paths=dict(), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True))
```

## Next Steps


---

*Source: test_auto_ApplyTransform.py:6 | Complexity: Beginner | Last updated: 2026-05-18*