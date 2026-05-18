# How To: Mrisexpand

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test mrisexpand

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
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: Assign subjects_dir = fs.Info.subjectsdir(...)

```python
subjects_dir = fs.Info.subjectsdir()
```

**Verification:**
```python
assert expand_if.cmdline == orig_cmdline
```

### Step 2: Assign fssrc = FreeSurferSource(...)

```python
fssrc = FreeSurferSource(subjects_dir=subjects_dir, subject_id='fsaverage', hemi='lh')
```

**Verification:**
```python
assert expand_nd.interface.cmdline == orig_cmdline
```

### Step 3: Assign fsavginfo = fssrc.run.outputs.get(...)

```python
fsavginfo = fssrc.run().outputs.get()
```

**Verification:**
```python
assert nd_res.runtime.cmdline == node_cmdline
```

### Step 4: Assign expand_if = fs.MRIsExpand(...)

```python
expand_if = fs.MRIsExpand(in_file=fsavginfo['smoothwm'], out_name='expandtmp', distance=1, dt=60)
```

**Verification:**
```python
assert op.basename(if_out_file) == op.basename(nd_out_file)
```

### Step 5: Assign expand_nd = pe.Node(...)

```python
expand_nd = pe.Node(fs.MRIsExpand(in_file=fsavginfo['smoothwm'], out_name='expandtmp', distance=1, dt=60), name='expand_node')
```

**Verification:**
```python
assert op.dirname(if_out_file) == op.dirname(fsavginfo['smoothwm'])
```

### Step 6: Assign orig_cmdline = unknown.format(...)

```python
orig_cmdline = 'mris_expand -T 60 {} 1 expandtmp'.format(fsavginfo['smoothwm'])
```

**Verification:**
```python
assert op.dirname(nd_out_file) == nd_res.runtime.cwd
```

### Step 7: Assign nd_res = expand_nd.run(...)

```python
nd_res = expand_nd.run()
```

### Step 8: Assign node_cmdline = unknown.format(...)

```python
node_cmdline = 'mris_expand -T 60 -pial {cwd}/lh.pial {cwd}/lh.smoothwm 1 expandtmp'.format(cwd=nd_res.runtime.cwd)
```

**Verification:**
```python
assert nd_res.runtime.cmdline == node_cmdline
```

### Step 9: Assign if_out_file = value

```python
if_out_file = expand_if._list_outputs()['out_file']
```

### Step 10: Assign nd_out_file = value

```python
nd_out_file = nd_res.outputs.get()['out_file']
```

**Verification:**
```python
assert op.basename(if_out_file) == op.basename(nd_out_file)
```

### Step 11: Call pytest.skip()

```python
pytest.skip('fsaverage subject not found in SUBJECTS_DIR')
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
subjects_dir = fs.Info.subjectsdir()
if subjects_dir is None or not os.path.exists(os.path.join(subjects_dir, 'fsaverage')):
    pytest.skip('fsaverage subject not found in SUBJECTS_DIR')
fssrc = FreeSurferSource(subjects_dir=subjects_dir, subject_id='fsaverage', hemi='lh')
fsavginfo = fssrc.run().outputs.get()
expand_if = fs.MRIsExpand(in_file=fsavginfo['smoothwm'], out_name='expandtmp', distance=1, dt=60)
expand_nd = pe.Node(fs.MRIsExpand(in_file=fsavginfo['smoothwm'], out_name='expandtmp', distance=1, dt=60), name='expand_node')
orig_cmdline = 'mris_expand -T 60 {} 1 expandtmp'.format(fsavginfo['smoothwm'])
assert expand_if.cmdline == orig_cmdline
assert expand_nd.interface.cmdline == orig_cmdline
nd_res = expand_nd.run()
node_cmdline = 'mris_expand -T 60 -pial {cwd}/lh.pial {cwd}/lh.smoothwm 1 expandtmp'.format(cwd=nd_res.runtime.cwd)
assert nd_res.runtime.cmdline == node_cmdline
if_out_file = expand_if._list_outputs()['out_file']
nd_out_file = nd_res.outputs.get()['out_file']
assert op.basename(if_out_file) == op.basename(nd_out_file)
assert op.dirname(if_out_file) == op.dirname(fsavginfo['smoothwm'])
assert op.dirname(nd_out_file) == nd_res.runtime.cwd
```

## Next Steps


---

*Source: test_utils.py:185 | Complexity: Advanced | Last updated: 2026-05-18*