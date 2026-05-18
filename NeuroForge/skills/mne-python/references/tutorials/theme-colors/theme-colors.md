# How To: Theme Colors

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, pytest, workflow, integration

## Overview

Workflow: Test that theme colors propagate properly.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `platform`
- `colorsys`
- `numpy`
- `pytest`
- `mne`
- `mne.io`
- `mne.utils`
- `mne.viz.backends._utils`
- `matplotlib.colors`

**Setup Required:**
```python
# Fixtures: pg_backend, theme, monkeypatch, tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test that theme colors propagate properly.'

```python
'Test that theme colors propagate properly.'
```

**Verification:**
```python
assert is_dark, theme
```

### Step 2: Assign darkdetect = pytest.importorskip(...)

```python
darkdetect = pytest.importorskip('darkdetect')
```

**Verification:**
```python
assert not is_dark, theme
```

### Step 3: Call monkeypatch.setenv()

```python
monkeypatch.setenv('_MNE_FAKE_HOME_DIR', str(tmp_path))
```

**Verification:**
```python
assert dark == want_dark, f'{widget} dark={dark} want_dark={want_dark}'
```

### Step 4: Call monkeypatch.delenv()

```python
monkeypatch.delenv('MNE_BROWSER_THEME', raising=False)
```

**Verification:**
```python
assert dark == want_dark, f'{widget} dark={dark} want_dark={want_dark}'
```

### Step 5: Call monkeypatch.setattr()

```python
monkeypatch.setattr(darkdetect, 'theme', lambda: 'light')
```

**Verification:**
```python
assert_correct_darkness(widget, is_dark)
```

### Step 6: Assign raw = RawArray(...)

```python
raw = RawArray(np.zeros((1, 1000)), create_info(1, 1000.0, 'eeg'))
```

### Step 7: Assign unknown = _check_qt_version(...)

```python
_, api = _check_qt_version(return_api=True)
```

### Step 8: Assign fig = raw.plot(...)

```python
fig = raw.plot(theme=theme)
```

### Step 9: Assign is_dark = _qt_is_dark(...)

```python
is_dark = _qt_is_dark(fig)
```

### Step 10: Call pytest.skip()

```python
pytest.skip('Problems on macOS')
```

**Verification:**
```python
assert is_dark, theme
```

### Step 11: Assign __tracebackhide__ = True

```python
__tracebackhide__ = True
```

### Step 12: Assign bgcolor = value

```python
bgcolor = widget.palette().color(widget.backgroundRole()).getRgbF()[:3]
```

### Step 13: Assign dark = value

```python
dark = rgb_to_hls(*bgcolor)[1] < 0.5
```

**Verification:**
```python
assert dark == want_dark, f'{widget} dark={dark} want_dark={want_dark}'
```

### Step 14: Assign colors = value

```python
colors = _pixmap_to_ndarray(widget.grab())[:, :, :3]
```

### Step 15: Assign dark = value

```python
dark = colors.mean() < 0.5
```

**Verification:**
```python
assert dark == want_dark, f'{widget} dark={dark} want_dark={want_dark}'
```

### Step 16: Call assert_correct_darkness()

```python
assert_correct_darkness(widget, is_dark)
```

**Verification:**
```python
assert not is_dark, theme
```


## Complete Example

```python
# Setup
# Fixtures: pg_backend, theme, monkeypatch, tmp_path

# Workflow
'Test that theme colors propagate properly.'
darkdetect = pytest.importorskip('darkdetect')
monkeypatch.setenv('_MNE_FAKE_HOME_DIR', str(tmp_path))
monkeypatch.delenv('MNE_BROWSER_THEME', raising=False)
monkeypatch.setattr(darkdetect, 'theme', lambda: 'light')
raw = RawArray(np.zeros((1, 1000)), create_info(1, 1000.0, 'eeg'))
_, api = _check_qt_version(return_api=True)
fig = raw.plot(theme=theme)
is_dark = _qt_is_dark(fig)
if platform.system() == 'Darwin':
    pytest.skip('Problems on macOS')
if theme == 'dark':
    assert is_dark, theme
elif theme == 'light':
    assert not is_dark, theme

def assert_correct_darkness(widget, want_dark):
    __tracebackhide__ = True
    bgcolor = widget.palette().color(widget.backgroundRole()).getRgbF()[:3]
    dark = rgb_to_hls(*bgcolor)[1] < 0.5
    assert dark == want_dark, f'{widget} dark={dark} want_dark={want_dark}'
    colors = _pixmap_to_ndarray(widget.grab())[:, :, :3]
    dark = colors.mean() < 0.5
    assert dark == want_dark, f'{widget} dark={dark} want_dark={want_dark}'
for widget in (fig.mne.toolbar, fig.statusBar()):
    assert_correct_darkness(widget, is_dark)
```

## Next Steps


---

*Source: test_utils.py:55 | Complexity: Advanced | Last updated: 2026-05-18*