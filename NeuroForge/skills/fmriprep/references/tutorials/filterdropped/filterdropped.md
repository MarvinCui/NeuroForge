# How To: Filterdropped

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test FilterDropped

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pandas`
- `nipype.pipeline`
- `fmriprep.interfaces`

**Setup Required:**
```python
# Fixtures: tmp_path, data_dir
```

## Step-by-Step Guide

### Step 1: Assign filt = pe.Node(...)

```python
filt = pe.Node(confounds.FilterDropped(), name='filt', base_dir=str(tmp_path))
```

**Verification:**
```python
assert filtered_meta == target_meta
```

### Step 2: Assign filt.inputs.in_file = value

```python
filt.inputs.in_file = data_dir / 'component_metadata_truncated.tsv'
```

### Step 3: Assign res = filt.run(...)

```python
res = filt.run()
```

### Step 4: Assign target_meta = Path.read_text(...)

```python
target_meta = Path.read_text(data_dir / 'component_metadata_filtered.tsv')
```

### Step 5: Assign filtered_meta = Path.read_text(...)

```python
filtered_meta = Path(res.outputs.out_file).read_text()
```

**Verification:**
```python
assert filtered_meta == target_meta
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, data_dir

# Workflow
filt = pe.Node(confounds.FilterDropped(), name='filt', base_dir=str(tmp_path))
filt.inputs.in_file = data_dir / 'component_metadata_truncated.tsv'
res = filt.run()
target_meta = Path.read_text(data_dir / 'component_metadata_filtered.tsv')
filtered_meta = Path(res.outputs.out_file).read_text()
assert filtered_meta == target_meta
```

## Next Steps


---

*Source: test_confounds.py:25 | Complexity: Intermediate | Last updated: 2026-05-18*