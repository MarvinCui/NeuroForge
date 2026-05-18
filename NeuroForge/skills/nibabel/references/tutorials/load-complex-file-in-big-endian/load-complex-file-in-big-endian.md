# How To: Load Complex File In Big Endian

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test load complex file in big endian

## Prerequisites

**Required Modules:**
- `copy`
- `os`
- `sys`
- `unittest`
- `io`
- `os.path`
- `numpy`
- `pytest`
- `numpy.testing`
- `testing`
- `header`
- `tractogram`
- `tractogram_file`
- `trk`
- `test_tractogram`


## Step-by-Step Guide

### Step 1: Assign unknown = self.trk_with_bytes(...)

```python
trk_struct, trk_bytes = self.trk_with_bytes('complex_trk_big_endian_fname', endian='>')
```

**Verification:**
```python
assert hdr_size.dtype.byteorder in good_orders
```

### Step 2: Assign good_orders = value

```python
good_orders = '>' if sys.byteorder == 'little' else '>='
```

**Verification:**
```python
assert hdr_size == 1000
```

### Step 3: Assign hdr_size = value

```python
hdr_size = trk_struct['hdr_size']
```

**Verification:**
```python
assert_tractogram_equal(trk.tractogram, DATA['complex_tractogram'])
```

### Step 4: Assign trk = TrkFile.load(...)

```python
trk = TrkFile.load(DATA['complex_trk_big_endian_fname'], lazy_load=lazy_load)
```

### Step 5: Call assert_tractogram_equal()

```python
assert_tractogram_equal(trk.tractogram, DATA['complex_tractogram'])
```


## Complete Example

```python
# Workflow
trk_struct, trk_bytes = self.trk_with_bytes('complex_trk_big_endian_fname', endian='>')
good_orders = '>' if sys.byteorder == 'little' else '>='
hdr_size = trk_struct['hdr_size']
assert hdr_size.dtype.byteorder in good_orders
assert hdr_size == 1000
for lazy_load in [False, True]:
    trk = TrkFile.load(DATA['complex_trk_big_endian_fname'], lazy_load=lazy_load)
    with pytest.warns(Warning) if lazy_load else error_warnings():
        assert_tractogram_equal(trk.tractogram, DATA['complex_tractogram'])
```

## Next Steps


---

*Source: test_trk.py:200 | Complexity: Intermediate | Last updated: 2026-05-18*