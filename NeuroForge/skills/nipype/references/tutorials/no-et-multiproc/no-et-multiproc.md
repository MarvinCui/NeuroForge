# How To: No Et Multiproc

**Difficulty**: Advanced
**Estimated Time**: 10 minutes
**Tags**: pytest, mock, workflow, integration

## Overview

Workflow: test no et multiproc

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `info`
- `pytest`
- `os`
- `unittest.mock`
- `unittest.mock`
- `nipype.pipeline`
- `nipype.interfaces`
- `nipype.interfaces.base`
- `unittest.mock`
- `nipype.pipeline`
- `nipype.interfaces`
- `nipype.interfaces.base`
- `nipype.interfaces.base`

**Setup Required:**
```python
# Fixtures: tmp_path, plugin, run_without_submitting
```

## Step-by-Step Guide

### Step 1: Assign et = value

```python
et = os.getenv('NIPYPE_NO_ET') is None
```

**Verification:**
```python
assert next(iter(res.nodes)).result.outputs.out is expectation
```

### Step 2: Assign expectation = value

```python
expectation = et if run_without_submitting else False
```

### Step 3: Assign wf = pe.Workflow(...)

```python
wf = pe.Workflow(name='wf2', base_dir=str(tmp_path))
```

### Step 4: Assign n = pe.Node(...)

```python
n = pe.Node(niu.Function(function=_check_no_et), run_without_submitting=run_without_submitting, name='n')
```

### Step 5: Call wf.add_nodes()

```python
wf.add_nodes([n])
```

### Step 6: Assign res = wf.run(...)

```python
res = wf.run(plugin=plugin, plugin_args={'n_procs': 1})
```

**Verification:**
```python
assert next(iter(res.nodes)).result.outputs.out is expectation
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, plugin, run_without_submitting

# Workflow
from unittest.mock import patch
from nipype.pipeline import engine as pe
from nipype.interfaces import utility as niu
from nipype.interfaces.base import BaseInterface
et = os.getenv('NIPYPE_NO_ET') is None
expectation = et if run_without_submitting else False
with patch.object(BaseInterface, '_etelemetry_version_data', {}):
    wf = pe.Workflow(name='wf2', base_dir=str(tmp_path))
    n = pe.Node(niu.Function(function=_check_no_et), run_without_submitting=run_without_submitting, name='n')
    wf.add_nodes([n])
    res = wf.run(plugin=plugin, plugin_args={'n_procs': 1})
    assert next(iter(res.nodes)).result.outputs.out is expectation
```

## Next Steps


---

*Source: test_nipype.py:75 | Complexity: Advanced | Last updated: 2026-05-18*