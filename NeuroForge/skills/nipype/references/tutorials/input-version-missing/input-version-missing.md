# How To: Input Version Missing

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test input version missing

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

### Step 1: Assign obj = DerivedInterface(...)

```python
obj = DerivedInterface()
```

**Verification:**
```python
assert len(caplog.records) == 2
```

### Step 2: Assign obj.inputs.foo = 1

```python
obj.inputs.foo = 1
```

### Step 3: Assign obj.inputs.bar = 1

```python
obj.inputs.bar = 1
```

**Verification:**
```python
assert len(caplog.records) == 2
```

### Step 4: Assign _version = 'misparsed-garbage'

```python
_version = 'misparsed-garbage'
```

### Step 5: Call obj._check_version_requirements()

```python
obj._check_version_requirements(obj.inputs)
```

### Step 6: Assign foo = nib.traits.Int(...)

```python
foo = nib.traits.Int(min_ver='0.9')
```

### Step 7: Assign bar = nib.traits.Int(...)

```python
bar = nib.traits.Int(max_ver='0.9')
```


## Complete Example

```python
# Setup
# Fixtures: caplog

# Workflow
class DerivedInterface(nib.BaseInterface):

    class input_spec(nib.TraitedSpec):
        foo = nib.traits.Int(min_ver='0.9')
        bar = nib.traits.Int(max_ver='0.9')
    _version = 'misparsed-garbage'
obj = DerivedInterface()
obj.inputs.foo = 1
obj.inputs.bar = 1
with caplog.at_level(logging.WARNING, logger='nipype.interface'):
    obj._check_version_requirements(obj.inputs)
assert len(caplog.records) == 2
```

## Next Steps


---

*Source: test_core.py:239 | Complexity: Intermediate | Last updated: 2026-05-18*