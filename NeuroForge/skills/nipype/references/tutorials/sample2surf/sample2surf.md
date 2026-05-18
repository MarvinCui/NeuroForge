# How To: Sample2Surf

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test sample2surf

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `os.path`
- `pytest`
- `nipype.testing.fixtures`
- `nipype.pipeline`
- `nipype.interfaces`
- `nipype.interfaces.base`
- `nipype.interfaces.io`

**Setup Required:**
```python
# Fixtures: create_files_in_directory_plus_dummy_file
```

## Step-by-Step Guide

### Step 1: Assign s2s = fs.SampleToSurface(...)

```python
s2s = fs.SampleToSurface()
```

**Verification:**
```python
assert s2s.cmd == 'mri_vol2surf'
```

### Step 2: Assign unknown = create_files_in_directory_plus_dummy_file

```python
files, cwd = create_files_in_directory_plus_dummy_file
```

**Verification:**
```python
assert s2s.cmdline == 'mri_vol2surf --hemi lh --o %s --ref %s --reg reg.dat --projfrac 0.500 --mov %s' % (os.path.join(cwd, 'lh.a.mgz'), files[1], files[0])
```

### Step 3: Assign s2s.inputs.source_file = value

```python
s2s.inputs.source_file = files[0]
```

**Verification:**
```python
assert s2s != s2sish
```

### Step 4: Assign s2s.inputs.reference_file = value

```python
s2s.inputs.reference_file = files[1]
```

**Verification:**
```python
assert s2s._get_outfilename('hits_file') == os.path.join(cwd, 'lh.a_hits.mgz')
```

### Step 5: Assign s2s.inputs.hemi = 'lh'

```python
s2s.inputs.hemi = 'lh'
```

### Step 6: Assign s2s.inputs.reg_file = value

```python
s2s.inputs.reg_file = files[2]
```

### Step 7: Assign s2s.inputs.sampling_range = 0.5

```python
s2s.inputs.sampling_range = 0.5
```

### Step 8: Assign s2s.inputs.sampling_units = 'frac'

```python
s2s.inputs.sampling_units = 'frac'
```

### Step 9: Assign s2s.inputs.sampling_method = 'point'

```python
s2s.inputs.sampling_method = 'point'
```

**Verification:**
```python
assert s2s.cmdline == 'mri_vol2surf --hemi lh --o %s --ref %s --reg reg.dat --projfrac 0.500 --mov %s' % (os.path.join(cwd, 'lh.a.mgz'), files[1], files[0])
```

### Step 10: Assign s2sish = fs.SampleToSurface(...)

```python
s2sish = fs.SampleToSurface(source_file=files[1], reference_file=files[0], hemi='rh')
```

**Verification:**
```python
assert s2s != s2sish
```

### Step 11: Assign s2s.inputs.hits_file = True

```python
s2s.inputs.hits_file = True
```

**Verification:**
```python
assert s2s._get_outfilename('hits_file') == os.path.join(cwd, 'lh.a_hits.mgz')
```

### Step 12: Call s2s.run()

```python
s2s.run()
```

### Step 13: Assign s2s.inputs.sampling_range = value

```python
s2s.inputs.sampling_range = (0.2, 0.5)
```

### Step 14: Call set_illegal_range()

```python
set_illegal_range()
```


## Complete Example

```python
# Setup
# Fixtures: create_files_in_directory_plus_dummy_file

# Workflow
s2s = fs.SampleToSurface()
assert s2s.cmd == 'mri_vol2surf'
with pytest.raises(ValueError):
    s2s.run()
files, cwd = create_files_in_directory_plus_dummy_file
s2s.inputs.source_file = files[0]
s2s.inputs.reference_file = files[1]
s2s.inputs.hemi = 'lh'
s2s.inputs.reg_file = files[2]
s2s.inputs.sampling_range = 0.5
s2s.inputs.sampling_units = 'frac'
s2s.inputs.sampling_method = 'point'
assert s2s.cmdline == 'mri_vol2surf --hemi lh --o %s --ref %s --reg reg.dat --projfrac 0.500 --mov %s' % (os.path.join(cwd, 'lh.a.mgz'), files[1], files[0])
s2sish = fs.SampleToSurface(source_file=files[1], reference_file=files[0], hemi='rh')
assert s2s != s2sish
s2s.inputs.hits_file = True
assert s2s._get_outfilename('hits_file') == os.path.join(cwd, 'lh.a_hits.mgz')

def set_illegal_range():
    s2s.inputs.sampling_range = (0.2, 0.5)
with pytest.raises(TraitError):
    set_illegal_range()
```

## Next Steps


---

*Source: test_utils.py:18 | Complexity: Advanced | Last updated: 2026-05-18*