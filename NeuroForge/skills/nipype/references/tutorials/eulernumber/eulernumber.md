# How To: Eulernumber

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test eulernumber

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
assert isinstance(pial, str), 'Problem when fetching surface file'
```

### Step 2: Assign fssrc = FreeSurferSource(...)

```python
fssrc = FreeSurferSource(subjects_dir=subjects_dir, subject_id='fsaverage', hemi='lh')
```

**Verification:**
```python
assert res.outputs.defects == 0
```

### Step 3: Assign pial = value

```python
pial = fssrc.run().outputs.pial
```

**Verification:**
```python
assert res.outputs.euler == 2
```

### Step 4: Assign eu = fs.EulerNumber(...)

```python
eu = fs.EulerNumber()
```

### Step 5: Assign eu.inputs.in_file = pial

```python
eu.inputs.in_file = pial
```

### Step 6: Assign res = eu.run(...)

```python
res = eu.run()
```

**Verification:**
```python
assert res.outputs.defects == 0
```

### Step 7: Call pytest.skip()

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
pial = fssrc.run().outputs.pial
assert isinstance(pial, str), 'Problem when fetching surface file'
eu = fs.EulerNumber()
eu.inputs.in_file = pial
res = eu.run()
assert res.outputs.defects == 0
assert res.outputs.euler == 2
```

## Next Steps


---

*Source: test_utils.py:237 | Complexity: Intermediate | Last updated: 2026-05-18*