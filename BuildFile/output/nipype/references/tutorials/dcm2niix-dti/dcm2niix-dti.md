# How To: Dcm2Niix Dti

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test dcm2niix dti

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `pytest`
- `nipype.interfaces.dcm2nii`
- `datalad`
- `datalad.support.exceptions`

**Setup Required:**
```python
# Fixtures: fetch_data, tmpdir
```

## Step-by-Step Guide

### Step 1: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

**Verification:**
```python
assert res.outputs.converted_files
```

### Step 2: Assign datadir = value

```python
datadir = tmpdir.mkdir('data').strpath
```

**Verification:**
```python
assert res.outputs.bvals
```

### Step 3: Assign dicoms = fetch_data(...)

```python
dicoms = fetch_data(datadir, 'Siemens_Sag_DTI_20160825_145811')
```

**Verification:**
```python
assert res.outputs.bvecs
```

### Step 4: Assign dcm = Dcm2niix(...)

```python
dcm = Dcm2niix()
```

**Verification:**
```python
assert len(set(map(len, outputs))) == 1
```

### Step 5: Assign dcm.inputs.source_dir = dicoms

```python
dcm.inputs.source_dir = dicoms
```

**Verification:**
```python
assert not res.outputs.bids
```

### Step 6: Assign dcm.inputs.out_filename = '%u%z'

```python
dcm.inputs.out_filename = '%u%z'
```

**Verification:**
```python
assert_dti(dcm.run())
```

### Step 7: Call assert_dti()

```python
assert_dti(dcm.run())
```

**Verification:**
```python
assert_dti(dcm.run())
```

### Step 8: Assign outdir = value

```python
outdir = tmpdir.mkdir('conversion').strpath
```

### Step 9: Assign dcm.inputs.output_dir = outdir

```python
dcm.inputs.output_dir = outdir
```

### Step 10: Assign dcm.inputs.bids_format = False

```python
dcm.inputs.bids_format = False
```

### Step 11: Call assert_dti()

```python
assert_dti(dcm.run())
```

### Step 12: """Some assertions we will make"""

```python
"""Some assertions we will make"""
```

**Verification:**
```python
assert res.outputs.converted_files
```

### Step 13: Assign outputs = value

```python
outputs = [y for x, y in res.outputs.get().items()]
```

**Verification:**
```python
assert len(set(map(len, outputs))) == 1
```


## Complete Example

```python
# Setup
# Fixtures: fetch_data, tmpdir

# Workflow
tmpdir.chdir()
datadir = tmpdir.mkdir('data').strpath
dicoms = fetch_data(datadir, 'Siemens_Sag_DTI_20160825_145811')

def assert_dti(res):
    """Some assertions we will make"""
    assert res.outputs.converted_files
    assert res.outputs.bvals
    assert res.outputs.bvecs
    outputs = [y for x, y in res.outputs.get().items()]
    if res.inputs.get('bids_format'):
        assert len(set(map(len, outputs))) == 1
    else:
        assert not res.outputs.bids
dcm = Dcm2niix()
dcm.inputs.source_dir = dicoms
dcm.inputs.out_filename = '%u%z'
assert_dti(dcm.run())
outdir = tmpdir.mkdir('conversion').strpath
dcm.inputs.output_dir = outdir
dcm.inputs.bids_format = False
assert_dti(dcm.run())
```

## Next Steps


---

*Source: test_extra_dcm2nii.py:34 | Complexity: Advanced | Last updated: 2026-05-18*