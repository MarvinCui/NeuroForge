# How To: Label Fill Restrict

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test label in fill and restrict.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `glob`
- `os`
- `pickle`
- `shutil`
- `itertools`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne.datasets`
- `mne.fixes`
- `mne.label`
- `mne.source_estimate`
- `mne.source_space`
- `mne.surface`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: fname
```

## Step-by-Step Guide

### Step 1: 'Test label in fill and restrict.'

```python
'Test label in fill and restrict.'
```

**Verification:**
```python
assert src[0]['nearest'] is not None
```

### Step 2: Assign src = read_source_spaces(...)

```python
src = read_source_spaces(src_fname)
```

**Verification:**
```python
assert_array_equal(label_src.vertices, vertices_in)
```

### Step 3: Assign label = read_label(...)

```python
label = read_label(fname)
```

**Verification:**
```python
assert_array_equal(np.isin(vertices_out, label_src.vertices), False)
```

### Step 4: Assign label_src = label.restrict(...)

```python
label_src = label.restrict(src)
```

**Verification:**
```python
assert_array_equal(label_src.values, values_in_src[value_idx])
```

### Step 5: Assign vert_in_src = value

```python
vert_in_src = label_src.vertices
```

**Verification:**
```python
assert_array_equal(label.vertices, np.array([], int))
```

### Step 6: Assign values_in_src = value

```python
values_in_src = label_src.values
```

**Verification:**
```python
assert src[0]['nearest'] is not None
```

### Step 7: Assign vertices_status = np.isin(...)

```python
vertices_status = np.isin(src[0]['nearest'], label.vertices)
```

### Step 8: Assign vertices_in = value

```python
vertices_in = np.nonzero(vertices_status)[0]
```

### Step 9: Assign vertices_out = value

```python
vertices_out = np.nonzero(np.logical_not(vertices_status))[0]
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(label_src.vertices, vertices_in)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(np.isin(vertices_out, label_src.vertices), False)
```

### Step 12: Assign value_idx = np.digitize(...)

```python
value_idx = np.digitize(src[0]['nearest'][vertices_in], vert_in_src, True)
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(label_src.values, values_in_src[value_idx])
```

### Step 14: Assign vertices = np.append(...)

```python
vertices = np.append([-1], vert_in_src)
```

### Step 15: Assign label = Label(...)

```python
label = Label([], hemi='lh')
```

### Step 16: Call label.fill()

```python
label.fill(src)
```

### Step 17: Call assert_array_equal()

```python
assert_array_equal(label.vertices, np.array([], int))
```

### Step 18: Assign label_src = label_src.fill(...)

```python
label_src = label_src.fill(src)
```

### Step 19: Call Label.fill()

```python
Label(vertices, hemi='lh').fill(src)
```

### Step 20: Assign unknown = None

```python
s['nearest'] = None
```

### Step 21: Assign label_src = label_src.fill(...)

```python
label_src = label_src.fill(src)
```


## Complete Example

```python
# Setup
# Fixtures: fname

# Workflow
'Test label in fill and restrict.'
src = read_source_spaces(src_fname)
label = read_label(fname)
label_src = label.restrict(src)
vert_in_src = label_src.vertices
values_in_src = label_src.values
if fname == real_label_fname:
    for s in src:
        s['nearest'] = None
    with _record_warnings():
        label_src = label_src.fill(src)
else:
    label_src = label_src.fill(src)
assert src[0]['nearest'] is not None
vertices_status = np.isin(src[0]['nearest'], label.vertices)
vertices_in = np.nonzero(vertices_status)[0]
vertices_out = np.nonzero(np.logical_not(vertices_status))[0]
assert_array_equal(label_src.vertices, vertices_in)
assert_array_equal(np.isin(vertices_out, label_src.vertices), False)
value_idx = np.digitize(src[0]['nearest'][vertices_in], vert_in_src, True)
assert_array_equal(label_src.values, values_in_src[value_idx])
vertices = np.append([-1], vert_in_src)
with pytest.raises(ValueError, match='does not contain all of the label'):
    Label(vertices, hemi='lh').fill(src)
label = Label([], hemi='lh')
label.fill(src)
assert_array_equal(label.vertices, np.array([], int))
```

## Next Steps


---

*Source: test_label.py:279 | Complexity: Advanced | Last updated: 2026-05-18*