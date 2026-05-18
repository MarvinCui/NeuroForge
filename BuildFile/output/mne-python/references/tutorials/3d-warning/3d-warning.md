# How To: 3D Warning

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: Test that warnings are emitted for old Mesa.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `platform`
- `sys`
- `numpy`
- `pytest`
- `matplotlib.font_manager`
- `mne.utils`
- `mne.viz`
- `mne.viz.backends._utils`
- `mne.viz.backends.renderer`
- `mne.viz.backends`
- `mne.viz.backends._pyvista`

**Setup Required:**
```python
# Fixtures: renderer_pyvistaqt, monkeypatch
```

## Step-by-Step Guide

### Step 1: 'Test that warnings are emitted for old Mesa.'

```python
'Test that warnings are emitted for old Mesa.'
```

**Verification:**
```python
assert _is_osmesa(plotter)
```

### Step 2: Assign fig = renderer_pyvistaqt.create_3d_figure(...)

```python
fig = renderer_pyvistaqt.create_3d_figure((800, 600))
```

**Verification:**
```python
assert _is_osmesa(plotter)
```

### Step 3: Assign plotter = value

```python
plotter = fig.plotter
```

**Verification:**
```python
assert not _is_osmesa(plotter)
```

### Step 4: Assign pre = 'OpenGL renderer string: '

```python
pre = 'OpenGL renderer string: '
```

**Verification:**
```python
assert not _is_osmesa(plotter)
```

### Step 5: Assign good = value

```python
good = f'{pre}OpenGL 3.3 (Core Profile) Mesa 20.0.8 via llvmpipe (LLVM 10.0.0, 256 bits)\n'
```

### Step 6: Assign bad = value

```python
bad = f'{pre}OpenGL 3.3 (Core Profile) Mesa 18.3.4 via llvmpipe (LLVM 7.0, 256 bits)\n'
```

### Step 7: Call monkeypatch.setattr()

```python
monkeypatch.setattr(platform, 'system', lambda: 'Linux')
```

### Step 8: Call monkeypatch.setattr()

```python
monkeypatch.setattr(plotter.ren_win, 'ReportCapabilities', lambda: good)
```

### Step 9: Call monkeypatch.setenv()

```python
monkeypatch.setenv('MNE_IS_OSMESA', 'false')
```

**Verification:**
```python
assert _is_osmesa(plotter)
```

### Step 10: Call monkeypatch.setattr()

```python
monkeypatch.setattr(plotter.ren_win, 'ReportCapabilities', lambda: bad)
```

### Step 11: Assign non = value

```python
non = f'{pre}OpenGL 4.1 Metal - 76.3 via Apple M1 Pro\n'
```

### Step 12: Call monkeypatch.setattr()

```python
monkeypatch.setattr(plotter.ren_win, 'ReportCapabilities', lambda: non)
```

**Verification:**
```python
assert not _is_osmesa(plotter)
```

### Step 13: Assign non = value

```python
non = f'{pre}OpenGL 4.5 (Core Profile) Mesa 24.2.3-1ubuntu1 via NVE6\n'
```

### Step 14: Call monkeypatch.setattr()

```python
monkeypatch.setattr(plotter.ren_win, 'ReportCapabilities', lambda: non)
```

**Verification:**
```python
assert not _is_osmesa(plotter)
```


## Complete Example

```python
# Setup
# Fixtures: renderer_pyvistaqt, monkeypatch

# Workflow
'Test that warnings are emitted for old Mesa.'
fig = renderer_pyvistaqt.create_3d_figure((800, 600))
from mne.viz.backends._pyvista import _is_osmesa
plotter = fig.plotter
pre = 'OpenGL renderer string: '
good = f'{pre}OpenGL 3.3 (Core Profile) Mesa 20.0.8 via llvmpipe (LLVM 10.0.0, 256 bits)\n'
bad = f'{pre}OpenGL 3.3 (Core Profile) Mesa 18.3.4 via llvmpipe (LLVM 7.0, 256 bits)\n'
monkeypatch.setattr(platform, 'system', lambda: 'Linux')
monkeypatch.setattr(plotter.ren_win, 'ReportCapabilities', lambda: good)
monkeypatch.setenv('MNE_IS_OSMESA', 'false')
assert _is_osmesa(plotter)
monkeypatch.setattr(plotter.ren_win, 'ReportCapabilities', lambda: bad)
with pytest.warns(RuntimeWarning, match='18\\.3\\.4 is too old'):
    assert _is_osmesa(plotter)
non = f'{pre}OpenGL 4.1 Metal - 76.3 via Apple M1 Pro\n'
monkeypatch.setattr(plotter.ren_win, 'ReportCapabilities', lambda: non)
assert not _is_osmesa(plotter)
non = f'{pre}OpenGL 4.5 (Core Profile) Mesa 24.2.3-1ubuntu1 via NVE6\n'
monkeypatch.setattr(plotter.ren_win, 'ReportCapabilities', lambda: non)
assert not _is_osmesa(plotter)
```

## Next Steps


---

*Source: test_renderer.py:227 | Complexity: Advanced | Last updated: 2026-05-18*