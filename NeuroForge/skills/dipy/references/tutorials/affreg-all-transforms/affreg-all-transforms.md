# How To: Affreg All Transforms

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test affreg all transforms

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `numpy.linalg`
- `numpy.testing`
- `dipy.align`
- `dipy.align.imaffine`
- `dipy.align.tests.test_parzenhist`
- `dipy.align.transforms`
- `dipy.core`
- `dipy.testing`
- `dipy.testing.decorators`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign metric = imaffine.MutualInformationMetric(...)

```python
metric = imaffine.MutualInformationMetric(nbins=32)
```

**Verification:**
```python
assert reduction > 0.9
```

### Step 2: Call assert_raises()

```python
assert_raises(ValueError, imaffine.AffineRegistration, metric=metric, level_iters=[])
```

**Verification:**
```python
assert_raises(ValueError, imaffine.AffineRegistration, metric=metric, level_iters=[])
```

### Step 3: Assign affine_map = assert_warns(...)

```python
affine_map = assert_warns(UserWarning, affreg.optimize, static, moving, trans, x0, static_grid2world=static_g2w, moving_grid2world=moving_g2w, starting_affine=None, ret_metric=None, static_mask=np.zeros_like(smask), moving_mask=np.zeros_like(mmask))
```

### Step 4: Assign dim = value

```python
dim = ttype[1]
```

### Step 5: Assign factor = value

```python
factor = factors[ttype][0]
```

### Step 6: Assign sampling_pc = value

```python
sampling_pc = factors[ttype][1]
```

### Step 7: Assign trans = value

```python
trans = regtransforms[ttype]
```

### Step 8: Assign srt = setup_random_transform

```python
srt = setup_random_transform
```

### Step 9: Assign unknown = srt(...)

```python
static, moving, static_g2w, moving_g2w, smask, mmask, T = srt(trans, factor, nslices, 1.0, rng=rng)
```

### Step 10: Assign start_sad = np.abs.sum(...)

```python
start_sad = np.abs(static - moving).sum()
```

### Step 11: Assign metric = imaffine.MutualInformationMetric(...)

```python
metric = imaffine.MutualInformationMetric(nbins=32, sampling_proportion=sampling_pc)
```

### Step 12: Assign affreg = imaffine.AffineRegistration(...)

```python
affreg = imaffine.AffineRegistration(metric=metric, level_iters=[1000, 100, 50], sigmas=[3, 1, 0], factors=[4, 2, 1], method='L-BFGS-B', ss_sigma_factor=None, options=None)
```

### Step 13: Assign x0 = trans.get_identity_parameters(...)

```python
x0 = trans.get_identity_parameters()
```

### Step 14: Assign transformed = affine_map.transform(...)

```python
transformed = affine_map.transform(moving)
```

### Step 15: Assign end_sad = np.abs.sum(...)

```python
end_sad = np.abs(static - transformed).sum()
```

### Step 16: Assign reduction = value

```python
reduction = 1 - end_sad / start_sad
```

### Step 17: Call print()

```python
print(f'{ttype}>>{reduction:f}')
```

**Verification:**
```python
assert reduction > 0.9
```

### Step 18: Assign nslices = 1

```python
nslices = 1
```

### Step 19: Assign nslices = 45

```python
nslices = 45
```

### Step 20: Assign affine_map = assert_warns(...)

```python
affine_map = assert_warns(UserWarning, affreg.optimize, static, moving, trans, x0, static_grid2world=static_g2w, moving_grid2world=moving_g2w, starting_affine=None, ret_metric=None, static_mask=smask, moving_mask=mmask)
```

### Step 21: Assign affine_map = affreg.optimize(...)

```python
affine_map = affreg.optimize(static, moving, trans, x0, static_grid2world=static_g2w, moving_grid2world=moving_g2w, starting_affine=None, ret_metric=None, static_mask=smask, moving_mask=mmask)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
for ttype in sorted(factors):
    dim = ttype[1]
    if dim == 2:
        nslices = 1
    else:
        nslices = 45
    factor = factors[ttype][0]
    sampling_pc = factors[ttype][1]
    trans = regtransforms[ttype]
    srt = setup_random_transform
    static, moving, static_g2w, moving_g2w, smask, mmask, T = srt(trans, factor, nslices, 1.0, rng=rng)
    start_sad = np.abs(static - moving).sum()
    metric = imaffine.MutualInformationMetric(nbins=32, sampling_proportion=sampling_pc)
    affreg = imaffine.AffineRegistration(metric=metric, level_iters=[1000, 100, 50], sigmas=[3, 1, 0], factors=[4, 2, 1], method='L-BFGS-B', ss_sigma_factor=None, options=None)
    x0 = trans.get_identity_parameters()
    if sampling_pc not in [1.0, None]:
        affine_map = assert_warns(UserWarning, affreg.optimize, static, moving, trans, x0, static_grid2world=static_g2w, moving_grid2world=moving_g2w, starting_affine=None, ret_metric=None, static_mask=smask, moving_mask=mmask)
    else:
        affine_map = affreg.optimize(static, moving, trans, x0, static_grid2world=static_g2w, moving_grid2world=moving_g2w, starting_affine=None, ret_metric=None, static_mask=smask, moving_mask=mmask)
    transformed = affine_map.transform(moving)
    end_sad = np.abs(static - transformed).sum()
    reduction = 1 - end_sad / start_sad
    print(f'{ttype}>>{reduction:f}')
    assert reduction > 0.9
metric = imaffine.MutualInformationMetric(nbins=32)
assert_raises(ValueError, imaffine.AffineRegistration, metric=metric, level_iters=[])
affine_map = assert_warns(UserWarning, affreg.optimize, static, moving, trans, x0, static_grid2world=static_g2w, moving_grid2world=moving_g2w, starting_affine=None, ret_metric=None, static_mask=np.zeros_like(smask), moving_mask=np.zeros_like(mmask))
```

## Next Steps


---

*Source: test_imaffine.py:209 | Complexity: Advanced | Last updated: 2026-05-18*