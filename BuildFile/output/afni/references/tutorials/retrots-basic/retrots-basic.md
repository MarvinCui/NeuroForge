# How To: Retrots Basic

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test RetroTS basic

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
kwargs_log = {'append_to_ignored': ['Clock time', 'but max simulated alpha=']}
```

### Step 3: Assign out_prefix = value

```python
out_prefix = data.outdir / f'reg.01.a.{vol_tr}'
```

### Step 4: Assign cmd = '\n    RetroTS.py\n        -c {data.ECG_epiRTslt_scan_4}\n        -r {data.Resp_epiRTslt_scan_4}\n        -v {vol_tr}\n        -p 50\n        -n 30\n        -prefix {out_prefix}\n    '

```python
cmd = '\n    RetroTS.py\n        -c {data.ECG_epiRTslt_scan_4}\n        -r {data.Resp_epiRTslt_scan_4}\n        -v {vol_tr}\n        -p 50\n        -n 30\n        -prefix {out_prefix}\n    '
```

### Step 5: Assign cmd = unknown.join(...)

```python
cmd = ' '.join(cmd.format(**locals()).split())
```

### Step 6: Assign differ = tools.OutputDiffer(...)

```python
differ = tools.OutputDiffer(data, cmd, python_interpreter=python_interpreter, kwargs_1d={'all_close_kwargs': {'rtol': 0.15}})
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
kwargs_log = {'append_to_ignored': ['Clock time', 'but max simulated alpha=']}
out_prefix = data.outdir / f'reg.01.a.{vol_tr}'
cmd = '\n    RetroTS.py\n        -c {data.ECG_epiRTslt_scan_4}\n        -r {data.Resp_epiRTslt_scan_4}\n        -v {vol_tr}\n        -p 50\n        -n 30\n        -prefix {out_prefix}\n    '
cmd = ' '.join(cmd.format(**locals()).split())
differ = tools.OutputDiffer(data, cmd, python_interpreter=python_interpreter, kwargs_1d={'all_close_kwargs': {'rtol': 0.15}})
differ.run(timeout=None)
```

## Next Steps


---

*Source: test_RetroTS.py:14 | Complexity: Intermediate | Last updated: 2026-05-18*