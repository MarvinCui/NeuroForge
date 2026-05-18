# How To: Bool

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test bool

## Prerequisites

**Required Modules:**
- `os`
- `numpy`
- `pytest`
- `nipype.testing.fixtures`
- `nipype.interfaces.spm.base`
- `nipype.interfaces.spm`
- `nipype.interfaces.matlab`
- `nipype.interfaces.spm.base`
- `nipype.interfaces.base`


## Step-by-Step Guide

### Step 1: Assign dc = TestClass(...)

```python
dc = TestClass()
```

**Verification:**
```python
assert out.find('jobs{1}.spm.jobtype.jobname.testfield = 1;') > 0, 1
```

### Step 2: Assign dc.inputs.test_in = True

```python
dc.inputs.test_in = True
```

**Verification:**
```python
assert out.find('jobs{1}.jobtype{1}.jobname{1}.testfield = 1;') > 0, 1
```

### Step 3: Assign out = dc._make_matlab_command(...)

```python
out = dc._make_matlab_command(dc._parse_inputs())
```

**Verification:**
```python
assert out.find('jobs{1}.spm.jobtype.jobname.testfield = 1;') > 0, 1
```

### Step 4: Assign dc.inputs.use_v8struct = False

```python
dc.inputs.use_v8struct = False
```

### Step 5: Assign out = dc._make_matlab_command(...)

```python
out = dc._make_matlab_command(dc._parse_inputs())
```

**Verification:**
```python
assert out.find('jobs{1}.jobtype{1}.jobname{1}.testfield = 1;') > 0, 1
```

### Step 6: Assign test_in, include_intercept = traits.Bool(...)

```python
test_in = include_intercept = traits.Bool(field='testfield')
```

### Step 7: Assign input_spec = TestClassInputSpec

```python
input_spec = TestClassInputSpec
```

### Step 8: Assign _jobtype = 'jobtype'

```python
_jobtype = 'jobtype'
```

### Step 9: Assign _jobname = 'jobname'

```python
_jobname = 'jobname'
```


## Complete Example

```python
# Workflow
class TestClassInputSpec(SPMCommandInputSpec):
    test_in = include_intercept = traits.Bool(field='testfield')

class TestClass(spm.SPMCommand):
    input_spec = TestClassInputSpec
    _jobtype = 'jobtype'
    _jobname = 'jobname'
dc = TestClass()
dc.inputs.test_in = True
out = dc._make_matlab_command(dc._parse_inputs())
assert out.find('jobs{1}.spm.jobtype.jobname.testfield = 1;') > 0, 1
dc.inputs.use_v8struct = False
out = dc._make_matlab_command(dc._parse_inputs())
assert out.find('jobs{1}.jobtype{1}.jobname{1}.testfield = 1;') > 0, 1
```

## Next Steps


---

*Source: test_base.py:135 | Complexity: Advanced | Last updated: 2026-05-18*