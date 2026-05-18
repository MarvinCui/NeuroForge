# How To: Ants Mand

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test ants mand

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `nipype.interfaces.ants`
- `os`
- `pytest`

**Setup Required:**
```python
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

**Verification:**
```python
assert "ANTS requires a value for input 'radius'" in str(er.value)
```

### Step 2: Assign filepath = os.path.dirname(...)

```python
filepath = os.path.dirname(os.path.realpath(__file__))
```

### Step 3: Assign datadir = os.path.realpath(...)

```python
datadir = os.path.realpath(os.path.join(filepath, '../../../testing/data'))
```

### Step 4: Assign ants = registration.ANTS(...)

```python
ants = registration.ANTS()
```

### Step 5: Assign ants.inputs.transformation_model = 'SyN'

```python
ants.inputs.transformation_model = 'SyN'
```

### Step 6: Assign ants.inputs.moving_image = value

```python
ants.inputs.moving_image = [os.path.join(datadir, 'resting.nii')]
```

### Step 7: Assign ants.inputs.fixed_image = value

```python
ants.inputs.fixed_image = [os.path.join(datadir, 'T1.nii')]
```

### Step 8: Assign ants.inputs.metric = value

```python
ants.inputs.metric = ['MI']
```

**Verification:**
```python
assert "ANTS requires a value for input 'radius'" in str(er.value)
```

### Step 9: Call ants.run()

```python
ants.run()
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
tmpdir.chdir()
filepath = os.path.dirname(os.path.realpath(__file__))
datadir = os.path.realpath(os.path.join(filepath, '../../../testing/data'))
ants = registration.ANTS()
ants.inputs.transformation_model = 'SyN'
ants.inputs.moving_image = [os.path.join(datadir, 'resting.nii')]
ants.inputs.fixed_image = [os.path.join(datadir, 'T1.nii')]
ants.inputs.metric = ['MI']
with pytest.raises(ValueError) as er:
    ants.run()
assert "ANTS requires a value for input 'radius'" in str(er.value)
```

## Next Steps


---

*Source: test_extra_Registration.py:8 | Complexity: Advanced | Last updated: 2026-05-18*