# How To: Slope Inter

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test slope inter

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `spatialimages`
- `spm2analyze`


## Step-by-Step Guide

### Step 1: Assign hdr = self.header_class(...)

```python
hdr = self.header_class()
```

**Verification:**
```python
assert hdr.get_slope_inter() == (1.0, 0.0)
```

### Step 2: Assign hdr = self.header_class(...)

```python
hdr = self.header_class()
```

**Verification:**
```python
assert hdr.get_slope_inter() == out_tup
```

### Step 3: Call assert_array_equal()

```python
assert_array_equal(hdr['scl_slope'], raw_slope)
```

**Verification:**
```python
assert hdr.get_slope_inter() == out_tup
```

### Step 4: Call hdr.set_slope_inter()

```python
hdr.set_slope_inter(*in_tup)
```

**Verification:**
```python
assert_array_equal(hdr['scl_slope'], raw_slope)
```

### Step 5: Assign hdr = Spm2AnalyzeHeader.from_header(...)

```python
hdr = Spm2AnalyzeHeader.from_header(hdr, check=True)
```

**Verification:**
```python
assert hdr.get_slope_inter() == out_tup
```

### Step 6: Call hdr.set_slope_inter()

```python
hdr.set_slope_inter(*in_tup)
```

### Step 7: Assign unknown = value

```python
hdr['scl_slope'] = in_tup[0]
```


## Complete Example

```python
# Workflow
hdr = self.header_class()
assert hdr.get_slope_inter() == (1.0, 0.0)
for in_tup, exp_err, out_tup, raw_slope in (((2.0,), None, (2.0, 0.0), 2.0), ((None,), None, (None, None), np.nan), ((1.0, None), None, (1.0, 0.0), 1.0), ((None, 1.1), HeaderTypeError, (None, None), np.nan), ((2.0, 1.1), HeaderTypeError, (None, None), 2.0), ((0.0, None), HeaderDataError, (None, None), 0.0), ((np.nan, np.nan), None, (None, None), np.nan), ((np.nan, None), None, (None, None), np.nan), ((None, np.nan), None, (None, None), np.nan), ((np.inf, None), HeaderDataError, (None, None), np.inf), ((-np.inf, None), HeaderDataError, (None, None), -np.inf), ((None, 0.0), None, (None, None), np.nan)):
    hdr = self.header_class()
    if not exp_err is None:
        with pytest.raises(exp_err):
            hdr.set_slope_inter(*in_tup)
        if not in_tup[0] is None:
            hdr['scl_slope'] = in_tup[0]
    else:
        hdr.set_slope_inter(*in_tup)
        assert hdr.get_slope_inter() == out_tup
        hdr = Spm2AnalyzeHeader.from_header(hdr, check=True)
        assert hdr.get_slope_inter() == out_tup
    assert_array_equal(hdr['scl_slope'], raw_slope)
```

## Next Steps


---

*Source: test_spm2analyze.py:23 | Complexity: Intermediate | Last updated: 2026-05-18*