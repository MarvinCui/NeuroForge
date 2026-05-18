# How To: Apas2Aseg Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Apas2Aseg inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='--i %s', extensions=None, mandatory=True), out_file=dict(argstr='--o %s', extensions=None, mandatory=True), subjects_dir=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='--i %s', extensions=None, mandatory=True), out_file=dict(argstr='--o %s', extensions=None, mandatory=True), subjects_dir=dict())
```

## Next Steps


---

*Source: test_auto_Apas2Aseg.py:6 | Complexity: Beginner | Last updated: 2026-05-18*