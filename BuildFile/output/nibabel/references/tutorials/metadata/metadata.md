# How To: Metadata

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test metadata

## Prerequisites

**Required Modules:**
- `itertools`
- `sys`
- `io`
- `numpy`
- `pytest`
- `numpy.testing`
- `nibabel.tmpdirs`
- `fileholders`
- `nifti1`
- `testing`
- `test_parse_gifti_fast`
- `gifti`


## Step-by-Step Guide

### Step 1: Assign md = GiftiMetaData(...)

```python
md = GiftiMetaData(key='value')
```

**Verification:**
```python
assert len(w) == 1
```

### Step 2: Assign nvpair = GiftiNVPairs(...)

```python
nvpair = GiftiNVPairs('key', 'value')
```

**Verification:**
```python
assert md == md2 == md3 == {'key': 'value'}
```

### Step 3: Assign md2 = GiftiMetaData(...)

```python
md2 = GiftiMetaData(nvpair=nvpair)
```

**Verification:**
```python
assert md.data[0].name == 'key'
```

### Step 4: Assign md3 = GiftiMetaData.from_dict(...)

```python
md3 = GiftiMetaData.from_dict({'key': 'value'})
```

**Verification:**
```python
assert md.data[0].value == 'value'
```


## Complete Example

```python
# Workflow
md = GiftiMetaData(key='value')
with deprecated_to('6.0.0'):
    nvpair = GiftiNVPairs('key', 'value')
with pytest.warns(FutureWarning) as w:
    md2 = GiftiMetaData(nvpair=nvpair)
assert len(w) == 1
with deprecated_to('6.0.0'):
    md3 = GiftiMetaData.from_dict({'key': 'value'})
assert md == md2 == md3 == {'key': 'value'}
with deprecated_to('6.0.0'):
    assert md.data[0].name == 'key'
with deprecated_to('6.0.0'):
    assert md.data[0].value == 'value'
```

## Next Steps


---

*Source: test_gifti.py:278 | Complexity: Intermediate | Last updated: 2026-05-18*