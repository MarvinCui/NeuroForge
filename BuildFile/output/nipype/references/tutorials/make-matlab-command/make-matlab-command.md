# How To: Make Matlab Command

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test make matlab command

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: create_files_in_directory
```

## Step-by-Step Guide

### Step 1: Assign dc = TestClass(...)

```python
dc = TestClass()
```

**Verification:**
```python
assert 'jobs{1}.spm.jobtype.jobname.contents(3) = 3;' in script
```

### Step 2: Assign unknown = create_files_in_directory

```python
filelist, outdir = create_files_in_directory
```

**Verification:**
```python
assert 'jobs{1}.jobtype{1}.jobname{1}.contents(3) = 3;' in script
```

### Step 3: Assign contents = value

```python
contents = {'contents': [1, 2, 3, 4]}
```

### Step 4: Assign script = dc._make_matlab_command(...)

```python
script = dc._make_matlab_command([contents])
```

**Verification:**
```python
assert 'jobs{1}.spm.jobtype.jobname.contents(3) = 3;' in script
```

### Step 5: Assign dc.inputs.use_v8struct = False

```python
dc.inputs.use_v8struct = False
```

### Step 6: Assign script = dc._make_matlab_command(...)

```python
script = dc._make_matlab_command([contents])
```

**Verification:**
```python
assert 'jobs{1}.jobtype{1}.jobname{1}.contents(3) = 3;' in script
```

### Step 7: Assign _jobtype = 'jobtype'

```python
_jobtype = 'jobtype'
```

### Step 8: Assign _jobname = 'jobname'

```python
_jobname = 'jobname'
```

### Step 9: Assign input_spec = value

```python
input_spec = spm.SPMCommandInputSpec
```


## Complete Example

```python
# Setup
# Fixtures: create_files_in_directory

# Workflow
class TestClass(spm.SPMCommand):
    _jobtype = 'jobtype'
    _jobname = 'jobname'
    input_spec = spm.SPMCommandInputSpec
dc = TestClass()
filelist, outdir = create_files_in_directory
contents = {'contents': [1, 2, 3, 4]}
script = dc._make_matlab_command([contents])
assert 'jobs{1}.spm.jobtype.jobname.contents(3) = 3;' in script
dc.inputs.use_v8struct = False
script = dc._make_matlab_command([contents])
assert 'jobs{1}.jobtype{1}.jobname{1}.contents(3) = 3;' in script
```

## Next Steps


---

*Source: test_base.py:153 | Complexity: Advanced | Last updated: 2026-05-18*