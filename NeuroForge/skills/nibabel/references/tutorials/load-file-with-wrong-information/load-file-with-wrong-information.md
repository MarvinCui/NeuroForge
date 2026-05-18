# How To: Load File With Wrong Information

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test load file with wrong information

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

### Step 1: Assign tck_file = open.read(...)

```python
tck_file = open(DATA['simple_tck_fname'], 'rb').read()
```

**Verification:**
```python
assert_array_equal(tck.header['datatype'], 'Float32LE')
```

### Step 2: Assign new_tck_file = tck_file.replace(...)

```python
new_tck_file = tck_file.replace(b'Float32LE', b'Float32BE')
```

**Verification:**
```python
assert_array_equal(tck.header['file'], '. 56')
```

### Step 3: Assign new_tck_file = tck_file.replace(...)

```python
new_tck_file = tck_file.replace(b'Float32LE', b'int32')
```

### Step 4: Assign new_tck_file = tck_file.replace(...)

```python
new_tck_file = tck_file.replace(b'datatype: Float32LE\n', b'')
```

### Step 5: Assign new_tck_file = new_tck_file.replace(...)

```python
new_tck_file = new_tck_file.replace(b'file: . 67\n', b'file: . 47\n')
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(tck.header['datatype'], 'Float32LE')
```

### Step 7: Assign new_tck_file = tck_file.replace(...)

```python
new_tck_file = tck_file.replace(b'\nfile: . 67', b'')
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(tck.header['file'], '. 56')
```

### Step 9: Assign new_tck_file = tck_file.replace(...)

```python
new_tck_file = tck_file.replace(b'file: . 67\n', b'file: dummy.mat 75\n')
```

### Step 10: Assign eos = TckFile.FIBER_DELIMITER.tobytes(...)

```python
eos = TckFile.FIBER_DELIMITER.tobytes()
```

### Step 11: Assign eof = TckFile.EOF_DELIMITER.tobytes(...)

```python
eof = TckFile.EOF_DELIMITER.tobytes()
```

### Step 12: Assign new_tck_file = value

```python
new_tck_file = tck_file[:-(len(eos) + len(eof))] + tck_file[-len(eof):]
```

### Step 13: Assign buffer_size = value

```python
buffer_size = 1.0 / 1024 ** 2
```

### Step 14: Assign hdr = TckFile._read_header(...)

```python
hdr = TckFile._read_header(BytesIO(new_tck_file))
```

### Step 15: Assign tck_reader = TckFile._read(...)

```python
tck_reader = TckFile._read(BytesIO(new_tck_file), hdr, buffer_size)
```

### Step 16: Assign new_tck_file = value

```python
new_tck_file = tck_file[:-len(eof)]
```

### Step 17: Call TckFile.load()

```python
TckFile.load(BytesIO(new_tck_file))
```

### Step 18: Call TckFile.load()

```python
TckFile.load(BytesIO(new_tck_file))
```

### Step 19: Assign tck = TckFile.load(...)

```python
tck = TckFile.load(BytesIO(new_tck_file))
```

### Step 20: Assign tck = TckFile.load(...)

```python
tck = TckFile.load(BytesIO(new_tck_file))
```

### Step 21: Call TckFile.load()

```python
TckFile.load(BytesIO(new_tck_file))
```

### Step 22: Call list()

```python
list(tck_reader)
```

### Step 23: Call TckFile.load()

```python
TckFile.load(BytesIO(new_tck_file))
```


## Complete Example

```python
# Workflow
tck_file = open(DATA['simple_tck_fname'], 'rb').read()
new_tck_file = tck_file.replace(b'Float32LE', b'Float32BE')
with pytest.raises(DataError):
    TckFile.load(BytesIO(new_tck_file))
new_tck_file = tck_file.replace(b'Float32LE', b'int32')
with pytest.raises(HeaderError):
    TckFile.load(BytesIO(new_tck_file))
new_tck_file = tck_file.replace(b'datatype: Float32LE\n', b'')
new_tck_file = new_tck_file.replace(b'file: . 67\n', b'file: . 47\n')
with pytest.warns(HeaderWarning, match="Missing 'datatype'"):
    tck = TckFile.load(BytesIO(new_tck_file))
assert_array_equal(tck.header['datatype'], 'Float32LE')
new_tck_file = tck_file.replace(b'\nfile: . 67', b'')
with pytest.warns(HeaderWarning, match="Missing 'file'"):
    tck = TckFile.load(BytesIO(new_tck_file))
assert_array_equal(tck.header['file'], '. 56')
new_tck_file = tck_file.replace(b'file: . 67\n', b'file: dummy.mat 75\n')
with pytest.raises(HeaderError):
    TckFile.load(BytesIO(new_tck_file))
eos = TckFile.FIBER_DELIMITER.tobytes()
eof = TckFile.EOF_DELIMITER.tobytes()
new_tck_file = tck_file[:-(len(eos) + len(eof))] + tck_file[-len(eof):]
buffer_size = 1.0 / 1024 ** 2
hdr = TckFile._read_header(BytesIO(new_tck_file))
tck_reader = TckFile._read(BytesIO(new_tck_file), hdr, buffer_size)
with pytest.raises(DataError):
    list(tck_reader)
new_tck_file = tck_file[:-len(eof)]
with pytest.raises(DataError):
    TckFile.load(BytesIO(new_tck_file))
```

## Next Steps


---

*Source: test_tck.py:116 | Complexity: Advanced | Last updated: 2026-05-18*