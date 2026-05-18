# How To: Btable Prepare

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test btable prepare

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.core.geometry`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.testing`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign sq2 = value

```python
sq2 = np.sqrt(2) / 2.0
```

### Step 2: Assign bvals = value

```python
bvals = 1500 * np.ones(7)
```

### Step 3: Assign unknown = 0

```python
bvals[0] = 0
```

### Step 4: Assign bvecs = np.array(...)

```python
bvecs = np.array([[0, 0, 0], [1, 0, 0], [0, 1, 0], [0, 0, 1], [sq2, sq2, 0], [sq2, 0, sq2], [0, sq2, sq2]])
```

### Step 5: Assign bt = gradient_table(...)

```python
bt = gradient_table(bvals, bvecs=bvecs)
```

### Step 6: Call npt.assert_array_equal()

```python
npt.assert_array_equal(bt.bvecs, bvecs)
```

### Step 7: Assign unknown = get_fnames(...)

```python
fimg, fbvals, fbvecs = get_fnames(name='small_64D')
```

### Step 8: Assign unknown = read_bvals_bvecs(...)

```python
bvals, bvecs = read_bvals_bvecs(fbvals, fbvecs)
```

### Step 9: Assign bvecs = np.where(...)

```python
bvecs = np.where(np.isnan(bvecs), 0, bvecs)
```

### Step 10: Assign bt = gradient_table(...)

```python
bt = gradient_table(bvals, bvecs=bvecs)
```

### Step 11: Call npt.assert_array_equal()

```python
npt.assert_array_equal(bt.bvecs, bvecs)
```

### Step 12: Assign bt2 = gradient_table(...)

```python
bt2 = gradient_table(bvals, bvecs=bvecs.T)
```

### Step 13: Call npt.assert_array_equal()

```python
npt.assert_array_equal(bt2.bvecs, bvecs)
```

### Step 14: Assign btab = np.concatenate(...)

```python
btab = np.concatenate((bvals[:, None], bvecs), axis=1)
```

### Step 15: Assign bt3 = gradient_table(...)

```python
bt3 = gradient_table(btab)
```

### Step 16: Call npt.assert_array_equal()

```python
npt.assert_array_equal(bt3.bvecs, bvecs)
```

### Step 17: Call npt.assert_array_equal()

```python
npt.assert_array_equal(bt3.bvals, bvals)
```

### Step 18: Assign bt4 = gradient_table(...)

```python
bt4 = gradient_table(btab.T)
```

### Step 19: Call npt.assert_array_equal()

```python
npt.assert_array_equal(bt4.bvecs, bvecs)
```

### Step 20: Call npt.assert_array_equal()

```python
npt.assert_array_equal(bt4.bvals, bvals)
```

### Step 21: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, gradient_table, bvecs)
```


## Complete Example

```python
# Workflow
sq2 = np.sqrt(2) / 2.0
bvals = 1500 * np.ones(7)
bvals[0] = 0
bvecs = np.array([[0, 0, 0], [1, 0, 0], [0, 1, 0], [0, 0, 1], [sq2, sq2, 0], [sq2, 0, sq2], [0, sq2, sq2]])
bt = gradient_table(bvals, bvecs=bvecs)
npt.assert_array_equal(bt.bvecs, bvecs)
fimg, fbvals, fbvecs = get_fnames(name='small_64D')
bvals, bvecs = read_bvals_bvecs(fbvals, fbvecs)
bvecs = np.where(np.isnan(bvecs), 0, bvecs)
bt = gradient_table(bvals, bvecs=bvecs)
npt.assert_array_equal(bt.bvecs, bvecs)
bt2 = gradient_table(bvals, bvecs=bvecs.T)
npt.assert_array_equal(bt2.bvecs, bvecs)
btab = np.concatenate((bvals[:, None], bvecs), axis=1)
bt3 = gradient_table(btab)
npt.assert_array_equal(bt3.bvecs, bvecs)
npt.assert_array_equal(bt3.bvals, bvals)
bt4 = gradient_table(btab.T)
npt.assert_array_equal(bt4.bvecs, bvecs)
npt.assert_array_equal(bt4.bvals, bvals)
npt.assert_raises(ValueError, gradient_table, bvecs)
```

## Next Steps


---

*Source: test_gradients.py:58 | Complexity: Advanced | Last updated: 2026-05-18*