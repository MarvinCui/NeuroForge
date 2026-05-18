# How To: Input Version 5

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test input version 5

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

### Step 1: Assign obj = DerivedInterface2(...)

```python
obj = DerivedInterface2()
```

**Verification:**
```python
assert 'version 0.8 > required 0.7' in str(excinfo.value)
```

### Step 2: Assign obj.inputs.foo = 1

```python
obj.inputs.foo = 1
```

**Verification:**
```python
assert 'version 0.8 > required 0.7' in str(excinfo.value)
```

### Step 3: Assign input_spec = MaxVerInputSpec

```python
input_spec = MaxVerInputSpec
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
class DerivedInterface2(nib.BaseInterface):
    input_spec = MaxVerInputSpec
    _version = '0.8'
obj = DerivedInterface2()
obj.inputs.foo = 1
with pytest.raises(Exception) as excinfo:
    obj._check_version_requirements(obj.inputs)
assert 'version 0.8 > required 0.7' in str(excinfo.value)
```

## Next Steps


---

*Source: test_core.py:217 | Complexity: Intermediate | Last updated: 2026-05-18*