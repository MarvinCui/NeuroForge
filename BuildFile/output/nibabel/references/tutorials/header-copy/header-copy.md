# How To: Header Copy

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test header copy

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
assert hdr1 is not hdr2
```

### Step 2: Assign hdr2 = hdr.copy(...)

```python
hdr2 = hdr.copy()
```

**Verification:**
```python
assert hdr1.permit_truncated == hdr2.permit_truncated
```

### Step 3: Call assert_copy_ok()

```python
assert_copy_ok(hdr, hdr2)
```

**Verification:**
```python
assert hdr1.general_info is not hdr2.general_info
```

### Step 4: Call assert_copy_ok()

```python
assert_copy_ok(trunc_hdr, trunc_hdr2)
```

**Verification:**
```python
assert_arr_dict_equal(hdr1.general_info, hdr2.general_info)
```

### Step 5: Call assert_arr_dict_equal()

```python
assert_arr_dict_equal(hdr1.general_info, hdr2.general_info)
```

**Verification:**
```python
assert hdr1.image_defs is not hdr2.image_defs
```

### Step 6: Call assert_structarr_equal()

```python
assert_structarr_equal(hdr1.image_defs, hdr2.image_defs)
```

**Verification:**
```python
assert_structarr_equal(hdr1.image_defs, hdr2.image_defs)
```

### Step 7: Assign trunc_hdr2 = trunc_hdr.copy(...)

```python
trunc_hdr2 = trunc_hdr.copy()
```

**Verification:**
```python
assert_copy_ok(hdr, hdr2)
```

### Step 8: Call PARRECHeader.from_fileobj()

```python
PARRECHeader.from_fileobj(fobj)
```

**Verification:**
```python
assert not hdr.permit_truncated
```

### Step 9: Assign trunc_hdr = PARRECHeader.from_fileobj(...)

```python
trunc_hdr = PARRECHeader.from_fileobj(fobj, True)
```

**Verification:**
```python
assert not hdr2.permit_truncated
```


## Complete Example

```python
# Workflow
hdr = PARRECHeader(HDR_INFO, HDR_DEFS)
hdr2 = hdr.copy()

def assert_copy_ok(hdr1, hdr2):
    assert hdr1 is not hdr2
    assert hdr1.permit_truncated == hdr2.permit_truncated
    assert hdr1.general_info is not hdr2.general_info
    assert_arr_dict_equal(hdr1.general_info, hdr2.general_info)
    assert hdr1.image_defs is not hdr2.image_defs
    assert_structarr_equal(hdr1.image_defs, hdr2.image_defs)
assert_copy_ok(hdr, hdr2)
assert not hdr.permit_truncated
assert not hdr2.permit_truncated
with open(TRUNC_PAR) as fobj:
    with pytest.raises(PARRECError):
        PARRECHeader.from_fileobj(fobj)
with open(TRUNC_PAR) as fobj:
    with pytest.warns(UserWarning, match='Header inconsistency'):
        trunc_hdr = PARRECHeader.from_fileobj(fobj, True)
assert trunc_hdr.permit_truncated
with pytest.warns(UserWarning, match='Header inconsistency'):
    trunc_hdr2 = trunc_hdr.copy()
assert_copy_ok(trunc_hdr, trunc_hdr2)
```

## Next Steps


---

*Source: test_parrec.py:674 | Complexity: Advanced | Last updated: 2026-05-18*