# How To: Ascconv Parse

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test ascconv parse

## Prerequisites

**Required Modules:**
- `collections`
- `os.path`
- `os.path`
- `numpy.testing`


## Step-by-Step Guide

### Step 1: Assign unknown = ascconv.parse_ascconv(...)

```python
ascconv_dict, attrs = ascconv.parse_ascconv(contents, str_delim='""')
```

**Verification:**
```python
assert attrs == OrderedDict()
```

### Step 2: Call assert_array_almost_equal()

```python
assert_array_almost_equal(ascconv_dict['sProtConsistencyInfo']['flNominalB0'], 2.89362)
```

**Verification:**
```python
assert len(ascconv_dict) == 72
```

### Step 3: Assign slice_arr = value

```python
slice_arr = ascconv_dict['sSliceArray']
```

**Verification:**
```python
assert ascconv_dict['tProtocolName'] == 'CBU+AF8-DTI+AF8-64D+AF8-1A'
```

### Step 4: Assign as_slice = value

```python
as_slice = slice_arr['asSlice']
```

**Verification:**
```python
assert ascconv_dict['ucScanRegionPosValid'] == 1
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal([e['dPhaseFOV'] for e in as_slice], 230)
```

**Verification:**
```python
assert_array_almost_equal(ascconv_dict['sProtConsistencyInfo']['flNominalB0'], 2.89362)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal([e['dReadoutFOV'] for e in as_slice], 230)
```

**Verification:**
```python
assert ascconv_dict['sProtConsistencyInfo']['flGMax'] == 26
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal([e['dThickness'] for e in as_slice], 2.5)
```

**Verification:**
```python
assert list(ascconv_dict['sSliceArray'].keys()) == ['asSlice', 'anAsc', 'anPos', 'lSize', 'lConc', 'ucMode', 'sTSat']
```

### Step 8: Assign as_list = value

```python
as_list = ascconv_dict['asCoilSelectMeas'][0]['asList']
```

**Verification:**
```python
assert_array_equal([e['dPhaseFOV'] for e in as_slice], 230)
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(as_slice[0]['sPosition']['dCor'], -20.03015269)
```

**Verification:**
```python
assert_array_equal([e['dReadoutFOV'] for e in as_slice], 230)
```

### Step 10: Assign contents = fobj.read(...)

```python
contents = fobj.read()
```

**Verification:**
```python
assert_array_equal([e['dThickness'] for e in as_slice], 2.5)
```


## Complete Example

```python
# Workflow
with open(ASCCONV_INPUT) as fobj:
    contents = fobj.read()
ascconv_dict, attrs = ascconv.parse_ascconv(contents, str_delim='""')
assert attrs == OrderedDict()
assert len(ascconv_dict) == 72
assert ascconv_dict['tProtocolName'] == 'CBU+AF8-DTI+AF8-64D+AF8-1A'
assert ascconv_dict['ucScanRegionPosValid'] == 1
assert_array_almost_equal(ascconv_dict['sProtConsistencyInfo']['flNominalB0'], 2.89362)
assert ascconv_dict['sProtConsistencyInfo']['flGMax'] == 26
assert list(ascconv_dict['sSliceArray'].keys()) == ['asSlice', 'anAsc', 'anPos', 'lSize', 'lConc', 'ucMode', 'sTSat']
slice_arr = ascconv_dict['sSliceArray']
as_slice = slice_arr['asSlice']
assert_array_equal([e['dPhaseFOV'] for e in as_slice], 230)
assert_array_equal([e['dReadoutFOV'] for e in as_slice], 230)
assert_array_equal([e['dThickness'] for e in as_slice], 2.5)
assert slice_arr['anAsc'] == [None] + list(range(1, 48))
assert slice_arr['anPos'] == [None] + list(range(1, 48))
assert len(ascconv_dict['asCoilSelectMeas']) == 1
as_list = ascconv_dict['asCoilSelectMeas'][0]['asList']
assert len(as_list) == 12
for i, el in enumerate(as_list):
    assert list(el.keys()) == ['sCoilElementID', 'lElementSelected', 'lRxChannelConnected']
    assert el['lElementSelected'] == 1
    assert el['lRxChannelConnected'] == i + 1
assert_array_almost_equal(as_slice[0]['sPosition']['dCor'], -20.03015269)
```

## Next Steps


---

*Source: test_ascconv.py:15 | Complexity: Advanced | Last updated: 2026-05-18*