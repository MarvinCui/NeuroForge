# How To: Concatenate

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test concatenate

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `nibabel`
- `pytest`
- `nipype.interfaces.freesurfer`
- `nipype.pipeline.engine`

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
assert res.outputs.concatenated_file == tmpdir.join('concat_output.nii.gz').strpath
```

### Step 2: Assign in1 = value

```python
in1 = tmpdir.join('cont1.nii').strpath
```

**Verification:**
```python
assert np.allclose(nb.load('concat_output.nii.gz').get_fdata(), out_data)
```

### Step 3: Assign in2 = value

```python
in2 = tmpdir.join('cont2.nii').strpath
```

**Verification:**
```python
assert res.outputs.concatenated_file == tmpdir.join(out).strpath
```

### Step 4: Assign out = 'bar.nii'

```python
out = 'bar.nii'
```

**Verification:**
```python
assert np.allclose(nb.load(out).get_fdata(), out_data)
```

### Step 5: Assign data1 = np.zeros(...)

```python
data1 = np.zeros((3, 3, 3, 1), dtype=np.float32)
```

**Verification:**
```python
assert np.allclose(nb.load(tmpdir.join('test_concatenate', 'concat', out).strpath).get_fdata(), out_data)
```

### Step 6: Assign data2 = np.ones(...)

```python
data2 = np.ones((3, 3, 3, 5), dtype=np.float32)
```

**Verification:**
```python
assert np.allclose(nb.load(out).get_fdata(), mean_data)
```

### Step 7: Assign out_data = np.concatenate(...)

```python
out_data = np.concatenate((data1, data2), axis=3)
```

### Step 8: Assign mean_data = np.mean(...)

```python
mean_data = np.mean(out_data, axis=3)
```

### Step 9: Call nb.Nifti1Image.to_filename()

```python
nb.Nifti1Image(data1, affine=np.eye(4)).to_filename(in1)
```

### Step 10: Call nb.Nifti1Image.to_filename()

```python
nb.Nifti1Image(data2, affine=np.eye(4)).to_filename(in2)
```

### Step 11: Assign res = model.Concatenate.run(...)

```python
res = model.Concatenate(in_files=[in1, in2]).run()
```

**Verification:**
```python
assert res.outputs.concatenated_file == tmpdir.join('concat_output.nii.gz').strpath
```

### Step 12: Assign res = model.Concatenate.run(...)

```python
res = model.Concatenate(in_files=[in1, in2], concatenated_file=out).run()
```

**Verification:**
```python
assert res.outputs.concatenated_file == tmpdir.join(out).strpath
```

### Step 13: Assign wf = pe.Workflow(...)

```python
wf = pe.Workflow('test_concatenate', base_dir=tmpdir.strpath)
```

### Step 14: Assign concat = pe.Node(...)

```python
concat = pe.Node(model.Concatenate(in_files=[in1, in2], concatenated_file=out), name='concat')
```

### Step 15: Call wf.add_nodes()

```python
wf.add_nodes([concat])
```

### Step 16: Call wf.run()

```python
wf.run()
```

**Verification:**
```python
assert np.allclose(nb.load(tmpdir.join('test_concatenate', 'concat', out).strpath).get_fdata(), out_data)
```

### Step 17: Assign res = model.Concatenate.run(...)

```python
res = model.Concatenate(in_files=[in1, in2], concatenated_file=out, stats='mean').run()
```

**Verification:**
```python
assert np.allclose(nb.load(out).get_fdata(), mean_data)
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
tmpdir.chdir()
in1 = tmpdir.join('cont1.nii').strpath
in2 = tmpdir.join('cont2.nii').strpath
out = 'bar.nii'
data1 = np.zeros((3, 3, 3, 1), dtype=np.float32)
data2 = np.ones((3, 3, 3, 5), dtype=np.float32)
out_data = np.concatenate((data1, data2), axis=3)
mean_data = np.mean(out_data, axis=3)
nb.Nifti1Image(data1, affine=np.eye(4)).to_filename(in1)
nb.Nifti1Image(data2, affine=np.eye(4)).to_filename(in2)
res = model.Concatenate(in_files=[in1, in2]).run()
assert res.outputs.concatenated_file == tmpdir.join('concat_output.nii.gz').strpath
assert np.allclose(nb.load('concat_output.nii.gz').get_fdata(), out_data)
res = model.Concatenate(in_files=[in1, in2], concatenated_file=out).run()
assert res.outputs.concatenated_file == tmpdir.join(out).strpath
assert np.allclose(nb.load(out).get_fdata(), out_data)
wf = pe.Workflow('test_concatenate', base_dir=tmpdir.strpath)
concat = pe.Node(model.Concatenate(in_files=[in1, in2], concatenated_file=out), name='concat')
wf.add_nodes([concat])
wf.run()
assert np.allclose(nb.load(tmpdir.join('test_concatenate', 'concat', out).strpath).get_fdata(), out_data)
res = model.Concatenate(in_files=[in1, in2], concatenated_file=out, stats='mean').run()
assert np.allclose(nb.load(out).get_fdata(), mean_data)
```

## Next Steps


---

*Source: test_model.py:14 | Complexity: Advanced | Last updated: 2026-05-18*