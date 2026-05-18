# How To: Io Mrk

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test IO for mrk files.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.io.kit`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test IO for mrk files.'

```python
'Test IO for mrk files.'
```

**Verification:**
```python
assert_array_equal(pts, pts_2, 'read/write mrk to text')
```

### Step 2: Assign pts = read_mrk(...)

```python
pts = read_mrk(mrk_fname)
```

### Step 3: Assign path = value

```python
path = tmp_path / 'mrk.txt'
```

### Step 4: Assign pts_2 = read_mrk(...)

```python
pts_2 = read_mrk(path)
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(pts, pts_2, 'read/write mrk to text')
```

### Step 6: Assign fname = value

```python
fname = tmp_path / 'file.ext'
```

### Step 7: Call fname.write_text()

```python
fname.write_text('')
```

### Step 8: Call fid.write()

```python
fid.write(b'%% %d 3D points, x y z per line\n' % len(pts))
```

### Step 9: Call np.savetxt()

```python
np.savetxt(fid, pts, delimiter='\t', newline='\n')
```

### Step 10: Call read_mrk()

```python
read_mrk(fname)
```

### Step 11: Call read_mrk()

```python
read_mrk(fname)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test IO for mrk files.'
pts = read_mrk(mrk_fname)
path = tmp_path / 'mrk.txt'
with open(path, 'wb') as fid:
    fid.write(b'%% %d 3D points, x y z per line\n' % len(pts))
    np.savetxt(fid, pts, delimiter='\t', newline='\n')
pts_2 = read_mrk(path)
assert_array_equal(pts, pts_2, 'read/write mrk to text')
fname = tmp_path / 'file.ext'
with pytest.raises(FileNotFoundError, match='does not exist'):
    read_mrk(fname)
fname.write_text('')
with pytest.raises(ValueError, match='file extension'):
    read_mrk(fname)
```

## Next Steps


---

*Source: test_coreg.py:16 | Complexity: Advanced | Last updated: 2026-05-18*