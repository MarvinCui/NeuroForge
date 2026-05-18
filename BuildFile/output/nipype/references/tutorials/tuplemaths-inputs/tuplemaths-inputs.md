# How To: Tuplemaths Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test TupleMaths inputs

## Prerequisites

**Required Modules:**
- `maths`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=2), operand_file1=dict(argstr='%s', extensions=None, mandatory=True, position=5, xor=['operand_value1']), operand_file2=dict(argstr='%s', extensions=None, mandatory=True, position=6, xor=['operand_value2']), operand_value1=dict(argstr='%.8f', mandatory=True, position=5, xor=['operand_file1']), operand_value2=dict(argstr='%.8f', mandatory=True, position=6, xor=['operand_file2']), operation=dict(argstr='-%s', mandatory=True, position=4), out_file=dict(argstr='%s', extensions=None, name_source=['in_file'], name_template='%s', position=-2), output_datatype=dict(argstr='-odt %s', position=-3))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=2), operand_file1=dict(argstr='%s', extensions=None, mandatory=True, position=5, xor=['operand_value1']), operand_file2=dict(argstr='%s', extensions=None, mandatory=True, position=6, xor=['operand_value2']), operand_value1=dict(argstr='%.8f', mandatory=True, position=5, xor=['operand_file1']), operand_value2=dict(argstr='%.8f', mandatory=True, position=6, xor=['operand_file2']), operation=dict(argstr='-%s', mandatory=True, position=4), out_file=dict(argstr='%s', extensions=None, name_source=['in_file'], name_template='%s', position=-2), output_datatype=dict(argstr='-odt %s', position=-3))
```

## Next Steps


---

*Source: test_auto_TupleMaths.py:6 | Complexity: Beginner | Last updated: 2026-05-18*