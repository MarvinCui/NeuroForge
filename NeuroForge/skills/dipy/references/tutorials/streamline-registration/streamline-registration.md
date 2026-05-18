# How To: Streamline Registration

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test streamline registration

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `tempfile`
- `nibabel`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.align`
- `dipy.align.imwarp`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.io.image`
- `dipy.io.stateful_tractogram`
- `dipy.io.streamline`
- `dipy.testing.decorators`
- `dipy.tracking.utils`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign sl1 = value

```python
sl1 = [np.array([[0, 0, 0], [0, 0, 0.5], [0, 0, 1], [0, 0, 1.5]]), np.array([[0, 0, 0], [0, 0.5, 0.5], [0, 1, 1]])]
```

### Step 2: Assign affine_mat = np.eye(...)

```python
affine_mat = np.eye(4)
```

### Step 3: Assign unknown = rng.standard_normal(...)

```python
affine_mat[:3, 3] = rng.standard_normal(3)
```

### Step 4: Assign sl2 = list(...)

```python
sl2 = list(transform_tracking_output(sl1, affine_mat))
```

### Step 5: Assign unknown = streamline_registration(...)

```python
aligned, matrix = streamline_registration(sl2, sl1)
```

### Step 6: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(matrix, np.linalg.inv(affine_mat))
```

### Step 7: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(aligned[0], sl1[0])
```

### Step 8: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(aligned[1], sl1[1])
```

### Step 9: Assign base_aff = value

```python
base_aff = np.eye(4) * rng.random()
```

### Step 10: Assign unknown = np.array(...)

```python
base_aff[:3, 3] = np.array([1, 2, 3])
```

### Step 11: Assign unknown = 1

```python
base_aff[3, 3] = 1
```

### Step 12: Assign fname1 = value

```python
fname1 = Path(tmpdir) / 'sl1.trx'
```

### Step 13: Assign fname2 = value

```python
fname2 = Path(tmpdir) / 'sl2.trx'
```

### Step 14: Assign unknown = streamline_registration(...)

```python
aligned, matrix = streamline_registration(fname2, fname1)
```

### Step 15: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(aligned[0], sl1[0], decimal=5)
```

### Step 16: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(aligned[1], sl1[1], decimal=5)
```

### Step 17: Assign img = nib.Nifti1Image(...)

```python
img = nib.Nifti1Image(np.zeros((2, 2, 2)), use_aff)
```

### Step 18: Assign tgm1 = StatefulTractogram(...)

```python
tgm1 = StatefulTractogram(transform_tracking_output(sl1, np.linalg.inv(use_aff)), img, Space.VOX)
```

### Step 19: Call save_tractogram()

```python
save_tractogram(tgm1, fname1, bbox_valid_check=False)
```

### Step 20: Assign tgm2 = StatefulTractogram(...)

```python
tgm2 = StatefulTractogram(transform_tracking_output(sl2, np.linalg.inv(use_aff)), img, Space.VOX)
```

### Step 21: Call save_tractogram()

```python
save_tractogram(tgm2, fname2, bbox_valid_check=False)
```

### Step 22: Assign img = nib.Nifti1Image(...)

```python
img = nib.Nifti1Image(np.zeros((2, 2, 2)), np.eye(4))
```

### Step 23: Assign tgm1 = StatefulTractogram(...)

```python
tgm1 = StatefulTractogram(sl1, img, Space.RASMM)
```

### Step 24: Assign tgm2 = StatefulTractogram(...)

```python
tgm2 = StatefulTractogram(sl2, img, Space.RASMM)
```

### Step 25: Call save_tractogram()

```python
save_tractogram(tgm1, fname1, bbox_valid_check=False)
```

### Step 26: Call save_tractogram()

```python
save_tractogram(tgm2, fname2, bbox_valid_check=False)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
sl1 = [np.array([[0, 0, 0], [0, 0, 0.5], [0, 0, 1], [0, 0, 1.5]]), np.array([[0, 0, 0], [0, 0.5, 0.5], [0, 1, 1]])]
affine_mat = np.eye(4)
affine_mat[:3, 3] = rng.standard_normal(3)
sl2 = list(transform_tracking_output(sl1, affine_mat))
aligned, matrix = streamline_registration(sl2, sl1)
npt.assert_almost_equal(matrix, np.linalg.inv(affine_mat))
npt.assert_almost_equal(aligned[0], sl1[0])
npt.assert_almost_equal(aligned[1], sl1[1])
base_aff = np.eye(4) * rng.random()
base_aff[:3, 3] = np.array([1, 2, 3])
base_aff[3, 3] = 1
with TemporaryDirectory() as tmpdir:
    for use_aff in [None, base_aff]:
        fname1 = Path(tmpdir) / 'sl1.trx'
        fname2 = Path(tmpdir) / 'sl2.trx'
        if use_aff is not None:
            img = nib.Nifti1Image(np.zeros((2, 2, 2)), use_aff)
            tgm1 = StatefulTractogram(transform_tracking_output(sl1, np.linalg.inv(use_aff)), img, Space.VOX)
            save_tractogram(tgm1, fname1, bbox_valid_check=False)
            tgm2 = StatefulTractogram(transform_tracking_output(sl2, np.linalg.inv(use_aff)), img, Space.VOX)
            save_tractogram(tgm2, fname2, bbox_valid_check=False)
        else:
            img = nib.Nifti1Image(np.zeros((2, 2, 2)), np.eye(4))
            tgm1 = StatefulTractogram(sl1, img, Space.RASMM)
            tgm2 = StatefulTractogram(sl2, img, Space.RASMM)
            save_tractogram(tgm1, fname1, bbox_valid_check=False)
            save_tractogram(tgm2, fname2, bbox_valid_check=False)
        aligned, matrix = streamline_registration(fname2, fname1)
        npt.assert_almost_equal(aligned[0], sl1[0], decimal=5)
        npt.assert_almost_equal(aligned[1], sl1[1], decimal=5)
```

## Next Steps


---

*Source: test_api.py:317 | Complexity: Advanced | Last updated: 2026-05-18*