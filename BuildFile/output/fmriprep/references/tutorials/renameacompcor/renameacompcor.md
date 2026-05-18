# How To: Renameacompcor

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test RenameACompCor

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

### Step 1: Assign renamer = pe.Node(...)

```python
renamer = pe.Node(confounds.RenameACompCor(), name='renamer', base_dir=str(tmp_path))
```

**Verification:**
```python
assert renamed_components == target_components
```

### Step 2: Assign renamer.inputs.components_file = value

```python
renamer.inputs.components_file = data_dir / 'acompcor_truncated.tsv'
```

**Verification:**
```python
assert renamed_meta == target_meta
```

### Step 3: Assign renamer.inputs.metadata_file = value

```python
renamer.inputs.metadata_file = data_dir / 'component_metadata_truncated.tsv'
```

### Step 4: Assign res = renamer.run(...)

```python
res = renamer.run()
```

### Step 5: Assign target_components = Path.read_text(...)

```python
target_components = Path.read_text(data_dir / 'acompcor_renamed.tsv')
```

### Step 6: Assign target_meta = Path.read_text(...)

```python
target_meta = Path.read_text(data_dir / 'component_metadata_renamed.tsv')
```

### Step 7: Assign renamed_components = Path.read_text(...)

```python
renamed_components = Path(res.outputs.components_file).read_text()
```

### Step 8: Assign renamed_meta = Path.read_text(...)

```python
renamed_meta = Path(res.outputs.metadata_file).read_text()
```

**Verification:**
```python
assert renamed_components == target_components
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, data_dir

# Workflow
renamer = pe.Node(confounds.RenameACompCor(), name='renamer', base_dir=str(tmp_path))
renamer.inputs.components_file = data_dir / 'acompcor_truncated.tsv'
renamer.inputs.metadata_file = data_dir / 'component_metadata_truncated.tsv'
res = renamer.run()
target_components = Path.read_text(data_dir / 'acompcor_renamed.tsv')
target_meta = Path.read_text(data_dir / 'component_metadata_renamed.tsv')
renamed_components = Path(res.outputs.components_file).read_text()
renamed_meta = Path(res.outputs.metadata_file).read_text()
assert renamed_components == target_components
assert renamed_meta == target_meta
```

## Next Steps


---

*Source: test_confounds.py:10 | Complexity: Advanced | Last updated: 2026-05-18*