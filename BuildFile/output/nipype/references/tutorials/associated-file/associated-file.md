# How To: Associated File

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test associated file

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `pytest`
- `base`
- `io`

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
assert FSSurfaceCommand._associated_file(white, name) == pial
```

### Step 2: Assign fssrc = FreeSurferSource(...)

```python
fssrc = FreeSurferSource(subjects_dir=subjects_dir, subject_id='fsaverage', hemi='lh')
```

**Verification:**
```python
assert FSSurfaceCommand._associated_file(white, name) == name
```

### Step 3: Assign fssrc.base_dir = value

```python
fssrc.base_dir = tmpdir.strpath
```

### Step 4: Assign fssrc.resource_monitor = False

```python
fssrc.resource_monitor = False
```

### Step 5: Assign fsavginfo = fssrc.run.outputs.get(...)

```python
fsavginfo = fssrc.run().outputs.get()
```

### Step 6: Call pytest.skip()

```python
pytest.skip('fsaverage subject not found in SUBJECTS_DIR')
```

**Verification:**
```python
assert FSSurfaceCommand._associated_file(white, name) == pial
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
fssrc.base_dir = tmpdir.strpath
fssrc.resource_monitor = False
fsavginfo = fssrc.run().outputs.get()
for white, pial in [('lh.white', 'lh.pial'), ('./lh.white', './lh.pial'), (fsavginfo['white'], fsavginfo['pial'])]:
    for name in ('pial', 'lh.pial', pial):
        assert FSSurfaceCommand._associated_file(white, name) == pial
    for name in ('./pial', './lh.pial', fsavginfo['pial']):
        assert FSSurfaceCommand._associated_file(white, name) == name
```

## Next Steps


---

*Source: test_FSSurfaceCommand.py:23 | Complexity: Intermediate | Last updated: 2026-05-18*