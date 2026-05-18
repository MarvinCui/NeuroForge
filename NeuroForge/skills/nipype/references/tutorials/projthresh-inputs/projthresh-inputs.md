# How To: Projthresh Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ProjThresh inputs

## Prerequisites

**Required Modules:**
- `dti`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_files=dict(argstr='%s', mandatory=True, position=0), output_type=dict(), threshold=dict(argstr='%d', mandatory=True, position=1))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_files=dict(argstr='%s', mandatory=True, position=0), output_type=dict(), threshold=dict(argstr='%d', mandatory=True, position=1))
```

## Next Steps


---

*Source: test_auto_ProjThresh.py:6 | Complexity: Beginner | Last updated: 2026-05-18*