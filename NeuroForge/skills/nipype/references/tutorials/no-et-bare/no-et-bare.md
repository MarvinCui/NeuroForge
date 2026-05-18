# How To: No Et Bare

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test no et bare

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
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: Assign et = value

```python
et = os.getenv('NIPYPE_NO_ET') is None
```

**Verification:**
```python
assert res.outputs.out == et
```

### Step 2: Assign f = niu.Function(...)

```python
f = niu.Function(function=_check_no_et)
```

**Verification:**
```python
assert res.outputs.out == et
```

### Step 3: Assign res = f.run(...)

```python
res = f.run()
```

**Verification:**
```python
assert next(iter(res.nodes)).result.outputs.out == et
```

### Step 4: Assign n = pe.Node(...)

```python
n = pe.Node(niu.Function(function=_check_no_et), name='n', base_dir=str(tmp_path))
```

### Step 5: Assign res = n.run(...)

```python
res = n.run()
```

**Verification:**
```python
assert res.outputs.out == et
```

### Step 6: Assign wf1 = pe.Workflow(...)

```python
wf1 = pe.Workflow(name='wf1', base_dir=str(tmp_path))
```

### Step 7: Call wf1.add_nodes()

```python
wf1.add_nodes([pe.Node(niu.Function(function=_check_no_et), name='n')])
```

### Step 8: Assign res = wf1.run(...)

```python
res = wf1.run()
```

**Verification:**
```python
assert next(iter(res.nodes)).result.outputs.out == et
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
from unittest.mock import patch
from nipype.pipeline import engine as pe
from nipype.interfaces import utility as niu
from nipype.interfaces.base import BaseInterface
et = os.getenv('NIPYPE_NO_ET') is None
with patch.object(BaseInterface, '_etelemetry_version_data', {}):
    f = niu.Function(function=_check_no_et)
    res = f.run()
    assert res.outputs.out == et
    n = pe.Node(niu.Function(function=_check_no_et), name='n', base_dir=str(tmp_path))
    res = n.run()
    assert res.outputs.out == et
    wf1 = pe.Workflow(name='wf1', base_dir=str(tmp_path))
    wf1.add_nodes([pe.Node(niu.Function(function=_check_no_et), name='n')])
    res = wf1.run()
    assert next(iter(res.nodes)).result.outputs.out == et
```

## Next Steps


---

*Source: test_nipype.py:44 | Complexity: Advanced | Last updated: 2026-05-18*