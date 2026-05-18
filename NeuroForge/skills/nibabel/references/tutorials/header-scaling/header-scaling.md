# How To: Header Scaling

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test header scaling

## Prerequisites

**Required Modules:**
- `glob`
- `os.path`
- `os.path`
- `warnings`
- `numpy`
- `pytest`
- `numpy`
- `numpy.testing`
- `fileholders`
- `nifti1`
- `openers`
- `parrec`
- `testing`
- `volumeutils`
- `test_arrayproxy`


## Step-by-Step Guide

### Step 1: Assign hdr = PARRECHeader(...)

```python
hdr = PARRECHeader(HDR_INFO, HDR_DEFS)
```

**Verification:**
```python
assert_array_equal(def_scaling, dv_scaling)
```

### Step 2: Assign def_scaling = value

```python
def_scaling = [np.unique(x) for x in hdr.get_data_scaling()]
```

**Verification:**
```python
assert_almost_equal(dv_scaling, [[1.2903541326522827], [0.0]], 5)
```

### Step 3: Assign fp_scaling = value

```python
fp_scaling = [np.unique(x) for x in hdr.get_data_scaling('fp')]
```

**Verification:**
```python
assert_array_equal(scaling, dv_scaling)
```

### Step 4: Assign dv_scaling = value

```python
dv_scaling = [np.unique(x) for x in hdr.get_data_scaling('dv')]
```

**Verification:**
```python
assert not np.all(fp_scaling == dv_scaling)
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(def_scaling, dv_scaling)
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(dv_scaling, [[1.2903541326522827], [0.0]], 5)
```

**Verification:**
```python
assert not np.all(fp_scaling == dv_scaling)
```

### Step 7: Assign scaling = value

```python
scaling = [np.unique(x) for x in hdr.get_data_scaling()]
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(scaling, dv_scaling)
```


## Complete Example

```python
# Workflow
hdr = PARRECHeader(HDR_INFO, HDR_DEFS)
def_scaling = [np.unique(x) for x in hdr.get_data_scaling()]
fp_scaling = [np.unique(x) for x in hdr.get_data_scaling('fp')]
dv_scaling = [np.unique(x) for x in hdr.get_data_scaling('dv')]
assert_array_equal(def_scaling, dv_scaling)
assert_almost_equal(dv_scaling, [[1.2903541326522827], [0.0]], 5)
for hdr in (hdr, PARRECHeader(HDR_INFO, HDR_DEFS)):
    scaling = [np.unique(x) for x in hdr.get_data_scaling()]
    assert_array_equal(scaling, dv_scaling)
assert not np.all(fp_scaling == dv_scaling)
```

## Next Steps


---

*Source: test_parrec.py:221 | Complexity: Advanced | Last updated: 2026-05-18*