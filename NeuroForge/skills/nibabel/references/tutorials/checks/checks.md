# How To: Checks

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test checks

## Prerequisites

**Required Modules:**
- `logging`
- `io`
- `pytest`
- `batteryrunners`


## Step-by-Step Guide

### Step 1: Assign battrun = BatteryRunner(...)

```python
battrun = BatteryRunner((chk1,))
```

**Verification:**
```python
assert reports[0] == Report(KeyError, 20, 'no "testkey"', '')
```

### Step 2: Assign reports = battrun.check_only(...)

```python
reports = battrun.check_only({})
```

**Verification:**
```python
assert reports[0] == Report(KeyError, 20, 'no "testkey"', 'added "testkey"')
```

### Step 3: Assign unknown = battrun.check_fix(...)

```python
obj, reports = battrun.check_fix({})
```

**Verification:**
```python
assert obj == {'testkey': 1}
```

### Step 4: Assign battrun = BatteryRunner(...)

```python
battrun = BatteryRunner((chk1, chk2))
```

**Verification:**
```python
assert reports[0] == Report(KeyError, 20, 'no "testkey"', '')
```

### Step 5: Assign reports = battrun.check_only(...)

```python
reports = battrun.check_only({})
```

**Verification:**
```python
assert reports[1] == Report(KeyError, 20, 'no "testkey"', '')
```

### Step 6: Assign unknown = battrun.check_fix(...)

```python
obj, reports = battrun.check_fix({})
```

**Verification:**
```python
assert reports[0] == Report(KeyError, 20, 'no "testkey"', 'added "testkey"')
```

### Step 7: Assign output_obj = value

```python
output_obj = {'testkey': 0}
```

**Verification:**
```python
assert reports[1] == Report(ValueError, 10, '"testkey" != 0', 'set "testkey" to 0')
```


## Complete Example

```python
# Workflow
battrun = BatteryRunner((chk1,))
reports = battrun.check_only({})
assert reports[0] == Report(KeyError, 20, 'no "testkey"', '')
obj, reports = battrun.check_fix({})
assert reports[0] == Report(KeyError, 20, 'no "testkey"', 'added "testkey"')
assert obj == {'testkey': 1}
battrun = BatteryRunner((chk1, chk2))
reports = battrun.check_only({})
assert reports[0] == Report(KeyError, 20, 'no "testkey"', '')
assert reports[1] == Report(KeyError, 20, 'no "testkey"', '')
obj, reports = battrun.check_fix({})
output_obj = {'testkey': 0}
assert reports[0] == Report(KeyError, 20, 'no "testkey"', 'added "testkey"')
assert reports[1] == Report(ValueError, 10, '"testkey" != 0', 'set "testkey" to 0')
assert obj == output_obj
```

## Next Steps


---

*Source: test_batteryrunners.py:159 | Complexity: Intermediate | Last updated: 2026-05-18*