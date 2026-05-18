# How To: Plugin Stub Links

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test plugin stub links

## Prerequisites

**Required Modules:**
- `http.client`
- `importlib`
- `pytest`
- `requests`
- `psychopy`
- `psychopy.plugins`


## Step-by-Step Guide

### Step 1: Assign knownStubModules = value

```python
knownStubModules = ['psychopy.microphone', 'psychopy.hardware.cedrus', 'psychopy.hardware.emulator', 'psychopy.hardware.gammasci', 'psychopy.hardware.minolta', 'psychopy.hardware.minolta', 'psychopy.hardware.pr', 'psychopy.hardware.crs.bits', 'psychopy.hardware.crs.optical', 'psychopy.hardware.crs.shaders', 'psychopy.visual.movie2', 'psychopy.visual.movie3', 'psychopy.visual.noise', 'psychopy.visual.patch', 'psychopy.visual.radial', 'psychopy.visual.ratingscale', 'psychopy.visual.secondorder', 'psychopy.hardware.brainproducts', 'psychopy.hardware.forp', 'psychopy.hardware.iolab', 'psychopy.hardware.labjacks', 'psychopy.hardware.qmix', 'psychopy.hardware.bbtk', 'psychopy.sound.backend_pyo', 'psychopy.sound.backend_sounddevice', 'psychopy.visual.backends.glfwbackend']
```

**Verification:**
```python
assert docsHome.ok, f'No documentation found at {cls.docsHome} (PluginStub for {cls.__module__}:{cls.__name__})'
```

### Step 2: Assign resp = requests.get(...)

```python
resp = requests.get('https://psychopy.org')
```

**Verification:**
```python
assert docsLink.ok, f'No documentation found at {cls.docsLink} (PluginStub for {cls.__module__}:{cls.__name__})'
```

### Step 3: Call importlib.import_module()

```python
importlib.import_module(stubModule)
```

### Step 4: Call pytest.skip()

```python
pytest.skip()
```

**Verification:**
```python
assert docsHome.ok, f'No documentation found at {cls.docsHome} (PluginStub for {cls.__module__}:{cls.__name__})'
```

### Step 5: Assign docsHome = requests.get(...)

```python
docsHome = requests.get(cls.docsHome)
```

### Step 6: Assign docsLink = requests.get(...)

```python
docsLink = requests.get(cls.docsLink)
```

### Step 7: Call pytest.skip()

```python
pytest.skip()
```


## Complete Example

```python
# Workflow
knownStubModules = ['psychopy.microphone', 'psychopy.hardware.cedrus', 'psychopy.hardware.emulator', 'psychopy.hardware.gammasci', 'psychopy.hardware.minolta', 'psychopy.hardware.minolta', 'psychopy.hardware.pr', 'psychopy.hardware.crs.bits', 'psychopy.hardware.crs.optical', 'psychopy.hardware.crs.shaders', 'psychopy.visual.movie2', 'psychopy.visual.movie3', 'psychopy.visual.noise', 'psychopy.visual.patch', 'psychopy.visual.radial', 'psychopy.visual.ratingscale', 'psychopy.visual.secondorder', 'psychopy.hardware.brainproducts', 'psychopy.hardware.forp', 'psychopy.hardware.iolab', 'psychopy.hardware.labjacks', 'psychopy.hardware.qmix', 'psychopy.hardware.bbtk', 'psychopy.sound.backend_pyo', 'psychopy.sound.backend_sounddevice', 'psychopy.visual.backends.glfwbackend']
for stubModule in knownStubModules:
    importlib.import_module(stubModule)
resp = requests.get('https://psychopy.org')
if not resp.ok:
    pytest.skip()
for cls in PluginStub.__subclasses__():
    if cls.__module__.startswith('psychopy.tests'):
        continue
    try:
        docsHome = requests.get(cls.docsHome)
        docsLink = requests.get(cls.docsLink)
    except RemoteDisconnected:
        pytest.skip()
    assert docsHome.ok, f'No documentation found at {cls.docsHome} (PluginStub for {cls.__module__}:{cls.__name__})'
    assert docsLink.ok, f'No documentation found at {cls.docsLink} (PluginStub for {cls.__module__}:{cls.__name__})'
```

## Next Steps


---

*Source: test_plugin_stubs.py:71 | Complexity: Advanced | Last updated: 2026-05-18*