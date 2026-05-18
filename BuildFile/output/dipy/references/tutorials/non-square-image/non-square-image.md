# How To: Non Square Image

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test non square image

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.denoise.gibbs`


## Step-by-Step Guide

### Step 1: Assign Nori = 32

```python
Nori = 32
```

**Verification:**
```python
assert_(diff_raw > diff_cor)
```

### Step 2: Assign img = np.zeros(...)

```python
img = np.zeros((6 * Nori, 6 * Nori))
```

### Step 3: Assign unknown = 1

```python
img[Nori:2 * Nori, Nori:2 * Nori] = 1
```

### Step 4: Assign unknown = 1

```python
img[2 * Nori:3 * Nori, Nori:3 * Nori] = 1
```

### Step 5: Assign unknown = 2

```python
img[3 * Nori:4 * Nori, 2 * Nori:3 * Nori] = 2
```

### Step 6: Assign unknown = 3

```python
img[4 * Nori:5 * Nori, 3 * Nori:5 * Nori] = 3
```

### Step 7: Assign c = np.fft.fft2(...)

```python
c = np.fft.fft2(img)
```

### Step 8: Assign c = np.fft.fftshift(...)

```python
c = np.fft.fftshift(c)
```

### Step 9: Assign c_crop = value

```python
c_crop = c[48:144, :]
```

### Step 10: Assign img_gibbs = abs(...)

```python
img_gibbs = abs(np.fft.ifft2(c_crop) / 2)
```

### Step 11: Assign Nre = 16

```python
Nre = 16
```

### Step 12: Assign img_gt = np.zeros(...)

```python
img_gt = np.zeros((6 * Nre, 6 * Nori))
```

### Step 13: Assign unknown = 1

```python
img_gt[Nre:2 * Nre, Nori:2 * Nori] = 1
```

### Step 14: Assign unknown = 1

```python
img_gt[2 * Nre:3 * Nre, Nori:3 * Nori] = 1
```

### Step 15: Assign unknown = 2

```python
img_gt[3 * Nre:4 * Nre, 2 * Nori:3 * Nori] = 2
```

### Step 16: Assign unknown = 3

```python
img_gt[4 * Nre:5 * Nre, 3 * Nori:5 * Nori] = 3
```

### Step 17: Assign img_cor = gibbs_removal(...)

```python
img_cor = gibbs_removal(img_gibbs, inplace=False)
```

### Step 18: Assign diff_raw = np.mean(...)

```python
diff_raw = np.mean(abs(img_gibbs - img_gt))
```

### Step 19: Assign diff_cor = np.mean(...)

```python
diff_cor = np.mean(abs(img_cor - img_gt))
```

### Step 20: Call assert_()

```python
assert_(diff_raw > diff_cor)
```


## Complete Example

```python
# Workflow
Nori = 32
img = np.zeros((6 * Nori, 6 * Nori))
img[Nori:2 * Nori, Nori:2 * Nori] = 1
img[2 * Nori:3 * Nori, Nori:3 * Nori] = 1
img[3 * Nori:4 * Nori, 2 * Nori:3 * Nori] = 2
img[4 * Nori:5 * Nori, 3 * Nori:5 * Nori] = 3
c = np.fft.fft2(img)
c = np.fft.fftshift(c)
c_crop = c[48:144, :]
img_gibbs = abs(np.fft.ifft2(c_crop) / 2)
Nre = 16
img_gt = np.zeros((6 * Nre, 6 * Nori))
img_gt[Nre:2 * Nre, Nori:2 * Nori] = 1
img_gt[2 * Nre:3 * Nre, Nori:3 * Nori] = 1
img_gt[3 * Nre:4 * Nre, 2 * Nori:3 * Nori] = 2
img_gt[4 * Nre:5 * Nre, 3 * Nori:5 * Nori] = 3
img_cor = gibbs_removal(img_gibbs, inplace=False)
diff_raw = np.mean(abs(img_gibbs - img_gt))
diff_cor = np.mean(abs(img_cor - img_gt))
assert_(diff_raw > diff_cor)
```

## Next Steps


---

*Source: test_gibbs.py:221 | Complexity: Advanced | Last updated: 2026-05-18*