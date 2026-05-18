# How To: Concat

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test concat

## Prerequisites

**Required Modules:**
- `__future__`
- `numpy`
- `funcs`
- `nifti1`
- `loadsave`
- `tmpdirs`
- `numpy.testing`
- `nose.tools`


## Step-by-Step Guide

### Step 1: Assign shape = value

```python
shape = (1, 2, 5)
```

**Verification:**
```python
assert_array_equal(all_imgs.get_data(), all_data)
```

### Step 2: Assign data0 = np.arange.reshape(...)

```python
data0 = np.arange(10).reshape(shape)
```

**Verification:**
```python
assert_array_equal(all_imgs.get_affine(), affine)
```

### Step 3: Assign affine = np.eye(...)

```python
affine = np.eye(4)
```

**Verification:**
```python
assert_raises(ValueError, concat_images, [img0, img2])
```

### Step 4: Assign img0_mem = Nifti1Image(...)

```python
img0_mem = Nifti1Image(data0, affine)
```

**Verification:**
```python
assert_raises(ValueError, concat_images, [img0, img3])
```

### Step 5: Assign data1 = value

```python
data1 = data0 - 10
```

**Verification:**
```python
assert_array_equal(all_imgs.get_data(), all_data)
```

### Step 6: Assign img1_mem = Nifti1Image(...)

```python
img1_mem = Nifti1Image(data1, affine)
```

**Verification:**
```python
assert_array_equal(all_imgs.get_affine(), affine)
```

### Step 7: Assign img2_mem = Nifti1Image(...)

```python
img2_mem = Nifti1Image(data1, affine + 1)
```

### Step 8: Assign img3_mem = Nifti1Image(...)

```python
img3_mem = Nifti1Image(data1.T, affine)
```

### Step 9: Assign all_data = np.concatenate(...)

```python
all_data = np.concatenate([data0[:, :, :, np.newaxis], data1[:, :, :, np.newaxis]], 3)
```

### Step 10: Assign imgs = value

```python
imgs = [img0_mem, img1_mem, img2_mem, img3_mem]
```

### Step 11: Assign img_files = value

```python
img_files = [_as_fname(img) for img in imgs]
```

### Step 12: Assign all_imgs = concat_images(...)

```python
all_imgs = concat_images([img0, img1])
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(all_imgs.get_data(), all_data)
```

### Step 14: Call assert_array_equal()

```python
assert_array_equal(all_imgs.get_affine(), affine)
```

### Step 15: Call assert_raises()

```python
assert_raises(ValueError, concat_images, [img0, img2])
```

### Step 16: Call assert_raises()

```python
assert_raises(ValueError, concat_images, [img0, img3])
```

### Step 17: Assign all_imgs = concat_images(...)

```python
all_imgs = concat_images([img0, img1])
```

### Step 18: Call assert_array_equal()

```python
assert_array_equal(all_imgs.get_data(), all_data)
```

### Step 19: Call assert_array_equal()

```python
assert_array_equal(all_imgs.get_affine(), affine)
```


## Complete Example

```python
# Workflow
shape = (1, 2, 5)
data0 = np.arange(10).reshape(shape)
affine = np.eye(4)
img0_mem = Nifti1Image(data0, affine)
data1 = data0 - 10
img1_mem = Nifti1Image(data1, affine)
img2_mem = Nifti1Image(data1, affine + 1)
img3_mem = Nifti1Image(data1.T, affine)
all_data = np.concatenate([data0[:, :, :, np.newaxis], data1[:, :, :, np.newaxis]], 3)
with InTemporaryDirectory():
    imgs = [img0_mem, img1_mem, img2_mem, img3_mem]
    img_files = [_as_fname(img) for img in imgs]
    for img0, img1, img2, img3 in (imgs, img_files):
        all_imgs = concat_images([img0, img1])
        assert_array_equal(all_imgs.get_data(), all_data)
        assert_array_equal(all_imgs.get_affine(), affine)
        assert_raises(ValueError, concat_images, [img0, img2])
        assert_raises(ValueError, concat_images, [img0, img3])
        all_imgs = concat_images([img0, img1])
        assert_array_equal(all_imgs.get_data(), all_data)
        assert_array_equal(all_imgs.get_affine(), affine)
    for img in imgs:
        del img
```

## Next Steps


---

*Source: test_funcs.py:32 | Complexity: Advanced | Last updated: 2026-05-18*