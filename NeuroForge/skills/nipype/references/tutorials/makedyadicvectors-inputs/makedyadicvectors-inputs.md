# How To: Makedyadicvectors Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MakeDyadicVectors inputs

## Prerequisites

**Required Modules:**
- `dti`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), mask=dict(argstr='%s', extensions=None, position=2), output=dict(argstr='%s', extensions=None, hash_files=False, position=3, usedefault=True), output_type=dict(), perc=dict(argstr='%f', position=4), phi_vol=dict(argstr='%s', extensions=None, mandatory=True, position=1), theta_vol=dict(argstr='%s', extensions=None, mandatory=True, position=0))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), mask=dict(argstr='%s', extensions=None, position=2), output=dict(argstr='%s', extensions=None, hash_files=False, position=3, usedefault=True), output_type=dict(), perc=dict(argstr='%f', position=4), phi_vol=dict(argstr='%s', extensions=None, mandatory=True, position=1), theta_vol=dict(argstr='%s', extensions=None, mandatory=True, position=0))
```

## Next Steps


---

*Source: test_auto_MakeDyadicVectors.py:6 | Complexity: Beginner | Last updated: 2026-05-18*