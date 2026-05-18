# How To: Quickshear Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Quickshear inputs

## Prerequisites

**Required Modules:**
- `quickshear`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), buff=dict(argstr='%d', position=4), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=1), mask_file=dict(argstr='%s', extensions=None, mandatory=True, position=2), out_file=dict(argstr='%s', extensions=None, keep_extension=True, name_source='in_file', name_template='%s_defaced', position=3))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), buff=dict(argstr='%d', position=4), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=1), mask_file=dict(argstr='%s', extensions=None, mandatory=True, position=2), out_file=dict(argstr='%s', extensions=None, keep_extension=True, name_source='in_file', name_template='%s_defaced', position=3))
```

## Next Steps


---

*Source: test_auto_Quickshear.py:6 | Complexity: Beginner | Last updated: 2026-05-18*