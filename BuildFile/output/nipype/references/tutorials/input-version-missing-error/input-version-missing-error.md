# How To: Input Version Missing Error

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: unittest, mock, workflow, integration

## Overview

Workflow: test input version missing error

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: caplog
```

## Step-by-Step Guide

### Step 1: Assign obj1 = DerivedInterface(...)

```python
obj1 = DerivedInterface(foo=1)
```

**Verification:**
```python
assert len(caplog.records) == 2
```

### Step 2: Assign obj2 = DerivedInterface(...)

```python
obj2 = DerivedInterface(bar=1)
```

**Verification:**
```python
assert len(caplog.records) == 2
```

### Step 3: Assign _version = 'misparsed-garbage'

```python
_version = 'misparsed-garbage'
```

### Step 4: Assign foo = nib.traits.Int(...)

```python
foo = nib.traits.Int(min_ver='0.9')
```

### Step 5: Assign bar = nib.traits.Int(...)

```python
bar = nib.traits.Int(max_ver='0.9')
```

### Step 6: Call obj1._check_version_requirements()

```python
obj1._check_version_requirements(obj1.inputs)
```

### Step 7: Call obj2._check_version_requirements()

```python
obj2._check_version_requirements(obj2.inputs)
```


## Complete Example

```python
# Setup
# Fixtures: caplog

# Workflow
from nipype import config

class DerivedInterface(nib.BaseInterface):

    class input_spec(nib.TraitedSpec):
        foo = nib.traits.Int(min_ver='0.9')
        bar = nib.traits.Int(max_ver='0.9')
    _version = 'misparsed-garbage'
obj1 = DerivedInterface(foo=1)
obj2 = DerivedInterface(bar=1)
with caplog.at_level(logging.WARNING, logger='nipype.interface'):
    with mock.patch.object(config, 'getboolean', return_value=True):
        with pytest.raises(ValueError):
            obj1._check_version_requirements(obj1.inputs)
        with pytest.raises(ValueError):
            obj2._check_version_requirements(obj2.inputs)
assert len(caplog.records) == 2
```

## Next Steps


---

*Source: test_core.py:255 | Complexity: Intermediate | Last updated: 2026-05-18*