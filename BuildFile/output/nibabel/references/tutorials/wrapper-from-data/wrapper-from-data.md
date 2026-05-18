# How To: Wrapper From Data

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test wrapper from data

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

### Step 1: Assign dw = didw.wrapper_from_file(...)

```python
dw = didw.wrapper_from_file(DATA_FILE_SLC_NORM)
```

**Verification:**
```python
assert dw.get('InstanceNumber') == 2
```

### Step 2: Assign fake_data = dict(...)

```python
fake_data = dict()
```

**Verification:**
```python
assert dw.get('AcquisitionNumber') == 2
```

### Step 3: Assign unknown = '1.2.840.10008.5.1.4.1.1.4.2'

```python
fake_data['SOPClassUID'] = '1.2.840.10008.5.1.4.1.1.4.2'
```

**Verification:**
```python
assert dw.is_mosaic
```

### Step 4: Assign dw = didw.wrapper_from_data(...)

```python
dw = didw.wrapper_from_data(fake_data)
```

**Verification:**
```python
assert_array_almost_equal(np.dot(didr.DPCS_TO_TAL, dw.affine), EXPECTED_AFFINE)
```

### Step 5: Assign unknown = '1.2.840.10008.5.1.4.1.1.4.1'

```python
fake_data['SOPClassUID'] = '1.2.840.10008.5.1.4.1.1.4.1'
```

**Verification:**
```python
assert dw.get('InstanceNumber') == 1
```

### Step 6: Assign unknown = value

```python
fake_data['PerFrameFunctionalGroupsSequence'] = [pydicom.Dataset()]
```

**Verification:**
```python
assert dw.get('AcquisitionNumber') == 3
```

### Step 7: Assign unknown = value

```python
fake_data['SharedFunctionalGroupsSequence'] = [pydicom.Dataset()]
```

**Verification:**
```python
assert dw.is_multiframe
```

### Step 8: Assign dw = didw.wrapper_from_data(...)

```python
dw = didw.wrapper_from_data(fake_data)
```

**Verification:**
```python
assert dw.is_mosaic
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(np.dot(didr.DPCS_TO_TAL, dw.affine), EXPECTED_AFFINE)
```

**Verification:**
```python
assert not dw.is_multiframe
```

### Step 10: Call didw.wrapper_from_data()

```python
didw.wrapper_from_data(fake_data)
```

**Verification:**
```python
assert dw.is_multiframe
```

### Step 11: Call didw.wrapper_from_data()

```python
didw.wrapper_from_data(fake_data)
```

### Step 12: dw['not an item']

```python
dw['not an item']
```

### Step 13: dw['not an item']

```python
dw['not an item']
```


## Complete Example

```python
# Workflow
for dw in (didw.wrapper_from_data(DATA), didw.wrapper_from_file(DATA_FILE)):
    assert dw.get('InstanceNumber') == 2
    assert dw.get('AcquisitionNumber') == 2
    with pytest.raises(KeyError):
        dw['not an item']
    assert dw.is_mosaic
    assert_array_almost_equal(np.dot(didr.DPCS_TO_TAL, dw.affine), EXPECTED_AFFINE)
for dw in (didw.wrapper_from_data(DATA_PHILIPS), didw.wrapper_from_file(DATA_FILE_PHILIPS)):
    assert dw.get('InstanceNumber') == 1
    assert dw.get('AcquisitionNumber') == 3
    with pytest.raises(KeyError):
        dw['not an item']
    assert dw.is_multiframe
dw = didw.wrapper_from_file(DATA_FILE_SLC_NORM)
assert dw.is_mosaic
fake_data = dict()
fake_data['SOPClassUID'] = '1.2.840.10008.5.1.4.1.1.4.2'
dw = didw.wrapper_from_data(fake_data)
assert not dw.is_multiframe
fake_data['SOPClassUID'] = '1.2.840.10008.5.1.4.1.1.4.1'
with pytest.raises(didw.WrapperError):
    didw.wrapper_from_data(fake_data)
fake_data['PerFrameFunctionalGroupsSequence'] = [pydicom.Dataset()]
with pytest.raises(didw.WrapperError):
    didw.wrapper_from_data(fake_data)
fake_data['SharedFunctionalGroupsSequence'] = [pydicom.Dataset()]
dw = didw.wrapper_from_data(fake_data)
assert dw.is_multiframe
```

## Next Steps


---

*Source: test_dicomwrappers.py:145 | Complexity: Advanced | Last updated: 2026-05-18*