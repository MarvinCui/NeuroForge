# How To: Eddycorrect Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test EddyCorrect inputs

## Prerequisites

**Required Modules:**
- `epi`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=0), out_file=dict(argstr='%s', extensions=None, name_source=['in_file'], name_template='%s_edc', output_name='eddy_corrected', position=1), output_type=dict(), ref_num=dict(argstr='%d', mandatory=True, position=2, usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=0), out_file=dict(argstr='%s', extensions=None, name_source=['in_file'], name_template='%s_edc', output_name='eddy_corrected', position=1), output_type=dict(), ref_num=dict(argstr='%d', mandatory=True, position=2, usedefault=True))
```

## Next Steps


---

*Source: test_auto_EddyCorrect.py:6 | Complexity: Beginner | Last updated: 2026-05-18*