# How To: Flow Runner

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test flow runner

## Prerequisites

**Required Modules:**
- `pathlib`
- `sys`
- `tempfile`
- `numpy.testing`
- `dipy.workflows.base`
- `dipy.workflows.flow_runner`
- `dipy.workflows.tests.workflow_tests_utils`


## Step-by-Step Guide

### Step 1: Assign old_argv = value

```python
old_argv = sys.argv
```

**Verification:**
```python
assert dcwf._force_overwrite
```

### Step 2: Assign sys.argv = value

```python
sys.argv = [sys.argv[0]]
```

**Verification:**
```python
assert dcwf._output_strategy == 'absolute'
```

### Step 3: Assign opt_keys = value

```python
opt_keys = ['param_combined', 'dwf1.param1', 'dwf2.param2', 'force', 'out_strat', 'mix_names']
```

**Verification:**
```python
assert dcwf._mix_names
```

### Step 4: Assign pos_results = value

```python
pos_results = ['dipy.txt']
```

**Verification:**
```python
assert param1 == 10
```

### Step 5: Assign opt_results = value

```python
opt_results = [30, 10, 20, True, 'absolute', True]
```

**Verification:**
```python
assert param2 == 20
```

### Step 6: Assign inputs = inputs_from_results(...)

```python
inputs = inputs_from_results(opt_results, opt_keys, optional=True)
```

**Verification:**
```python
assert combined == 30
```

### Step 7: Call inputs.extend()

```python
inputs.extend(inputs_from_results(pos_results))
```

### Step 8: Call sys.argv.extend()

```python
sys.argv.extend(inputs)
```

### Step 9: Assign dcwf = DummyCombinedWorkflow(...)

```python
dcwf = DummyCombinedWorkflow()
```

### Step 10: Assign unknown = run_flow(...)

```python
param1, param2, combined = run_flow(dcwf)
```

**Verification:**
```python
assert dcwf._force_overwrite
```

### Step 11: Assign sys.argv = old_argv

```python
sys.argv = old_argv
```


## Complete Example

```python
# Workflow
old_argv = sys.argv
sys.argv = [sys.argv[0]]
opt_keys = ['param_combined', 'dwf1.param1', 'dwf2.param2', 'force', 'out_strat', 'mix_names']
pos_results = ['dipy.txt']
opt_results = [30, 10, 20, True, 'absolute', True]
inputs = inputs_from_results(opt_results, opt_keys, optional=True)
inputs.extend(inputs_from_results(pos_results))
sys.argv.extend(inputs)
dcwf = DummyCombinedWorkflow()
param1, param2, combined = run_flow(dcwf)
assert dcwf._force_overwrite
assert dcwf._output_strategy == 'absolute'
assert dcwf._mix_names
assert param1 == 10
assert param2 == 20
assert combined == 30
sys.argv = old_argv
```

## Next Steps


---

*Source: test_iap.py:178 | Complexity: Advanced | Last updated: 2026-05-18*