# How To: Nifti Extensions

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test nifti extensions

## Prerequisites

**Required Modules:**
- `__future__`
- `os`
- `py3k`
- `numpy`
- `casting`
- `tmpdirs`
- `spatialimages`
- `affines`
- `nifti1`
- `test_arraywriters`
- `numpy.testing`
- `nose.tools`
- `nose`
- `testing`


## Step-by-Step Guide

### Step 1: Assign nim = load(...)

```python
nim = load(image_file)
```

**Verification:**
```python
assert_equal(len(exts_container), 2)
```

### Step 2: Assign hdr = nim.get_header(...)

```python
hdr = nim.get_header()
```

**Verification:**
```python
assert_equal(exts_container.count('comment'), 2)
```

### Step 3: Assign exts_container = value

```python
exts_container = hdr.extensions
```

**Verification:**
```python
assert_equal(exts_container.count('afni'), 0)
```

### Step 4: Call assert_equal()

```python
assert_equal(len(exts_container), 2)
```

**Verification:**
```python
assert_equal(exts_container.get_codes(), [6, 6])
```

### Step 5: Call assert_equal()

```python
assert_equal(exts_container.count('comment'), 2)
```

**Verification:**
```python
assert_equal(exts_container.get_sizeondisk() % 16, 0)
```

### Step 6: Call assert_equal()

```python
assert_equal(exts_container.count('afni'), 0)
```

**Verification:**
```python
assert_equal(exts_container[0].get_content(), asbytes('extcomment1'))
```

### Step 7: Call assert_equal()

```python
assert_equal(exts_container.get_codes(), [6, 6])
```

**Verification:**
```python
assert_true(exts_container.get_codes() == [6, 6, 4])
```

### Step 8: Call assert_equal()

```python
assert_equal(exts_container.get_sizeondisk() % 16, 0)
```

**Verification:**
```python
assert_true(exts_container.count('comment') == 2)
```

### Step 9: Call assert_equal()

```python
assert_equal(exts_container[0].get_content(), asbytes('extcomment1'))
```

**Verification:**
```python
assert_true(exts_container.count('afni') == 1)
```

### Step 10: Assign afniext = Nifti1Extension(...)

```python
afniext = Nifti1Extension('afni', '<xml></xml>')
```

**Verification:**
```python
assert_true(exts_container.get_sizeondisk() % 16 == 0)
```

### Step 11: Call exts_container.append()

```python
exts_container.append(afniext)
```

**Verification:**
```python
assert_true(exts_container.get_codes() == [6, 4])
```

### Step 12: Call assert_true()

```python
assert_true(exts_container.get_codes() == [6, 6, 4])
```

**Verification:**
```python
assert_true(exts_container.count('comment') == 1)
```

### Step 13: Call assert_true()

```python
assert_true(exts_container.count('comment') == 2)
```

**Verification:**
```python
assert_true(exts_container.count('afni') == 1)
```

### Step 14: Call assert_true()

```python
assert_true(exts_container.count('afni') == 1)
```

### Step 15: Call assert_true()

```python
assert_true(exts_container.get_sizeondisk() % 16 == 0)
```

### Step 16: Call assert_true()

```python
assert_true(exts_container.get_codes() == [6, 4])
```

### Step 17: Call assert_true()

```python
assert_true(exts_container.count('comment') == 1)
```

### Step 18: Call assert_true()

```python
assert_true(exts_container.count('afni') == 1)
```


## Complete Example

```python
# Workflow
nim = load(image_file)
hdr = nim.get_header()
exts_container = hdr.extensions
assert_equal(len(exts_container), 2)
assert_equal(exts_container.count('comment'), 2)
assert_equal(exts_container.count('afni'), 0)
assert_equal(exts_container.get_codes(), [6, 6])
assert_equal(exts_container.get_sizeondisk() % 16, 0)
assert_equal(exts_container[0].get_content(), asbytes('extcomment1'))
afniext = Nifti1Extension('afni', '<xml></xml>')
exts_container.append(afniext)
assert_true(exts_container.get_codes() == [6, 6, 4])
assert_true(exts_container.count('comment') == 2)
assert_true(exts_container.count('afni') == 1)
assert_true(exts_container.get_sizeondisk() % 16 == 0)
del exts_container[1]
assert_true(exts_container.get_codes() == [6, 4])
assert_true(exts_container.count('comment') == 1)
assert_true(exts_container.count('afni') == 1)
```

## Next Steps


---

*Source: test_nifti1.py:763 | Complexity: Advanced | Last updated: 2026-05-18*