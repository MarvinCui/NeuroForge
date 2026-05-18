# How To: Save Load Endian

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test save load endian

## Prerequisites

**Required Modules:**
- `__future__`
- `os.path`
- `shutil`
- `tempfile`
- `py3k`
- `numpy`
- `tmpdirs`
- `volumeutils`
- `numpy.testing`
- `nose.tools`
- `scipy.io`


## Step-by-Step Guide

### Step 1: Assign shape = value

```python
shape = (2, 4, 6)
```

**Verification:**
```python
assert_equal(img.get_header().endianness, native_code)
```

### Step 2: Assign affine = np.diag(...)

```python
affine = np.diag([1, 2, 3, 1])
```

**Verification:**
```python
assert_equal(img2.get_header().endianness, native_code)
```

### Step 3: Assign data = np.arange.reshape(...)

```python
data = np.arange(np.prod(shape), dtype='f4').reshape(shape)
```

**Verification:**
```python
assert_array_equal(img2.get_data(), data)
```

### Step 4: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(data, affine)
```

**Verification:**
```python
assert_equal(bs_img.get_header().endianness, swapped_code)
```

### Step 5: Call assert_equal()

```python
assert_equal(img.get_header().endianness, native_code)
```

**Verification:**
```python
assert_array_equal(bs_img.get_data(), data)
```

### Step 6: Assign img2 = round_trip(...)

```python
img2 = round_trip(img)
```

**Verification:**
```python
assert_equal(cbs_hdr.endianness, native_code)
```

### Step 7: Call assert_equal()

```python
assert_equal(img2.get_header().endianness, native_code)
```

**Verification:**
```python
assert_equal(cbs_hdr2.endianness, native_code)
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(img2.get_data(), data)
```

**Verification:**
```python
assert_equal(bs_data2.dtype.byteorder, swapped_code)
```

### Step 9: Assign bs_hdr = img.get_header.as_byteswapped(...)

```python
bs_hdr = img.get_header().as_byteswapped()
```

**Verification:**
```python
assert_equal(bs_img2.get_header().endianness, swapped_code)
```

### Step 10: Assign bs_img = Nifti1Image(...)

```python
bs_img = Nifti1Image(data, affine, bs_hdr)
```

**Verification:**
```python
assert_array_equal(bs_data2, data)
```

### Step 11: Call assert_equal()

```python
assert_equal(bs_img.get_header().endianness, swapped_code)
```

**Verification:**
```python
assert_equal(mixed_img.get_header().endianness, native_code)
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(bs_img.get_data(), data)
```

**Verification:**
```python
assert_equal(m_img2.get_header().endianness, native_code)
```

### Step 13: Assign cbs_img = AnalyzeImage.from_image(...)

```python
cbs_img = AnalyzeImage.from_image(bs_img)
```

**Verification:**
```python
assert_array_equal(m_img2.get_data(), data)
```

### Step 14: Assign cbs_hdr = cbs_img.get_header(...)

```python
cbs_hdr = cbs_img.get_header()
```

### Step 15: Call assert_equal()

```python
assert_equal(cbs_hdr.endianness, native_code)
```

### Step 16: Assign cbs_img2 = Nifti1Image.from_image(...)

```python
cbs_img2 = Nifti1Image.from_image(cbs_img)
```

### Step 17: Assign cbs_hdr2 = cbs_img2.get_header(...)

```python
cbs_hdr2 = cbs_img2.get_header()
```

### Step 18: Call assert_equal()

```python
assert_equal(cbs_hdr2.endianness, native_code)
```

### Step 19: Assign bs_img2 = round_trip(...)

```python
bs_img2 = round_trip(bs_img)
```

### Step 20: Assign bs_data2 = bs_img2.get_data(...)

```python
bs_data2 = bs_img2.get_data()
```

### Step 21: Call assert_equal()

```python
assert_equal(bs_data2.dtype.byteorder, swapped_code)
```

### Step 22: Call assert_equal()

```python
assert_equal(bs_img2.get_header().endianness, swapped_code)
```

### Step 23: Call assert_array_equal()

```python
assert_array_equal(bs_data2, data)
```

### Step 24: Assign mixed_img = Nifti1Image(...)

```python
mixed_img = Nifti1Image(bs_data2, affine)
```

### Step 25: Call assert_equal()

```python
assert_equal(mixed_img.get_header().endianness, native_code)
```

### Step 26: Assign m_img2 = round_trip(...)

```python
m_img2 = round_trip(mixed_img)
```

### Step 27: Call assert_equal()

```python
assert_equal(m_img2.get_header().endianness, native_code)
```

### Step 28: Call assert_array_equal()

```python
assert_array_equal(m_img2.get_data(), data)
```


## Complete Example

```python
# Workflow
shape = (2, 4, 6)
affine = np.diag([1, 2, 3, 1])
data = np.arange(np.prod(shape), dtype='f4').reshape(shape)
img = Nifti1Image(data, affine)
assert_equal(img.get_header().endianness, native_code)
img2 = round_trip(img)
assert_equal(img2.get_header().endianness, native_code)
assert_array_equal(img2.get_data(), data)
bs_hdr = img.get_header().as_byteswapped()
bs_img = Nifti1Image(data, affine, bs_hdr)
assert_equal(bs_img.get_header().endianness, swapped_code)
assert_array_equal(bs_img.get_data(), data)
cbs_img = AnalyzeImage.from_image(bs_img)
cbs_hdr = cbs_img.get_header()
assert_equal(cbs_hdr.endianness, native_code)
cbs_img2 = Nifti1Image.from_image(cbs_img)
cbs_hdr2 = cbs_img2.get_header()
assert_equal(cbs_hdr2.endianness, native_code)
bs_img2 = round_trip(bs_img)
bs_data2 = bs_img2.get_data()
assert_equal(bs_data2.dtype.byteorder, swapped_code)
assert_equal(bs_img2.get_header().endianness, swapped_code)
assert_array_equal(bs_data2, data)
mixed_img = Nifti1Image(bs_data2, affine)
assert_equal(mixed_img.get_header().endianness, native_code)
m_img2 = round_trip(mixed_img)
assert_equal(m_img2.get_header().endianness, native_code)
assert_array_equal(m_img2.get_data(), data)
```

## Next Steps


---

*Source: test_image_load_save.py:68 | Complexity: Advanced | Last updated: 2026-05-18*