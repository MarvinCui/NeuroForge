# How To: Concatenate

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test concatenate

## Prerequisites

**Required Modules:**
- `sys`
- `pytest`
- `trx.trx_file_memmap`
- `dipy.data`
- `dipy.io.streamline`
- `dipy.utils.tractogram`


## Step-by-Step Guide

### Step 1: Assign unknown = get_fnames(...)

```python
filepath_dix, _, _ = get_fnames(name='gold_standard_io')
```

**Verification:**
```python
assert len(concat) == 2 * len(trx)
```

### Step 2: Assign sft = load_tractogram(...)

```python
sft = load_tractogram(filepath_dix['gs_streamlines.trk'], filepath_dix['gs_volume.nii'])
```

### Step 3: Assign trx = tmm.load(...)

```python
trx = tmm.load(filepath_dix['gs_streamlines.trx'])
```

### Step 4: Assign concat = concatenate_tractogram(...)

```python
concat = concatenate_tractogram([sft, trx])
```

**Verification:**
```python
assert len(concat) == 2 * len(trx)
```

### Step 5: Call trx.close()

```python
trx.close()
```

### Step 6: Call concat.close()

```python
concat.close()
```


## Complete Example

```python
# Workflow
filepath_dix, _, _ = get_fnames(name='gold_standard_io')
sft = load_tractogram(filepath_dix['gs_streamlines.trk'], filepath_dix['gs_volume.nii'])
trx = tmm.load(filepath_dix['gs_streamlines.trx'])
concat = concatenate_tractogram([sft, trx])
assert len(concat) == 2 * len(trx)
trx.close()
concat.close()
```

## Next Steps


---

*Source: test_tractogram.py:14 | Complexity: Intermediate | Last updated: 2026-05-18*