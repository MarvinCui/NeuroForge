# How To: Gibbs Subfunction

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test gibbs subfunction

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.denoise.gibbs`


## Step-by-Step Guide

### Step 1: Assign image_a0 = _gibbs_removal_1d(...)

```python
image_a0 = _gibbs_removal_1d(image_gibbs, axis=0)
```

**Verification:**
```python
assert_(mean_tv0 < mean_tv1)
```

### Step 2: Assign unknown = _image_tv(...)

```python
tv0_a0_r, tv0_a0_l = _image_tv(image_a0, axis=0)
```

**Verification:**
```python
assert_(mean_tv0 > mean_tv1)
```

### Step 3: Assign tv0_a0 = np.minimum(...)

```python
tv0_a0 = np.minimum(tv0_a0_r, tv0_a0_l)
```

### Step 4: Assign unknown = _image_tv(...)

```python
tv1_a0_r, tv1_a0_l = _image_tv(image_a0, axis=1)
```

### Step 5: Assign tv1_a0 = np.minimum(...)

```python
tv1_a0 = np.minimum(tv1_a0_r, tv1_a0_l)
```

### Step 6: Assign mean_tv0 = np.mean(...)

```python
mean_tv0 = np.mean(abs(tv0_a0))
```

### Step 7: Assign mean_tv1 = np.mean(...)

```python
mean_tv1 = np.mean(abs(tv1_a0))
```

### Step 8: Call assert_()

```python
assert_(mean_tv0 < mean_tv1)
```

### Step 9: Assign image_a1 = _gibbs_removal_1d(...)

```python
image_a1 = _gibbs_removal_1d(image_gibbs, axis=1)
```

### Step 10: Assign unknown = _image_tv(...)

```python
tv0_a1_r, tv0_a1_l = _image_tv(image_a1, axis=0)
```

### Step 11: Assign tv0_a1 = np.minimum(...)

```python
tv0_a1 = np.minimum(tv0_a1_r, tv0_a1_l)
```

### Step 12: Assign unknown = _image_tv(...)

```python
tv1_a1_r, tv1_a1_l = _image_tv(image_a1, axis=1)
```

### Step 13: Assign tv1_a1 = np.minimum(...)

```python
tv1_a1 = np.minimum(tv1_a1_r, tv1_a1_l)
```

### Step 14: Assign mean_tv0 = np.mean(...)

```python
mean_tv0 = np.mean(abs(tv0_a1))
```

### Step 15: Assign mean_tv1 = np.mean(...)

```python
mean_tv1 = np.mean(abs(tv1_a1))
```

### Step 16: Call assert_()

```python
assert_(mean_tv0 > mean_tv1)
```


## Complete Example

```python
# Workflow
image_a0 = _gibbs_removal_1d(image_gibbs, axis=0)
tv0_a0_r, tv0_a0_l = _image_tv(image_a0, axis=0)
tv0_a0 = np.minimum(tv0_a0_r, tv0_a0_l)
tv1_a0_r, tv1_a0_l = _image_tv(image_a0, axis=1)
tv1_a0 = np.minimum(tv1_a0_r, tv1_a0_l)
mean_tv0 = np.mean(abs(tv0_a0))
mean_tv1 = np.mean(abs(tv1_a0))
assert_(mean_tv0 < mean_tv1)
image_a1 = _gibbs_removal_1d(image_gibbs, axis=1)
tv0_a1_r, tv0_a1_l = _image_tv(image_a1, axis=0)
tv0_a1 = np.minimum(tv0_a1_r, tv0_a1_l)
tv1_a1_r, tv1_a1_l = _image_tv(image_a1, axis=1)
tv1_a1 = np.minimum(tv1_a1_r, tv1_a1_l)
mean_tv0 = np.mean(abs(tv0_a1))
mean_tv1 = np.mean(abs(tv1_a1))
assert_(mean_tv0 > mean_tv1)
```

## Next Steps


---

*Source: test_gibbs.py:190 | Complexity: Advanced | Last updated: 2026-05-18*