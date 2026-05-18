# How To: Surfaces

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test surfaces

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `tempfile`
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.data`
- `dipy.direction.peaks`
- `dipy.io.stateful_tractogram`
- `dipy.io.utils`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.tracking.streamline`
- `dipy.utils.optpkg`
- `fury`
- `dipy.viz.horizon.app`
- `dipy.segment.tests.test_bundles`
- `dipy.segment.tests.test_bundles`
- `dipy.viz`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign vertices = rng.random(...)

```python
vertices = rng.random((100, 3))
```

### Step 2: Assign faces = rng.integers(...)

```python
faces = rng.integers(0, 100, size=(100, 3))
```

### Step 3: Assign surfaces = value

```python
surfaces = [(vertices, faces), (vertices, faces, '/test/filename.pial'), (vertices, faces, '/test/filename.pial')]
```

### Step 4: Assign show_m = horizon(...)

```python
show_m = horizon(surfaces=surfaces, return_showm=True)
```

### Step 5: Assign analysis = window.analyze_scene(...)

```python
analysis = window.analyze_scene(show_m.scene)
```

### Step 6: Call npt.assert_equal()

```python
npt.assert_equal(analysis.actors, 3)
```

### Step 7: Assign vertices = rng.random(...)

```python
vertices = rng.random((100, 4))
```

### Step 8: Assign faces = rng.integers(...)

```python
faces = rng.integers(0, 100, size=(100, 3))
```

### Step 9: Assign surfaces = value

```python
surfaces = [(vertices, faces), (vertices, faces, '/test/filename.pial'), (vertices, faces, '/test/filename.pial')]
```

### Step 10: Assign vertices = rng.random(...)

```python
vertices = rng.random((100, 3))
```

### Step 11: Assign faces = rng.integers(...)

```python
faces = rng.integers(0, 100, size=(100, 4))
```

### Step 12: Assign surfaces = value

```python
surfaces = [(vertices, faces), (vertices, faces, '/test/filename.pial'), (vertices, faces, '/test/filename.pial')]
```

### Step 13: Assign show_m = horizon(...)

```python
show_m = horizon(surfaces=surfaces, return_showm=True)
```

### Step 14: Assign analysis = window.analyze_scene(...)

```python
analysis = window.analyze_scene(show_m.scene)
```

### Step 15: Call npt.assert_equal()

```python
npt.assert_equal(analysis.actors, 0)
```

### Step 16: Call check_for_warnings()

```python
check_for_warnings(l_warns, 'Vertices do not have correct shape: (100, 4)')
```

### Step 17: Assign show_m = horizon(...)

```python
show_m = horizon(surfaces=surfaces, return_showm=True)
```

### Step 18: Assign analysis = window.analyze_scene(...)

```python
analysis = window.analyze_scene(show_m.scene)
```

### Step 19: Call npt.assert_equal()

```python
npt.assert_equal(analysis.actors, 0)
```

### Step 20: Call check_for_warnings()

```python
check_for_warnings(l_warns, 'Faces do not have correct shape: (100, 4)')
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
vertices = rng.random((100, 3))
faces = rng.integers(0, 100, size=(100, 3))
surfaces = [(vertices, faces), (vertices, faces, '/test/filename.pial'), (vertices, faces, '/test/filename.pial')]
show_m = horizon(surfaces=surfaces, return_showm=True)
analysis = window.analyze_scene(show_m.scene)
npt.assert_equal(analysis.actors, 3)
vertices = rng.random((100, 4))
faces = rng.integers(0, 100, size=(100, 3))
surfaces = [(vertices, faces), (vertices, faces, '/test/filename.pial'), (vertices, faces, '/test/filename.pial')]
with warnings.catch_warnings(record=True) as l_warns:
    show_m = horizon(surfaces=surfaces, return_showm=True)
    analysis = window.analyze_scene(show_m.scene)
    npt.assert_equal(analysis.actors, 0)
    check_for_warnings(l_warns, 'Vertices do not have correct shape: (100, 4)')
vertices = rng.random((100, 3))
faces = rng.integers(0, 100, size=(100, 4))
surfaces = [(vertices, faces), (vertices, faces, '/test/filename.pial'), (vertices, faces, '/test/filename.pial')]
with warnings.catch_warnings(record=True) as l_warns:
    show_m = horizon(surfaces=surfaces, return_showm=True)
    analysis = window.analyze_scene(show_m.scene)
    npt.assert_equal(analysis.actors, 0)
    check_for_warnings(l_warns, 'Faces do not have correct shape: (100, 4)')
```

## Next Steps


---

*Source: test_apps.py:299 | Complexity: Advanced | Last updated: 2026-05-18*