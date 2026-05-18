# How To: Io Fetch Fetcher Datanames

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test io fetch fetcher datanames

## Prerequisites

**Required Modules:**
- `importlib`
- `inspect`
- `logging`
- `pathlib`
- `shutil`
- `sys`
- `tempfile`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.data.fetcher`
- `dipy.direction.peaks`
- `dipy.io.image`
- `dipy.io.peaks`
- `dipy.io.streamline`
- `dipy.io.utils`
- `dipy.reconst`
- `dipy.reconst.shm`
- `dipy.testing`
- `dipy.utils.optpkg`
- `dipy.utils.tripwire`
- `dipy.workflows.base`
- `dipy.workflows.io`


## Step-by-Step Guide

### Step 1: Assign available_data = FetchFlow.get_fetcher_datanames(...)

```python
available_data = FetchFlow.get_fetcher_datanames()
```

### Step 2: Assign module_path = 'dipy.data.fetcher'

```python
module_path = 'dipy.data.fetcher'
```

### Step 3: Assign ignored_fetchers = value

```python
ignored_fetchers = ['fetch_data']
```

### Step 4: Assign fetcher_list = value

```python
fetcher_list = {name.replace('fetch_', ''): func for name, func in getmembers(fetcher_module, isfunction) if name.lower().startswith('fetch_') and name.lower() not in ignored_fetchers}
```

### Step 5: Assign num_expected_fetch_methods = len(...)

```python
num_expected_fetch_methods = len(fetcher_list)
```

### Step 6: Call npt.assert_equal()

```python
npt.assert_equal(len(available_data), num_expected_fetch_methods)
```

### Step 7: Call npt.assert_equal()

```python
npt.assert_equal(all((dataset_name in available_data.keys() for dataset_name in fetcher_list)), True)
```

### Step 8: Assign fetcher_module = importlib.reload(...)

```python
fetcher_module = importlib.reload(sys.modules[module_path])
```

### Step 9: Assign fetcher_module = importlib.import_module(...)

```python
fetcher_module = importlib.import_module(module_path)
```


## Complete Example

```python
# Workflow
available_data = FetchFlow.get_fetcher_datanames()
module_path = 'dipy.data.fetcher'
if module_path in sys.modules:
    fetcher_module = importlib.reload(sys.modules[module_path])
else:
    fetcher_module = importlib.import_module(module_path)
ignored_fetchers = ['fetch_data']
fetcher_list = {name.replace('fetch_', ''): func for name, func in getmembers(fetcher_module, isfunction) if name.lower().startswith('fetch_') and name.lower() not in ignored_fetchers}
num_expected_fetch_methods = len(fetcher_list)
npt.assert_equal(len(available_data), num_expected_fetch_methods)
npt.assert_equal(all((dataset_name in available_data.keys() for dataset_name in fetcher_list)), True)
```

## Next Steps


---

*Source: test_io.py:165 | Complexity: Advanced | Last updated: 2026-05-18*