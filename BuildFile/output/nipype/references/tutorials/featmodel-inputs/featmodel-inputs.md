# How To: Featmodel Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test FEATModel inputs

## Prerequisites

**Required Modules:**
- `model`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), ev_files=dict(argstr='%s', copyfile=False, mandatory=True, position=1), fsf_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=0), output_type=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), ev_files=dict(argstr='%s', copyfile=False, mandatory=True, position=1), fsf_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=0), output_type=dict())
```

## Next Steps


---

*Source: test_auto_FEATModel.py:6 | Complexity: Beginner | Last updated: 2026-05-18*