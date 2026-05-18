# How To: Vest2Text Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Vest2Text inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=0), out_file=dict(argstr='%s', extensions=None, position=1, usedefault=True), output_type=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=0), out_file=dict(argstr='%s', extensions=None, position=1, usedefault=True), output_type=dict())
```

## Next Steps


---

*Source: test_auto_Vest2Text.py:6 | Complexity: Beginner | Last updated: 2026-05-18*