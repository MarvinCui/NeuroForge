# How To: Classify

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test classify

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.data`
- `dipy.segment.mrf`
- `dipy.segment.tissue`
- `dipy.sims.voxel`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign imgseg = TissueClassifierHMRF(...)

```python
imgseg = TissueClassifierHMRF()
```

### Step 2: Assign nclasses = 4

```python
nclasses = 4
```

### Step 3: Assign beta = 0.1

```python
beta = 0.1
```

### Step 4: Assign tolerance = 0.0001

```python
tolerance = 0.0001
```

### Step 5: Assign max_iter = 10

```python
max_iter = 10
```

### Step 6: Assign image = create_image(...)

```python
image = create_image()
```

### Step 7: Call npt.assert_()

```python
npt.assert_(image.max() == 1.0)
```

### Step 8: Call npt.assert_()

```python
npt.assert_(image.min() == 0.0)
```

### Step 9: Assign unknown = imgseg.classify(...)

```python
seg_init, seg_final, PVE = imgseg.classify(image, nclasses, beta)
```

### Step 10: Call npt.assert_()

```python
npt.assert_(seg_final.max() == nclasses)
```

### Step 11: Call npt.assert_()

```python
npt.assert_(seg_final.min() == 0.0)
```

### Step 12: Assign unknown = imgseg.classify(...)

```python
seg_init, seg_final, PVE = imgseg.classify(image, nclasses, beta, tolerance=tolerance)
```

### Step 13: Call npt.assert_()

```python
npt.assert_(seg_final.max() == nclasses)
```

### Step 14: Call npt.assert_()

```python
npt.assert_(seg_final.min() == 0.0)
```

### Step 15: Assign unknown = imgseg.classify(...)

```python
seg_init, seg_final, PVE = imgseg.classify(image, nclasses, beta, max_iter=max_iter)
```

### Step 16: Call npt.assert_()

```python
npt.assert_(seg_final.max() == nclasses)
```

### Step 17: Call npt.assert_()

```python
npt.assert_(seg_final.min() == 0.0)
```

### Step 18: Assign masked_image = np.copy(...)

```python
masked_image = np.copy(image)
```

### Step 19: Assign unknown = 0

```python
masked_image[masked_image.shape[0] // 2:, :, :] = 0
```

### Step 20: Assign unknown = imgseg.classify(...)

```python
seg_init, seg_final, PVE = imgseg.classify(masked_image, nclasses, beta)
```

### Step 21: Call npt.assert_()

```python
npt.assert_(seg_init.max() == nclasses)
```

### Step 22: Call npt.assert_()

```python
npt.assert_(seg_init.min() == 0.0)
```

### Step 23: Call npt.assert_()

```python
npt.assert_(seg_final.max() == nclasses)
```

### Step 24: Call npt.assert_()

```python
npt.assert_(seg_final.min() == 0.0)
```

### Step 25: Call npt.assert_()

```python
npt.assert_(PVE.shape[-1] == nclasses)
```

### Step 26: Assign imgseg = TissueClassifierHMRF(...)

```python
imgseg = TissueClassifierHMRF(save_history=True)
```

### Step 27: Assign unknown = imgseg.classify(...)

```python
seg_init, seg_final, PVE = imgseg.classify(200 * image, nclasses, beta, tolerance=tolerance)
```

### Step 28: Call npt.assert_()

```python
npt.assert_(seg_final.max() == nclasses)
```

### Step 29: Call npt.assert_()

```python
npt.assert_(seg_final.min() == 0.0)
```

### Step 30: Call npt.assert_()

```python
npt.assert_(imgseg.energies_sum[0] > imgseg.energies_sum[-1])
```


## Complete Example

```python
# Workflow
imgseg = TissueClassifierHMRF()
nclasses = 4
beta = 0.1
tolerance = 0.0001
max_iter = 10
image = create_image()
npt.assert_(image.max() == 1.0)
npt.assert_(image.min() == 0.0)
seg_init, seg_final, PVE = imgseg.classify(image, nclasses, beta)
npt.assert_(seg_final.max() == nclasses)
npt.assert_(seg_final.min() == 0.0)
seg_init, seg_final, PVE = imgseg.classify(image, nclasses, beta, tolerance=tolerance)
npt.assert_(seg_final.max() == nclasses)
npt.assert_(seg_final.min() == 0.0)
seg_init, seg_final, PVE = imgseg.classify(image, nclasses, beta, max_iter=max_iter)
npt.assert_(seg_final.max() == nclasses)
npt.assert_(seg_final.min() == 0.0)
masked_image = np.copy(image)
masked_image[masked_image.shape[0] // 2:, :, :] = 0
seg_init, seg_final, PVE = imgseg.classify(masked_image, nclasses, beta)
npt.assert_(seg_init.max() == nclasses)
npt.assert_(seg_init.min() == 0.0)
npt.assert_(seg_final.max() == nclasses)
npt.assert_(seg_final.min() == 0.0)
npt.assert_(PVE.shape[-1] == nclasses)
imgseg = TissueClassifierHMRF(save_history=True)
seg_init, seg_final, PVE = imgseg.classify(200 * image, nclasses, beta, tolerance=tolerance)
npt.assert_(seg_final.max() == nclasses)
npt.assert_(seg_final.min() == 0.0)
npt.assert_(imgseg.energies_sum[0] > imgseg.energies_sum[-1])
```

## Next Steps


---

*Source: test_mrf.py:380 | Complexity: Advanced | Last updated: 2026-05-18*