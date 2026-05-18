# How To: Read Scalar

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test read scalar

## Prerequisites

**Required Modules:**
- `os.path`
- `os.path`
- `numpy`
- `pytest`
- `numpy.testing`
- `packaging.version`
- `nibabel`
- `nibabel`
- `nibabel.cifti2.parse_cifti2`
- `nibabel.tests`
- `nibabel.tests.nibabel_data`
- `nibabel.tmpdirs`


## Step-by-Step Guide

### Step 1: Assign img = ci.Cifti2Image.from_filename(...)

```python
img = ci.Cifti2Image.from_filename(DATA_FILE2)
```

**Verification:**
```python
assert img.shape[0] == len(expected_names)
```

### Step 2: Assign scalar_mapping = img.header.matrix.get_index_map(...)

```python
scalar_mapping = img.header.matrix.get_index_map(0)
```

**Verification:**
```python
assert len(list(scalar_mapping.named_maps)) == len(expected_names)
```

### Step 3: Assign expected_names = value

```python
expected_names = ('MyelinMap_BC_decurv', 'corrThickness')
```

**Verification:**
```python
assert scalar.map_name == name
```

### Step 4: Assign expected_meta = value

```python
expected_meta = [('PaletteColorMapping', '<PaletteColorMapping Version="1">\n   <ScaleMo')]
```

**Verification:**
```python
assert len(scalar.metadata) == len(expected_meta)
```

### Step 5: Call print()

```python
print(expected_meta[0], scalar.metadata.data.keys())
```

**Verification:**
```python
assert key in scalar.metadata.data.keys()
```


## Complete Example

```python
# Workflow
img = ci.Cifti2Image.from_filename(DATA_FILE2)
scalar_mapping = img.header.matrix.get_index_map(0)
expected_names = ('MyelinMap_BC_decurv', 'corrThickness')
assert img.shape[0] == len(expected_names)
assert len(list(scalar_mapping.named_maps)) == len(expected_names)
expected_meta = [('PaletteColorMapping', '<PaletteColorMapping Version="1">\n   <ScaleMo')]
for scalar, name in zip(scalar_mapping.named_maps, expected_names):
    assert scalar.map_name == name
    assert len(scalar.metadata) == len(expected_meta)
    print(expected_meta[0], scalar.metadata.data.keys())
    for key, value in expected_meta:
        assert key in scalar.metadata.data.keys()
        assert scalar.metadata[key][:len(value)] == value
    assert scalar.label_table is None, '.dscalar file should not define a label table'
```

## Next Steps


---

*Source: test_cifti2io_header.py:346 | Complexity: Intermediate | Last updated: 2026-05-18*