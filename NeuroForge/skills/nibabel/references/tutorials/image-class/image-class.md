# How To: Image Class

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Compare an image of one image class to all others.

The function should make sure that it loads the image with the expected
class, but failing when given a bad sniff (when the sniff is used).

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `copy`
- `os.path`
- `os.path`
- `numpy`

**Setup Required:**
```python
# Fixtures: img_path, expected_img_klass
```

## Step-by-Step Guide

### Step 1: 'Compare an image of one image class to all others.\n\n        The function should make sure that it loads the image with the expected\n        class, but failing when given a bad sniff (when the sniff is used).'

```python
'Compare an image of one image class to all others.\n\n        The function should make sure that it loads the image with the expected\n        class, but failing when given a bad sniff (when the sniff is used).'
```

**Verification:**
```python
assert current_sizeof_hdr >= expected_sizeof_hdr, new_msg
```

### Step 2: Assign sizeof_hdr = getattr(...)

```python
sizeof_hdr = getattr(expected_img_klass.header_class, 'sizeof_hdr', 0)
```

**Verification:**
```python
assert is_img, new_msg
```

### Step 3: """Embedded function to do the actual checks expected."""

```python
"""Embedded function to do the actual checks expected."""
```

### Step 4: Assign unknown = img_klass.path_maybe_image(...)

```python
is_img, new_sniff = img_klass.path_maybe_image(img_path)
```

### Step 5: Assign new_msg = value

```python
new_msg = f'{img_klass.__name__} returned sniff==None ({msg})'
```

### Step 6: Assign expected_sizeof_hdr = getattr(...)

```python
expected_sizeof_hdr = getattr(img_klass.header_class, 'sizeof_hdr', 0)
```

### Step 7: Assign current_sizeof_hdr = value

```python
current_sizeof_hdr = 0 if new_sniff is None else len(new_sniff[0])
```

**Verification:**
```python
assert current_sizeof_hdr >= expected_sizeof_hdr, new_msg
```

### Step 8: Assign new_msg = value

```python
new_msg = f"{basename(img_path)} ({msg}) image is{('' if is_img else ' not')} a {img_klass.__name__} image."
```

**Verification:**
```python
assert is_img, new_msg
```

### Step 9: Assign msg = value

```python
msg = f'{expected_img_klass.__name__}/ {sniff_mode}/ {expect_success}'
```

### Step 10: Assign sniff = check_img(...)

```python
sniff = check_img(img_path, klass, sniff_mode=sniff_mode, sniff=sniff, expect_success=expect_success, msg=msg)
```

### Step 11: Assign unknown = img_klass.path_maybe_image(...)

```python
is_img, new_sniff = img_klass.path_maybe_image(img_path, (sniff, img_path))
```

### Step 12: Assign unknown = img_klass.path_maybe_image(...)

```python
is_img, new_sniff = img_klass.path_maybe_image(img_path, sniff)
```

### Step 13: Assign expect_success = value

```python
expect_success = sniff_mode != 'bad_sniff' or sizeof_hdr == 0
```

### Step 14: Assign expect_success = False

```python
expect_success = False
```


## Complete Example

```python
# Setup
# Fixtures: img_path, expected_img_klass

# Workflow
'Compare an image of one image class to all others.\n\n        The function should make sure that it loads the image with the expected\n        class, but failing when given a bad sniff (when the sniff is used).'

def check_img(img_path, img_klass, sniff_mode, sniff, expect_success, msg):
    """Embedded function to do the actual checks expected."""
    if sniff_mode == 'no_sniff':
        is_img, new_sniff = img_klass.path_maybe_image(img_path)
    elif sniff_mode in ('empty', 'irrelevant', 'bad_sniff'):
        is_img, new_sniff = img_klass.path_maybe_image(img_path, (sniff, img_path))
    else:
        is_img, new_sniff = img_klass.path_maybe_image(img_path, sniff)
    if expect_success:
        new_msg = f'{img_klass.__name__} returned sniff==None ({msg})'
        expected_sizeof_hdr = getattr(img_klass.header_class, 'sizeof_hdr', 0)
        current_sizeof_hdr = 0 if new_sniff is None else len(new_sniff[0])
        assert current_sizeof_hdr >= expected_sizeof_hdr, new_msg
        new_msg = f"{basename(img_path)} ({msg}) image is{('' if is_img else ' not')} a {img_klass.__name__} image."
        assert is_img, new_msg
    if sniff_mode == 'vanilla':
        return new_sniff
    else:
        return sniff
sizeof_hdr = getattr(expected_img_klass.header_class, 'sizeof_hdr', 0)
for sniff_mode, sniff in dict(vanilla=None, no_sniff=None, none=None, empty=b'', irrelevant=b'a' * (sizeof_hdr - 1), bad_sniff=b'a' * sizeof_hdr).items():
    for klass in img_klasses:
        if klass == expected_img_klass:
            expect_success = sniff_mode != 'bad_sniff' or sizeof_hdr == 0
        else:
            expect_success = False
        msg = f'{expected_img_klass.__name__}/ {sniff_mode}/ {expect_success}'
        sniff = check_img(img_path, klass, sniff_mode=sniff_mode, sniff=sniff, expect_success=expect_success, msg=msg)
```

## Next Steps


---

*Source: test_image_types.py:42 | Complexity: Advanced | Last updated: 2026-05-18*