# How To: Wrappers

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test wrappers

## Prerequisites

**Required Modules:**
- `gzip`
- `copy`
- `decimal`
- `hashlib`
- `os.path`
- `os.path`
- `unittest`
- `numpy`
- `pytest`
- `numpy.testing`
- `openers`
- `tests.nibabel_data`
- `volumeutils`


## Step-by-Step Guide

### Step 1: Assign multi_minimal = value

```python
multi_minimal = {'PerFrameFunctionalGroupsSequence': [pydicom.Dataset()], 'SharedFunctionalGroupsSequence': [pydicom.Dataset()]}
```

**Verification:**
```python
assert dw.get('InstanceNumber') is None
```

### Step 2: Assign dw = maker(...)

```python
dw = maker(*args)
```

**Verification:**
```python
assert dw.get('AcquisitionNumber') is None
```

### Step 3: Assign dw = maker(...)

```python
dw = maker(DATA)
```

**Verification:**
```python
assert not dw.is_mosaic
```

### Step 4: Assign dw = maker(...)

```python
dw = maker(DATA)
```

**Verification:**
```python
assert dw.b_matrix is None
```

### Step 5: Call didw.MultiframeWrapper()

```python
didw.MultiframeWrapper(DATA)
```

**Verification:**
```python
assert dw.q_vector is None
```

### Step 6: dw['not an item']

```python
dw['not an item']
```

**Verification:**
```python
assert dw.get('InstanceNumber') == 2
```

### Step 7: Call dw.get_data()

```python
dw.get_data()
```

**Verification:**
```python
assert dw.get('AcquisitionNumber') == 2
```

### Step 8: dw.affine

```python
dw.affine
```

**Verification:**
```python
assert dw.is_mosaic
```

### Step 9: Call maker()

```python
maker()
```

**Verification:**
```python
assert not dw.is_mosaic
```

### Step 10: dw['not an item']

```python
dw['not an item']
```


## Complete Example

```python
# Workflow
multi_minimal = {'PerFrameFunctionalGroupsSequence': [pydicom.Dataset()], 'SharedFunctionalGroupsSequence': [pydicom.Dataset()]}
for maker, args in ((didw.Wrapper, ({},)), (didw.SiemensWrapper, ({},)), (didw.MosaicWrapper, ({}, None, 10)), (didw.MultiframeWrapper, (multi_minimal,))):
    dw = maker(*args)
    assert dw.get('InstanceNumber') is None
    assert dw.get('AcquisitionNumber') is None
    with pytest.raises(KeyError):
        dw['not an item']
    with pytest.raises(didw.WrapperError):
        dw.get_data()
    with pytest.raises(didw.WrapperError):
        dw.affine
    with pytest.raises(TypeError):
        maker()
    if not maker is didw.MosaicWrapper:
        assert not dw.is_mosaic
    assert dw.b_matrix is None
    assert dw.q_vector is None
for maker in (didw.wrapper_from_data, didw.Wrapper, didw.SiemensWrapper, didw.MosaicWrapper):
    dw = maker(DATA)
    assert dw.get('InstanceNumber') == 2
    assert dw.get('AcquisitionNumber') == 2
    with pytest.raises(KeyError):
        dw['not an item']
for maker in (didw.MosaicWrapper, didw.wrapper_from_data):
    dw = maker(DATA)
    assert dw.is_mosaic
with pytest.raises(didw.WrapperError):
    didw.MultiframeWrapper(DATA)
```

## Next Steps


---

*Source: test_dicomwrappers.py:68 | Complexity: Advanced | Last updated: 2026-05-18*