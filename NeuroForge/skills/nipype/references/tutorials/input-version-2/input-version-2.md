# How To: Input Version 2

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test input version 2

## Prerequisites

**Required Modules:**
- `os`
- `simplejson`
- `logging`
- `pytest`
- `unittest`
- `testing`
- `support`
- `nipype.interfaces.ants`
- `nipype`
- `nipype`
- `nipype.interfaces.fsl`


## Step-by-Step Guide

### Step 1: Assign obj = DerivedInterface1(...)

```python
obj = DerivedInterface1()
```

**Verification:**
```python
assert 'version 0.8 < required 0.9' in str(excinfo.value)
```

### Step 2: Assign obj.inputs.foo = 1

```python
obj.inputs.foo = 1
```

**Verification:**
```python
assert 'version 0.8 < required 0.9' in str(excinfo.value)
```

### Step 3: Assign input_spec = MinVerInputSpec

```python
input_spec = MinVerInputSpec
```

### Step 4: Assign _version = '0.8'

```python
_version = '0.8'
```

### Step 5: Call obj._check_version_requirements()

```python
obj._check_version_requirements(obj.inputs)
```


## Complete Example

```python
# Workflow
class DerivedInterface1(nib.BaseInterface):
    input_spec = MinVerInputSpec
    _version = '0.8'
obj = DerivedInterface1()
obj.inputs.foo = 1
with pytest.raises(Exception) as excinfo:
    obj._check_version_requirements(obj.inputs)
assert 'version 0.8 < required 0.9' in str(excinfo.value)
```

## Next Steps


---

*Source: test_core.py:186 | Complexity: Intermediate | Last updated: 2026-05-18*