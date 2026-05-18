# How To: Sh2Amp Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test SH2Amp inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), directions=dict(argstr='%s', extensions=None, mandatory=True, position=-2), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-3), nonnegative=dict(argstr='-nonnegative'), out_file=dict(argstr='%s', extensions=None, name_source=['in_file'], name_template='%s_amp.mif', position=-1, usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), directions=dict(argstr='%s', extensions=None, mandatory=True, position=-2), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-3), nonnegative=dict(argstr='-nonnegative'), out_file=dict(argstr='%s', extensions=None, name_source=['in_file'], name_template='%s_amp.mif', position=-1, usedefault=True))
```

## Next Steps


---

*Source: test_auto_SH2Amp.py:6 | Complexity: Beginner | Last updated: 2026-05-18*