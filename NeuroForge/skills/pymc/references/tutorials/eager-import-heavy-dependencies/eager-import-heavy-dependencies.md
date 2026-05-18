# How To: Eager Import Heavy Dependencies

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: `import pymc` must not eagerly load heavy optional dependencies.

These modules are deferred to first use to keep ``import pymc`` fast.
Note: ``scipy.sparse`` is intentionally omitted because ``xarray`` pulls it
in transitively, which is outside of pymc's control.

## Prerequisites

**Required Modules:**
- `subprocess`
- `sys`
- `textwrap`
- `types`
- `pymc`


## Step-by-Step Guide

### Step 1: "`import pymc` must not eagerly load heavy optional dependencies.\n\n    These modules are deferred to first use to keep ``import pymc`` fast.\n    Note: ``scipy.sparse`` is intentionally omitted because ``xarray`` pulls it\n    in transitively, which is outside of pymc's control.\n    "

```python
"`import pymc` must not eagerly load heavy optional dependencies.\n\n    These modules are deferred to first use to keep ``import pymc`` fast.\n    Note: ``scipy.sparse`` is intentionally omitted because ``xarray`` pulls it\n    in transitively, which is outside of pymc's control.\n    "
```

**Verification:**
```python
assert not loaded, f'`import pymc` eagerly loaded heavy modules: {loaded}. These should be deferred to first use.\n' + '\n'.join(lines[1:])
```

### Step 2: Assign expensive_modules = value

```python
expensive_modules = ('arviz_base', 'arviz_plots', 'arviz_stats', 'pytensor.sparse', 'scipy.cluster', 'scipy.interpolate', 'scipy.linalg', 'scipy.optimize', 'scipy.spatial', 'scipy.special', 'scipy.stats', 'zarr')
```

### Step 3: Assign code = textwrap.dedent.format(...)

```python
code = textwrap.dedent("        import builtins, sys, traceback\n        _targets = set({targets})\n        _traces, _real = {{}}, builtins.__import__\n        def _hook(name, *a, **kw):\n            if name in _targets and name not in sys.modules and name not in _traces:\n                _traces[name] = ''.join(traceback.format_stack())\n            return _real(name, *a, **kw)\n        builtins.__import__ = _hook\n        import pymc\n        loaded = [m for m in sorted(_targets) if m in sys.modules]\n        print(','.join(loaded))\n        for m in loaded[:3]:\n            print(f'--- {{m}} ---')\n            print(_traces.get(m, '(no trace)'))\n    ").format(targets=expensive_modules)
```

### Step 4: Assign result = subprocess.run(...)

```python
result = subprocess.run([sys.executable, '-c', code], check=True, capture_output=True, text=True)
```

### Step 5: Assign lines = result.stdout.strip.split(...)

```python
lines = result.stdout.strip().split('\n')
```

### Step 6: Assign loaded = value

```python
loaded = [m for m in lines[0].split(',') if m]
```

**Verification:**
```python
assert not loaded, f'`import pymc` eagerly loaded heavy modules: {loaded}. These should be deferred to first use.\n' + '\n'.join(lines[1:])
```


## Complete Example

```python
# Workflow
"`import pymc` must not eagerly load heavy optional dependencies.\n\n    These modules are deferred to first use to keep ``import pymc`` fast.\n    Note: ``scipy.sparse`` is intentionally omitted because ``xarray`` pulls it\n    in transitively, which is outside of pymc's control.\n    "
expensive_modules = ('arviz_base', 'arviz_plots', 'arviz_stats', 'pytensor.sparse', 'scipy.cluster', 'scipy.interpolate', 'scipy.linalg', 'scipy.optimize', 'scipy.spatial', 'scipy.special', 'scipy.stats', 'zarr')
code = textwrap.dedent("        import builtins, sys, traceback\n        _targets = set({targets})\n        _traces, _real = {{}}, builtins.__import__\n        def _hook(name, *a, **kw):\n            if name in _targets and name not in sys.modules and name not in _traces:\n                _traces[name] = ''.join(traceback.format_stack())\n            return _real(name, *a, **kw)\n        builtins.__import__ = _hook\n        import pymc\n        loaded = [m for m in sorted(_targets) if m in sys.modules]\n        print(','.join(loaded))\n        for m in loaded[:3]:\n            print(f'--- {{m}} ---')\n            print(_traces.get(m, '(no trace)'))\n    ").format(targets=expensive_modules)
result = subprocess.run([sys.executable, '-c', code], check=True, capture_output=True, text=True)
lines = result.stdout.strip().split('\n')
loaded = [m for m in lines[0].split(',') if m]
assert not loaded, f'`import pymc` eagerly loaded heavy modules: {loaded}. These should be deferred to first use.\n' + '\n'.join(lines[1:])
```

## Next Steps


---

*Source: test_root_namespace.py:91 | Complexity: Intermediate | Last updated: 2026-05-18*