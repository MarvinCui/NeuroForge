# How To: Proj Thresh

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test Proj thresh

## Prerequisites

**Required Modules:**
- `os`
- `nipype.interfaces.fsl.dti`
- `nipype.interfaces.fsl`
- `nipype.interfaces.base`
- `pytest`
- `nipype.testing.fixtures`


## Step-by-Step Guide

### Step 1: Assign proj = fsl.ProjThresh(...)

```python
proj = fsl.ProjThresh()
```

**Verification:**
```python
assert proj.cmd == 'proj_thresh'
```

### Step 2: Assign proj.inputs.volumes = value

```python
proj.inputs.volumes = ['vol1', 'vol2', 'vol3']
```

**Verification:**
```python
assert proj.cmdline == 'proj_thresh vol1 vol2 vol3 3'
```

### Step 3: Assign proj.inputs.threshold = 3

```python
proj.inputs.threshold = 3
```

**Verification:**
```python
assert proj2.cmdline == 'proj_thresh vola volb 10'
```

### Step 4: Assign proj2 = fsl.ProjThresh(...)

```python
proj2 = fsl.ProjThresh(threshold=10, volumes=['vola', 'volb'])
```

**Verification:**
```python
assert results.runtime.cmdline == 'proj_thresh inp1 inp3 inp2 2'
```

### Step 5: Assign proj3 = fsl.ProjThresh(...)

```python
proj3 = fsl.ProjThresh()
```

**Verification:**
```python
assert results.runtime.returncode != 0
```

### Step 6: Assign results = proj3.run(...)

```python
results = proj3.run(volumes=['inp1', 'inp3', 'inp2'], threshold=2)
```

**Verification:**
```python
assert isinstance(results.interface.inputs.volumes, list)
```

### Step 7: Call proj.run()

```python
proj.run()
```

**Verification:**
```python
assert results.interface.inputs.threshold == 2
```


## Complete Example

```python
# Workflow
proj = fsl.ProjThresh()
assert proj.cmd == 'proj_thresh'
with pytest.raises(ValueError):
    proj.run()
proj.inputs.volumes = ['vol1', 'vol2', 'vol3']
proj.inputs.threshold = 3
assert proj.cmdline == 'proj_thresh vol1 vol2 vol3 3'
proj2 = fsl.ProjThresh(threshold=10, volumes=['vola', 'volb'])
assert proj2.cmdline == 'proj_thresh vola volb 10'
proj3 = fsl.ProjThresh()
results = proj3.run(volumes=['inp1', 'inp3', 'inp2'], threshold=2)
assert results.runtime.cmdline == 'proj_thresh inp1 inp3 inp2 2'
assert results.runtime.returncode != 0
assert isinstance(results.interface.inputs.volumes, list)
assert results.interface.inputs.threshold == 2
```

## Next Steps


---

*Source: test_dti.py:201 | Complexity: Intermediate | Last updated: 2026-05-18*