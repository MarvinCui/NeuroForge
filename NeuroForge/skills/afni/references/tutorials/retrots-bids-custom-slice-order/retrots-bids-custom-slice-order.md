# How To: Retrots Bids Custom Slice Order

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test RetroTS bids custom slice order

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `afni_test_utils`
- `pytest`

**Setup Required:**
```python
# Fixtures: data, vol_tr, python_interpreter
```

## Step-by-Step Guide

### Step 1: Assign seedval = 31416

```python
seedval = 31416
```

### Step 2: Assign kwargs_log = value

```python
kwargs_log = {'append_to_ignored': ['applying custom slice timing']}
```

### Step 3: Assign out_prefix = value

```python
out_prefix = data.outdir / f'reg.02.a.{vol_tr}'
```

### Step 4: Assign cmd = '\n    RetroTS.py\n        -phys_file {data.epiRTslt_scan_4_bids}\n        -v {vol_tr}\n        -n 1\n        -p 50\n        -slice_order custom\n        -slice_offset [1000]\n        -prefix {out_prefix}\n    '

```python
cmd = '\n    RetroTS.py\n        -phys_file {data.epiRTslt_scan_4_bids}\n        -v {vol_tr}\n        -n 1\n        -p 50\n        -slice_order custom\n        -slice_offset [1000]\n        -prefix {out_prefix}\n    '
```

### Step 5: Assign cmd = unknown.join(...)

```python
cmd = ' '.join(cmd.format(**locals()).split())
```

### Step 6: Assign differ = tools.OutputDiffer(...)

```python
differ = tools.OutputDiffer(data, cmd, python_interpreter=python_interpreter, kwargs_1d={'all_close_kwargs': {'rtol': 0.15}}, kwargs_log=kwargs_log)
```

### Step 7: Call differ.run()

```python
differ.run(timeout=None)
```


## Complete Example

```python
# Setup
# Fixtures: data, vol_tr, python_interpreter

# Workflow
seedval = 31416
kwargs_log = {'append_to_ignored': ['applying custom slice timing']}
out_prefix = data.outdir / f'reg.02.a.{vol_tr}'
cmd = '\n    RetroTS.py\n        -phys_file {data.epiRTslt_scan_4_bids}\n        -v {vol_tr}\n        -n 1\n        -p 50\n        -slice_order custom\n        -slice_offset [1000]\n        -prefix {out_prefix}\n    '
cmd = ' '.join(cmd.format(**locals()).split())
differ = tools.OutputDiffer(data, cmd, python_interpreter=python_interpreter, kwargs_1d={'all_close_kwargs': {'rtol': 0.15}}, kwargs_log=kwargs_log)
differ.run(timeout=None)
```

## Next Steps


---

*Source: test_RetroTS.py:80 | Complexity: Intermediate | Last updated: 2026-05-18*