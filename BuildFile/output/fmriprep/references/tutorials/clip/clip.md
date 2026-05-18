# How To: Clip

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test Clip

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `nibabel`
- `numpy`
- `nipype.pipeline`
- `fmriprep.interfaces.maths`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: Assign in_file = str(...)

```python
in_file = str(tmp_path / 'input.nii')
```

**Verification:**
```python
assert ret.outputs.out_file == str(tmp_path / 'threshold/input_clipped.nii')
```

### Step 2: Assign data = np.array(...)

```python
data = np.array([[[-1.0, 1.0], [-2.0, 2.0]]])
```

**Verification:**
```python
assert np.allclose(out_img.get_fdata(), [[[0.0, 1.0], [0.0, 2.0]]])
```

### Step 3: Call nb.Nifti1Image.to_filename()

```python
nb.Nifti1Image(data, np.eye(4)).to_filename(in_file)
```

**Verification:**
```python
assert ret.outputs.out_file == in_file
```

### Step 4: Assign threshold = pe.Node(...)

```python
threshold = pe.Node(Clip(in_file=in_file, minimum=0), name='threshold', base_dir=tmp_path)
```

**Verification:**
```python
assert np.allclose(out_img.get_fdata(), [[[-1.0, 1.0], [-2.0, 2.0]]])
```

### Step 5: Assign ret = threshold.run(...)

```python
ret = threshold.run()
```

**Verification:**
```python
assert ret.outputs.out_file == str(tmp_path / 'clip/input_clipped.nii')
```

### Step 6: Assign out_img = nb.load(...)

```python
out_img = nb.load(ret.outputs.out_file)
```

**Verification:**
```python
assert np.allclose(out_img.get_fdata(), [[[-1.0, 1.0], [-1.0, 1.0]]])
```

### Step 7: Assign threshold2 = pe.Node(...)

```python
threshold2 = pe.Node(Clip(in_file=in_file, minimum=-3), name='threshold2', base_dir=tmp_path)
```

**Verification:**
```python
assert ret.outputs.out_file == str(tmp_path / 'nonpositive/input_clipped.nii')
```

### Step 8: Assign ret = threshold2.run(...)

```python
ret = threshold2.run()
```

**Verification:**
```python
assert np.allclose(out_img.get_fdata(), [[[-1.0, 0.0], [-2.0, 0.0]]])
```

### Step 9: Assign out_img = nb.load(...)

```python
out_img = nb.load(ret.outputs.out_file)
```

**Verification:**
```python
assert np.allclose(out_img.get_fdata(), [[[-1.0, 1.0], [-2.0, 2.0]]])
```

### Step 10: Assign clip = pe.Node(...)

```python
clip = pe.Node(Clip(in_file=in_file, minimum=-1, maximum=1), name='clip', base_dir=tmp_path)
```

### Step 11: Assign ret = clip.run(...)

```python
ret = clip.run()
```

**Verification:**
```python
assert ret.outputs.out_file == str(tmp_path / 'clip/input_clipped.nii')
```

### Step 12: Assign out_img = nb.load(...)

```python
out_img = nb.load(ret.outputs.out_file)
```

**Verification:**
```python
assert np.allclose(out_img.get_fdata(), [[[-1.0, 1.0], [-1.0, 1.0]]])
```

### Step 13: Assign nonpositive = pe.Node(...)

```python
nonpositive = pe.Node(Clip(in_file=in_file, maximum=0), name='nonpositive', base_dir=tmp_path)
```

### Step 14: Assign ret = nonpositive.run(...)

```python
ret = nonpositive.run()
```

**Verification:**
```python
assert ret.outputs.out_file == str(tmp_path / 'nonpositive/input_clipped.nii')
```

### Step 15: Assign out_img = nb.load(...)

```python
out_img = nb.load(ret.outputs.out_file)
```

**Verification:**
```python
assert np.allclose(out_img.get_fdata(), [[[-1.0, 0.0], [-2.0, 0.0]]])
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
in_file = str(tmp_path / 'input.nii')
data = np.array([[[-1.0, 1.0], [-2.0, 2.0]]])
nb.Nifti1Image(data, np.eye(4)).to_filename(in_file)
threshold = pe.Node(Clip(in_file=in_file, minimum=0), name='threshold', base_dir=tmp_path)
ret = threshold.run()
assert ret.outputs.out_file == str(tmp_path / 'threshold/input_clipped.nii')
out_img = nb.load(ret.outputs.out_file)
assert np.allclose(out_img.get_fdata(), [[[0.0, 1.0], [0.0, 2.0]]])
threshold2 = pe.Node(Clip(in_file=in_file, minimum=-3), name='threshold2', base_dir=tmp_path)
ret = threshold2.run()
assert ret.outputs.out_file == in_file
out_img = nb.load(ret.outputs.out_file)
assert np.allclose(out_img.get_fdata(), [[[-1.0, 1.0], [-2.0, 2.0]]])
clip = pe.Node(Clip(in_file=in_file, minimum=-1, maximum=1), name='clip', base_dir=tmp_path)
ret = clip.run()
assert ret.outputs.out_file == str(tmp_path / 'clip/input_clipped.nii')
out_img = nb.load(ret.outputs.out_file)
assert np.allclose(out_img.get_fdata(), [[[-1.0, 1.0], [-1.0, 1.0]]])
nonpositive = pe.Node(Clip(in_file=in_file, maximum=0), name='nonpositive', base_dir=tmp_path)
ret = nonpositive.run()
assert ret.outputs.out_file == str(tmp_path / 'nonpositive/input_clipped.nii')
out_img = nb.load(ret.outputs.out_file)
assert np.allclose(out_img.get_fdata(), [[[-1.0, 0.0], [-2.0, 0.0]]])
```

## Next Steps


---

*Source: test_maths.py:8 | Complexity: Advanced | Last updated: 2026-05-18*