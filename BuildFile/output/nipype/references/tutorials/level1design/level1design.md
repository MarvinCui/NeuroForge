# How To: Level1Design

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test level1design

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `base`
- `model`

**Setup Required:**
```python
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: Assign old = tmpdir.chdir(...)

```python
old = tmpdir.chdir()
```

**Verification:**
```python
assert f'set fmri(convolve1) {val}' in output_txt
```

### Step 2: Assign l = Level1Design(...)

```python
l = Level1Design()
```

### Step 3: Assign runinfo = dict(...)

```python
runinfo = dict(cond=[{'name': 'test_condition', 'onset': [0, 10], 'duration': [10, 10]}], regress=[])
```

### Step 4: Assign runidx = 0

```python
runidx = 0
```

### Step 5: Assign contrasts = Undefined

```python
contrasts = Undefined
```

### Step 6: Assign do_tempfilter = False

```python
do_tempfilter = False
```

### Step 7: Assign orthogonalization = value

```python
orthogonalization = {}
```

### Step 8: Assign basic_ev_parameters = value

```python
basic_ev_parameters = {'temporalderiv': False}
```

### Step 9: Assign convolution_variants = value

```python
convolution_variants = [('custom', 7, {'temporalderiv': False, 'bfcustompath': '/some/path'}), ('hrf', 3, basic_ev_parameters), ('dgamma', 3, basic_ev_parameters), ('gamma', 2, basic_ev_parameters), ('none', 0, basic_ev_parameters)]
```

### Step 10: Assign unknown = Level1Design._create_ev_files(...)

```python
output_num, output_txt = Level1Design._create_ev_files(l, os.getcwd(), runinfo, runidx, ev_parameters, orthogonalization, contrasts, do_tempfilter, key)
```

**Verification:**
```python
assert f'set fmri(convolve1) {val}' in output_txt
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
old = tmpdir.chdir()
l = Level1Design()
runinfo = dict(cond=[{'name': 'test_condition', 'onset': [0, 10], 'duration': [10, 10]}], regress=[])
runidx = 0
contrasts = Undefined
do_tempfilter = False
orthogonalization = {}
basic_ev_parameters = {'temporalderiv': False}
convolution_variants = [('custom', 7, {'temporalderiv': False, 'bfcustompath': '/some/path'}), ('hrf', 3, basic_ev_parameters), ('dgamma', 3, basic_ev_parameters), ('gamma', 2, basic_ev_parameters), ('none', 0, basic_ev_parameters)]
for key, val, ev_parameters in convolution_variants:
    output_num, output_txt = Level1Design._create_ev_files(l, os.getcwd(), runinfo, runidx, ev_parameters, orthogonalization, contrasts, do_tempfilter, key)
    assert f'set fmri(convolve1) {val}' in output_txt
```

## Next Steps


---

*Source: test_Level1Design_functions.py:6 | Complexity: Advanced | Last updated: 2026-05-18*