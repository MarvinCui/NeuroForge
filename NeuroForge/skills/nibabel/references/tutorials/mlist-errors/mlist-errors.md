# How To: Mlist Errors

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test mlist errors

## Prerequisites

**Required Modules:**
- `os`
- `pathlib`
- `unittest`
- `numpy`
- `pytest`
- `numpy.testing`
- `ecat`
- `openers`
- `testing`
- `tmpdirs`
- `test_fileslice`


## Step-by-Step Guide

### Step 1: Assign fid = open(...)

```python
fid = open(self.example_file, 'rb')
```

**Verification:**
```python
assert series_framenumbers[0] == 2
```

### Step 2: Assign hdr = self.header_class.from_fileobj(...)

```python
hdr = self.header_class.from_fileobj(fid)
```

**Verification:**
```python
assert order == [2, 1, 3, 4, 5, 6]
```

### Step 3: Assign unknown = 6

```python
hdr['num_frames'] = 6
```

**Verification:**
```python
assert neworder == [1, 2, 3, 4, 5]
```

### Step 4: Assign mlist = read_mlist(...)

```python
mlist = read_mlist(fid, hdr.endianness)
```

### Step 5: Call fid.close()

```python
fid.close()
```

### Step 6: Assign mlist = np.array(...)

```python
mlist = np.array([[16842754.0, 3.0, 12035.0, 1.0], [16842753.0, 12036.0, 24068.0, 1.0], [16842755.0, 24069.0, 36101.0, 1.0], [16842756.0, 36102.0, 48134.0, 1.0], [16842757.0, 48135.0, 60167.0, 1.0], [16842758.0, 60168.0, 72200.0, 1.0]])
```

**Verification:**
```python
assert series_framenumbers[0] == 2
```

### Step 7: Assign order = value

```python
order = [series_framenumbers[x] for x in sorted(series_framenumbers)]
```

**Verification:**
```python
assert order == [2, 1, 3, 4, 5, 6]
```

### Step 8: Assign unknown = 0

```python
mlist[0, 0] = 0
```

### Step 9: Assign neworder = value

```python
neworder = [frames_order[x][0] for x in sorted(frames_order)]
```

**Verification:**
```python
assert neworder == [1, 2, 3, 4, 5]
```

### Step 10: Assign series_framenumbers = get_series_framenumbers(...)

```python
series_framenumbers = get_series_framenumbers(mlist)
```

### Step 11: Assign frames_order = get_frame_order(...)

```python
frames_order = get_frame_order(mlist)
```

### Step 12: Call get_series_framenumbers()

```python
get_series_framenumbers(mlist)
```


## Complete Example

```python
# Workflow
fid = open(self.example_file, 'rb')
hdr = self.header_class.from_fileobj(fid)
hdr['num_frames'] = 6
mlist = read_mlist(fid, hdr.endianness)
fid.close()
mlist = np.array([[16842754.0, 3.0, 12035.0, 1.0], [16842753.0, 12036.0, 24068.0, 1.0], [16842755.0, 24069.0, 36101.0, 1.0], [16842756.0, 36102.0, 48134.0, 1.0], [16842757.0, 48135.0, 60167.0, 1.0], [16842758.0, 60168.0, 72200.0, 1.0]])
with suppress_warnings():
    series_framenumbers = get_series_framenumbers(mlist)
assert series_framenumbers[0] == 2
order = [series_framenumbers[x] for x in sorted(series_framenumbers)]
assert order == [2, 1, 3, 4, 5, 6]
mlist[0, 0] = 0
with suppress_warnings():
    frames_order = get_frame_order(mlist)
neworder = [frames_order[x][0] for x in sorted(frames_order)]
assert neworder == [1, 2, 3, 4, 5]
with suppress_warnings():
    with pytest.raises(OSError):
        get_series_framenumbers(mlist)
```

## Next Steps


---

*Source: test_ecat.py:116 | Complexity: Advanced | Last updated: 2026-05-18*