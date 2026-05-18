# How To: Split Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Split inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), dimension=dict(argstr='-%s', mandatory=True, position=2), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=0), out_base_name=dict(argstr='%s', position=1), output_type=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), dimension=dict(argstr='-%s', mandatory=True, position=2), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=0), out_base_name=dict(argstr='%s', position=1), output_type=dict())
```

## Next Steps


---

*Source: test_auto_Split.py:6 | Complexity: Beginner | Last updated: 2026-05-18*