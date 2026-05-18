# How To: Mlist Errors

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test mlist errors

## Prerequisites

**Required Modules:**
- `__future__`
- `os`
- `numpy`
- `py3k`
- `volumeutils`
- `ecat`
- `unittest`
- `nose.tools`
- `numpy.testing`
- `testing`
- `tmpdirs`


## Step-by-Step Guide

### Step 1: Assign fid = open(...)

```python
fid = open(self.example_file, 'rb')
```

**Verification:**
```python
assert_true(series_framenumbers[0] == 2)
```

### Step 2: Assign hdr = self.header_class.from_fileobj(...)

```python
hdr = self.header_class.from_fileobj(fid)
```

**Verification:**
```python
assert_true(order == [2, 1, 3, 4, 5, 6])
```

### Step 3: Assign unknown = 6

```python
hdr['num_frames'] = 6
```

**Verification:**
```python
assert_true(neworder == [1, 2, 3, 4, 5])
```

### Step 4: Assign mlist = self.mlist_class(...)

```python
mlist = self.mlist_class(fid, hdr)
```

**Verification:**
```python
assert_raises(IOError, mlist.get_series_framenumbers)
```

### Step 5: Assign mlist._mlist = np.array(...)

```python
mlist._mlist = np.array([[16842754.0, 3.0, 12035.0, 1.0], [16842753.0, 12036.0, 24068.0, 1.0], [16842755.0, 24069.0, 36101.0, 1.0], [16842756.0, 36102.0, 48134.0, 1.0], [16842757.0, 48135.0, 60167.0, 1.0], [16842758.0, 60168.0, 72200.0, 1.0]])
```

### Step 6: Assign series_framenumbers = mlist.get_series_framenumbers(...)

```python
series_framenumbers = mlist.get_series_framenumbers()
```

### Step 7: Call assert_true()

```python
assert_true(series_framenumbers[0] == 2)
```

### Step 8: Assign order = value

```python
order = [series_framenumbers[x] for x in sorted(series_framenumbers)]
```

### Step 9: Call assert_true()

```python
assert_true(order == [2, 1, 3, 4, 5, 6])
```

### Step 10: Assign unknown = 0

```python
mlist._mlist[0, 0] = 0
```

### Step 11: Assign frames_order = mlist.get_frame_order(...)

```python
frames_order = mlist.get_frame_order()
```

### Step 12: Assign neworder = value

```python
neworder = [frames_order[x][0] for x in sorted(frames_order)]
```

### Step 13: Call assert_true()

```python
assert_true(neworder == [1, 2, 3, 4, 5])
```

### Step 14: Call assert_raises()

```python
assert_raises(IOError, mlist.get_series_framenumbers)
```


## Complete Example

```python
# Workflow
fid = open(self.example_file, 'rb')
hdr = self.header_class.from_fileobj(fid)
hdr['num_frames'] = 6
mlist = self.mlist_class(fid, hdr)
mlist._mlist = np.array([[16842754.0, 3.0, 12035.0, 1.0], [16842753.0, 12036.0, 24068.0, 1.0], [16842755.0, 24069.0, 36101.0, 1.0], [16842756.0, 36102.0, 48134.0, 1.0], [16842757.0, 48135.0, 60167.0, 1.0], [16842758.0, 60168.0, 72200.0, 1.0]])
series_framenumbers = mlist.get_series_framenumbers()
assert_true(series_framenumbers[0] == 2)
order = [series_framenumbers[x] for x in sorted(series_framenumbers)]
assert_true(order == [2, 1, 3, 4, 5, 6])
mlist._mlist[0, 0] = 0
frames_order = mlist.get_frame_order()
neworder = [frames_order[x][0] for x in sorted(frames_order)]
assert_true(neworder == [1, 2, 3, 4, 5])
assert_raises(IOError, mlist.get_series_framenumbers)
```

## Next Steps


---

*Source: test_ecat.py:126 | Complexity: Advanced | Last updated: 2026-05-18*