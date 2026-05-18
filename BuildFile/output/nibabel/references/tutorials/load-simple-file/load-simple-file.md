# How To: Load Simple File

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test load simple file

## Prerequisites

**Required Modules:**
- `os`
- `unittest`
- `io`
- `os.path`
- `numpy`
- `pytest`
- `numpy.testing`
- `testing`
- `array_sequence`
- `tck`
- `tractogram`
- `tractogram_file`
- `test_tractogram`


## Step-by-Step Guide

### Step 1: Assign buffer_size = value

```python
buffer_size = 1.0 / 1024 ** 2
```

**Verification:**
```python
assert_tractogram_equal(tck.tractogram, DATA['simple_tractogram'])
```

### Step 2: Assign hdr = TckFile._read_header(...)

```python
hdr = TckFile._read_header(DATA['simple_tck_fname'])
```

**Verification:**
```python
assert_tractogram_equal(tck.tractogram, DATA['simple_tractogram'])
```

### Step 3: Assign tck_reader = TckFile._read(...)

```python
tck_reader = TckFile._read(DATA['simple_tck_fname'], hdr, buffer_size)
```

### Step 4: Assign streamlines = ArraySequence(...)

```python
streamlines = ArraySequence(tck_reader)
```

### Step 5: Assign tractogram = Tractogram(...)

```python
tractogram = Tractogram(streamlines)
```

### Step 6: Assign tractogram.affine_to_rasmm = np.eye(...)

```python
tractogram.affine_to_rasmm = np.eye(4)
```

### Step 7: Assign tck = TckFile(...)

```python
tck = TckFile(tractogram, header=hdr)
```

### Step 8: Call assert_tractogram_equal()

```python
assert_tractogram_equal(tck.tractogram, DATA['simple_tractogram'])
```

### Step 9: Assign tck = TckFile.load(...)

```python
tck = TckFile.load(DATA['simple_tck_fname'], lazy_load=lazy_load)
```

### Step 10: Call assert_tractogram_equal()

```python
assert_tractogram_equal(tck.tractogram, DATA['simple_tractogram'])
```


## Complete Example

```python
# Workflow
for lazy_load in [False, True]:
    tck = TckFile.load(DATA['simple_tck_fname'], lazy_load=lazy_load)
    with pytest.warns(Warning) if lazy_load else error_warnings():
        assert_tractogram_equal(tck.tractogram, DATA['simple_tractogram'])
buffer_size = 1.0 / 1024 ** 2
hdr = TckFile._read_header(DATA['simple_tck_fname'])
tck_reader = TckFile._read(DATA['simple_tck_fname'], hdr, buffer_size)
streamlines = ArraySequence(tck_reader)
tractogram = Tractogram(streamlines)
tractogram.affine_to_rasmm = np.eye(4)
tck = TckFile(tractogram, header=hdr)
assert_tractogram_equal(tck.tractogram, DATA['simple_tractogram'])
```

## Next Steps


---

*Source: test_tck.py:67 | Complexity: Advanced | Last updated: 2026-05-18*