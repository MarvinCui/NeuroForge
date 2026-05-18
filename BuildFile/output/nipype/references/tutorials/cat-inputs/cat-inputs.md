# How To: Cat Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Cat inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_files=dict(argstr='%s', mandatory=True, position=-2), keepfree=dict(argstr='-nonfixed'), num_threads=dict(nohash=True, usedefault=True), omitconst=dict(argstr='-nonconst'), out_cint=dict(xor=['out_format', 'out_nice', 'out_double', 'out_fint', 'out_int']), out_double=dict(argstr='-d', xor=['out_format', 'out_nice', 'out_int', 'out_fint', 'out_cint']), out_file=dict(argstr='> %s', extensions=None, mandatory=True, position=-1, usedefault=True), out_fint=dict(argstr='-f', xor=['out_format', 'out_nice', 'out_double', 'out_int', 'out_cint']), out_format=dict(argstr='-form %s', xor=['out_int', 'out_nice', 'out_double', 'out_fint', 'out_cint']), out_int=dict(argstr='-i', xor=['out_format', 'out_nice', 'out_double', 'out_fint', 'out_cint']), out_nice=dict(argstr='-n', xor=['out_format', 'out_int', 'out_double', 'out_fint', 'out_cint']), outputtype=dict(), sel=dict(argstr='-sel %s'), stack=dict(argstr='-stack'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_files=dict(argstr='%s', mandatory=True, position=-2), keepfree=dict(argstr='-nonfixed'), num_threads=dict(nohash=True, usedefault=True), omitconst=dict(argstr='-nonconst'), out_cint=dict(xor=['out_format', 'out_nice', 'out_double', 'out_fint', 'out_int']), out_double=dict(argstr='-d', xor=['out_format', 'out_nice', 'out_int', 'out_fint', 'out_cint']), out_file=dict(argstr='> %s', extensions=None, mandatory=True, position=-1, usedefault=True), out_fint=dict(argstr='-f', xor=['out_format', 'out_nice', 'out_double', 'out_int', 'out_cint']), out_format=dict(argstr='-form %s', xor=['out_int', 'out_nice', 'out_double', 'out_fint', 'out_cint']), out_int=dict(argstr='-i', xor=['out_format', 'out_nice', 'out_double', 'out_fint', 'out_cint']), out_nice=dict(argstr='-n', xor=['out_format', 'out_int', 'out_double', 'out_fint', 'out_cint']), outputtype=dict(), sel=dict(argstr='-sel %s'), stack=dict(argstr='-stack'))
```

## Next Steps


---

*Source: test_auto_Cat.py:6 | Complexity: Beginner | Last updated: 2026-05-18*