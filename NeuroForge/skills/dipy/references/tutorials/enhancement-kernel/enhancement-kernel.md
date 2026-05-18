# How To: Enhancement Kernel

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test if the kernel values are correct by comparison against the values
originally calculated by implementation in Mathematica, and at the same time
checks the symmetry of the kernel.

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.core.sphere`
- `dipy.denoise.enhancement_kernel`
- `dipy.denoise.shift_twist_convolution`
- `dipy.reconst.shm`


## Step-by-Step Guide

### Step 1: 'Test if the kernel values are correct by comparison against the values\n    originally calculated by implementation in Mathematica, and at the same time\n    checks the symmetry of the kernel.'

```python
'Test if the kernel values are correct by comparison against the values\n    originally calculated by implementation in Mathematica, and at the same time\n    checks the symmetry of the kernel.'
```

### Step 2: Assign D33 = 1.0

```python
D33 = 1.0
```

### Step 3: Assign D44 = 0.04

```python
D44 = 0.04
```

### Step 4: Assign t = 1

```python
t = 1
```

### Step 5: Assign k = EnhancementKernel(...)

```python
k = EnhancementKernel(D33, D44, t, orientations=0, force_recompute=True)
```

### Step 6: Assign y = np.array(...)

```python
y = np.array([0.0, 0.0, 0.0])
```

### Step 7: Assign v = np.array(...)

```python
v = np.array([0.0, 0.0, 1.0])
```

### Step 8: Assign orientationlist = value

```python
orientationlist = [[0.0, 0.0, 1.0], [-0.0527864, 0.688191, 0.723607], [-0.67082, -0.16246, 0.723607], [-0.0527864, -0.688191, 0.723607], [0.638197, -0.262866, 0.723607], [0.831052, 0.238856, 0.502295], [0.262866, -0.809017, -0.525731], [0.812731, 0.295242, -0.502295], [-0.029644, 0.864188, -0.502295], [-0.831052, 0.238856, -0.502295], [-0.638197, -0.262866, -0.723607], [-0.436009, 0.864188, -0.251148], [-0.687157, -0.681718, 0.251148], [0.67082, -0.688191, 0.276393], [0.67082, 0.688191, 0.276393], [0.947214, 0.16246, -0.276393], [-0.861803, -0.425325, -0.276393]]
```

### Step 9: Assign positionlist = value

```python
positionlist = [[-0.108096, 0.0412229, 0.339119], [0.220647, -0.422053, 0.427524], [-0.337432, -0.0644619, -0.340777], [0.172579, -0.217602, -0.292446], [-0.271575, -0.125249, -0.350906], [-0.483807, 0.326651, 0.191993], [-0.480936, -0.0718426, 0.33202], [0.497193, -0.00585659, -0.251344], [0.237737, 0.013634, -0.471988], [0.367569, -0.163581, 0.0723955], [0.47859, -0.143252, 0.318579], [-0.21474, -0.264929, -0.46786], [-0.0684234, 0.0342464, 0.0942475], [0.344272, 0.423119, -0.303866], [0.0430714, 0.216233, -0.308475], [0.386085, 0.127333, 0.0503609], [0.334723, 0.071415, 0.403906]]
```

### Step 10: Assign kernelvalues = value

```python
kernelvalues = [0.10701063104295713, 0.0030052117308328923, 0.003125410084676201, 0.0031765819772012613, 0.003127254657020615, 0.0001295130396491743, 6.882352014430076e-14, 1.3821277371353332e-13, 1.3951939946082493e-13, 1.381612071786285e-13, 5.0861109163441125e-17, 1.0722120295517027e-10, 2.425145934791457e-06, 3.557919265806602e-06, 3.6669510385105265e-06, 5.97473789679846e-11, 6.155412262223178e-11]
```

### Step 11: Assign r = np.array(...)

```python
r = np.array(orientationlist[p])
```

### Step 12: Assign x = np.array(...)

```python
x = np.array(positionlist[p])
```

### Step 13: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(k.evaluate_kernel(x, y, r, v), kernelvalues[p])
```


## Complete Example

```python
# Workflow
'Test if the kernel values are correct by comparison against the values\n    originally calculated by implementation in Mathematica, and at the same time\n    checks the symmetry of the kernel.'
D33 = 1.0
D44 = 0.04
t = 1
k = EnhancementKernel(D33, D44, t, orientations=0, force_recompute=True)
y = np.array([0.0, 0.0, 0.0])
v = np.array([0.0, 0.0, 1.0])
orientationlist = [[0.0, 0.0, 1.0], [-0.0527864, 0.688191, 0.723607], [-0.67082, -0.16246, 0.723607], [-0.0527864, -0.688191, 0.723607], [0.638197, -0.262866, 0.723607], [0.831052, 0.238856, 0.502295], [0.262866, -0.809017, -0.525731], [0.812731, 0.295242, -0.502295], [-0.029644, 0.864188, -0.502295], [-0.831052, 0.238856, -0.502295], [-0.638197, -0.262866, -0.723607], [-0.436009, 0.864188, -0.251148], [-0.687157, -0.681718, 0.251148], [0.67082, -0.688191, 0.276393], [0.67082, 0.688191, 0.276393], [0.947214, 0.16246, -0.276393], [-0.861803, -0.425325, -0.276393]]
positionlist = [[-0.108096, 0.0412229, 0.339119], [0.220647, -0.422053, 0.427524], [-0.337432, -0.0644619, -0.340777], [0.172579, -0.217602, -0.292446], [-0.271575, -0.125249, -0.350906], [-0.483807, 0.326651, 0.191993], [-0.480936, -0.0718426, 0.33202], [0.497193, -0.00585659, -0.251344], [0.237737, 0.013634, -0.471988], [0.367569, -0.163581, 0.0723955], [0.47859, -0.143252, 0.318579], [-0.21474, -0.264929, -0.46786], [-0.0684234, 0.0342464, 0.0942475], [0.344272, 0.423119, -0.303866], [0.0430714, 0.216233, -0.308475], [0.386085, 0.127333, 0.0503609], [0.334723, 0.071415, 0.403906]]
kernelvalues = [0.10701063104295713, 0.0030052117308328923, 0.003125410084676201, 0.0031765819772012613, 0.003127254657020615, 0.0001295130396491743, 6.882352014430076e-14, 1.3821277371353332e-13, 1.3951939946082493e-13, 1.381612071786285e-13, 5.0861109163441125e-17, 1.0722120295517027e-10, 2.425145934791457e-06, 3.557919265806602e-06, 3.6669510385105265e-06, 5.97473789679846e-11, 6.155412262223178e-11]
for p in range(len(orientationlist)):
    r = np.array(orientationlist[p])
    x = np.array(positionlist[p])
    npt.assert_almost_equal(k.evaluate_kernel(x, y, r, v), kernelvalues[p])
```

## Next Steps


---

*Source: test_kernel.py:12 | Complexity: Advanced | Last updated: 2026-05-18*