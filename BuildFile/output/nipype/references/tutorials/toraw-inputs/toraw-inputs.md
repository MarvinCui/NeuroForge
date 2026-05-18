# How To: Toraw Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ToRaw inputs

## Prerequisites

**Required Modules:**
- `minc`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), input_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), nonormalize=dict(argstr='-nonormalize', xor=('normalize', 'nonormalize')), normalize=dict(argstr='-normalize', xor=('normalize', 'nonormalize')), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), output_file=dict(extensions=None, hash_files=False, keep_extension=False, name_source=['input_file'], name_template='%s.raw', position=-1), write_byte=dict(argstr='-byte', xor=('write_byte', 'write_short', 'write_int', 'write_long', 'write_float', 'write_double')), write_double=dict(argstr='-double', xor=('write_byte', 'write_short', 'write_int', 'write_long', 'write_float', 'write_double')), write_float=dict(argstr='-float', xor=('write_byte', 'write_short', 'write_int', 'write_long', 'write_float', 'write_double')), write_int=dict(argstr='-int', xor=('write_byte', 'write_short', 'write_int', 'write_long', 'write_float', 'write_double')), write_long=dict(argstr='-long', xor=('write_byte', 'write_short', 'write_int', 'write_long', 'write_float', 'write_double')), write_range=dict(argstr='-range %s %s'), write_short=dict(argstr='-short', xor=('write_byte', 'write_short', 'write_int', 'write_long', 'write_float', 'write_double')), write_signed=dict(argstr='-signed', xor=('write_signed', 'write_unsigned')), write_unsigned=dict(argstr='-unsigned', xor=('write_signed', 'write_unsigned')))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), input_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), nonormalize=dict(argstr='-nonormalize', xor=('normalize', 'nonormalize')), normalize=dict(argstr='-normalize', xor=('normalize', 'nonormalize')), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), output_file=dict(extensions=None, hash_files=False, keep_extension=False, name_source=['input_file'], name_template='%s.raw', position=-1), write_byte=dict(argstr='-byte', xor=('write_byte', 'write_short', 'write_int', 'write_long', 'write_float', 'write_double')), write_double=dict(argstr='-double', xor=('write_byte', 'write_short', 'write_int', 'write_long', 'write_float', 'write_double')), write_float=dict(argstr='-float', xor=('write_byte', 'write_short', 'write_int', 'write_long', 'write_float', 'write_double')), write_int=dict(argstr='-int', xor=('write_byte', 'write_short', 'write_int', 'write_long', 'write_float', 'write_double')), write_long=dict(argstr='-long', xor=('write_byte', 'write_short', 'write_int', 'write_long', 'write_float', 'write_double')), write_range=dict(argstr='-range %s %s'), write_short=dict(argstr='-short', xor=('write_byte', 'write_short', 'write_int', 'write_long', 'write_float', 'write_double')), write_signed=dict(argstr='-signed', xor=('write_signed', 'write_unsigned')), write_unsigned=dict(argstr='-unsigned', xor=('write_signed', 'write_unsigned')))
```

## Next Steps


---

*Source: test_auto_ToRaw.py:6 | Complexity: Beginner | Last updated: 2026-05-18*